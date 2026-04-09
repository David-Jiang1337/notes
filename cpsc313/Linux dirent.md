The Linux *dirent* (directory entry) struct is used to represent a mapping from a file name to an inode. Specifically, *dirents* typically represent contents of their directory, with the exception of the *.* file which refers to the directory itself and the *..* file which refers to the parent directory.

For the purposes of CPSC 313, the directory entry is defined as such:
```c
struct dirent 
{
	uint8_t de_type;
	uint8_t de_namelen;
	uint16_t de_reserved;
	ino_t de_ino;
	char de_name[256];
}
```
where `de_type` represents the type of file, `de_namelen` represents the length of the name. `de_reserved` is unused space reserved for future use, `de_ino` represents the inode, and `de_name` represents the name corresponding to the inode.

A special property of the `dirent` struct is that its total size is aligned to 4 bytes, rather than being aligned to a multiple of the size of the largest type contained within. Furthermore, because this size is calculated based on the length of `dirent`'s fields and the length of the name, there is no guarantee of a null character at the end of the string `de_name`.