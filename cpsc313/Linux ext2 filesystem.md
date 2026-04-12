
The Linux "ext2" second extended filesystem developed in 1993 was a relatively simple filesystem that serves now as the basis of the newer ext3 and ext4 filesystems on Linux.

## Filesystem Metadata
The metadata stored on an ext2 superblock is similar to most other filesystems, containing data about the number of total blocks, number of free blocks, block size, etc. However, it also contained some fields which are unique to ext2 like:
- `s_blocks_per_group` representing the number of blocks per group
- `s_inodes_per_group` representing the number of inodes per group
- `s_log_block_size` representing the size of a block.

## Disk Layout
The block size on ext2 is configurable to `1024 B` times a power of $2$, usually `1024 B`, `2048 B`, or `4096 B`.  The superblock, rather than always being stored at PBN $1$ (the second block on the disk), is stored at exactly offset `1024 B`. This means that it will show up at PBN 1 on a file of block size `1024 B`, but will occupy the second half of PBN $0$ for a block size of `2048 B`. 
### Block Groups
On ext2, blocks are organized into block groups to allow for more frequent contiguous allocation, reducing the [[Quiz 5 Information]]number of seeks needed to read a file. Each block group contains a block dedicated to a data block bitmap representing which blocks in the group are free and which ones are in use, as well as an inode bitmap to do the same for inodes. 

Each block group also contains some blocks dedicated to inodes. Furthermore, a copy of the superblock and block descriptor table will be stored at the beginning of block groups 0 and 1, as well as in any block group $i$ where $i$ is a power of $3$, $5$, or $7$.

The presence of these redundant superblocks allows the filesystem to possibly recover if a superblock is corrupted by consulting other superblocks.
#### Block Group Size
A good way to determine how many blocks should be in one block group is to look at how many bits are in a block, because that will be how many blocks our one-block bitmap can account for. We also need to account for how many inodes can be accommodated by the inode bitmap, which is the same number as the data block bitmap. In summary, our block group size needs to be big enough to fit:
- $1$ block for a data block bitmap
- $1$ block for an inode bitmap
- $1$ inode for each bit in the inode bitmap
- $1$ block for each bit in the data block bitmap

For example, suppose we have an ext2 filesystem with a block size of `8192 B` with inodes of size `128 B`, and suppose it does not contain a superblock and block descriptor table.
First, we need $1$ block for the data block bitmap and $1$ for the inode bitmap. Then, since the block is `8192 B`, we can represent $8192 B \times \frac{8}{1 B} = 65536$ blocks. Hence we can store $65536$ inodes which will require $\frac{128B \times 65536}{8192B} = 1024$ blocks. Since the data bitmap will have the same number of blocks it can represent, we can add another $65536$ blocks for data.
Adding all these blocks together, we get:
$$1 \text{ (data bitmap)} + 1 \text{ (inode bitmap)} + 1024 \text{ (inode blocks)} + 65536 \text{ (data blocks)} = 66562$$
This represents $66562 \times 8192B = 545275904 B$ for one block group, or approximately `520 MB`.

## File Mappings
The ext2 filesystem used a hybrid index wherein the `ext2_inode` contained 15 32-bit PBNs. These blocks, in order, represented:
- $12$ direct data blocks
- $1$ indirect block
- $1$ double indirect block
- $1$ triple indirect block

## Directory Entries
The ext2 directory entry is defined as follows:
```c
struct ext2_dir_entry {
	_le32 inode;
	_le16 rec_len;
	_le16 name_len
	char name[256]
}
```
where `inode` represents the inode the directory entry is mapped to, `rec_len` is the total length of the `dirent`, `name_len` is the length of the name, and `name` is the name of the file the `dirent` is mapping. [[Linux dirent|In later filesystems]], the `rec_len` would be removed as the size of the entry can be calculated dynamically given `name_len`, `name_len` would be shortened to a type `uint8_t`, and the other $1$ byte of the longer `name_len` would be used to represent the file type. Like newer `dirent` structs, ext2 `dirent`s are aligned to $4$ bytes with no guarantee that the string is null-terminated.