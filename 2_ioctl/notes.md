BLKGETSIZE ioctl returns unsigned long , it may fail if the size is 2TB or greater. 

For this reason it is better to use BLKGETSIZE64  which produces a 64-bit result which is the size in bytes

Header File: <linux/fs.h>


