## Filesystem Metadata
Unix v6 has a filesystem metadata struct which we would now call a superblock. The struct is as such:
```c
struct filsys {
	int s_isize;        /* size in blocks of the I list */
	int s_fsize;        /* size in blocks of the entire volume */
	int s_nfree;        /* number of in core free blocks */
	int s_free[100];    /* in core free blocks */
	int s_ninode;       /* number of in core I nodes */
	int s_inode[100];   /* in core free I nodes */
	char s_flock;       /* lock during free list manipulation */
	char s_ilock;       /* lock during I list manipulation */
	char s_fmod;        /* super block modified flag */
	char s_ronly;       /* super block read-only flag */
	int s_time[2];      /* current date of last update */
	int pad[50];
}
```
We should keep in mind that during the time of Unix v6, `int` types were typically $2$ bytes long, as opposed to the default $4$ bytes of many modern systems, as the C specification states that the minimum length of an `int` is $2$ bytes.

## Disk Layout
The v6 filesystem begins with the boot block at PBN $0$, the super block at PBN $1$, some amount of contiguous blocks from PBN $[2, k]$ for inodes, and more contiguous blocks from PBN $[k+1, n]$ for data blocks. Each block was exactly `512 B` and each inode was exactly `32 B`.

Inodes in the v6 FS are structured thusly:
```c
struct ino {
	int i_mode;         /* File type, size, permissions */
	char i_nlink;       /* Link count */
	char i_uid;         /* Owner user id */
	char i_gid;         /* Group id */
	char i_size0;       /* most significant bits of size */
	int i_size1;        /* least sig */
	int i_addr[8];      /* Disk addresses of blocks */
	int i_atime[2];     /* Access time */
	int i_atime[2];     /* Modified time */
}
```
Where, again, `int` is a type of $2$ bytes.
### In Memory Vnode
The in memory inode (vnode) of a file with active IO contained some additional information compared to its on-disk equivalent related to IO operations like handling permissions:
```c
struct inode {
	char i_flag;
	char i_count;       /* reference count */
	int i_dev;          /* device where inode resides */
	int i_number;       /* i number 1:1 w/device addr */
	...                 /* on-disk inode fields in the same order */
	int i_lastr;        /* last logical block read */
}
```

## Free Space Management
In v6's disk layout, we notice there are no blocks explicitly dedicated to tracking free blocks. This is because free space is recorded as essentially an array of pointers to free blocks, where the first pointer's free block also serves as another node along the linked list where the `filsys` superblock represents the root node of the linked list. That is to say, the `int s_free[100]` field of `filsys` represents $100$ pointers to free blocks, and `filsys.s_free[0]` also represents the pointer to the next node in the linked list, which in turn contains $100$ more block pointers with the first one pointing to the next node. This strategy ensures no additional blocks are dedicated to counting free space since free blocks by definition do not need to be used to store user data and therefore can be used to store data about free blocks until they are allocated. When we need to allocate a block, we look at `filsys.s_nfree` to determine how many addresses in `filsys.s_free` are valid free blocks, and allocate `filsys.s_free[filsys.s_nfree -1]` , decrementing `filsys.s_nfree` afterwards to represent that pointer no longer being a free block. In the case that `filsys.s_nfree` is $1$ when allocation begins, the $100$ pointers and `nfree` inside the block at `filsys.s_free[0]` is loaded into `filsys`, basically advancing the head to deallocate the first node of the linked list. Inodes were also allocated in the same way.

## File Mappings
Unix v6 employed a multi-level hybrid approach to file mappings where the PBN pointers inside of the inode represented a tree of some height. `ino.i_addr` has a length of $8$, and for files which were $\le 8$ blocks long, each address in `ino.i_addr` represented a direct pointer to one of the data blocks. Once files exceeded $8$ blocks, the first $7$ indices $[0,6]$ represented single indirect blocks, and the final `ino.i_addr[7]` represented a double indirect block. Each block could contain $\frac{512B}{2B} =  256$ addresses, so the maximum size of a file on Unix v6 was $7 \cdot 256 \cdot 512B + 256^2 \cdot 512B = 34471936B = 32.875 MB$, which was considered very large in the late 1970s when Unix v6 was commonly in use.

## Directory Entries
Directory entries on Unix v6 were very simple, with a fixed length of `16 B`. They used $2$ bytes to store the inumber and $14$ bytes to store the name, meaning that the maximum character length of file names on v6 was $14$ characters:
```c
struct dirent {
	int d_ino;
	char d_name[14];
}
```

