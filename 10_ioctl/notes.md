access_ok
==============

We need to take care of the arg parameter in the ioctl function, as it is a user space.

We can use copy_from_user/copy_to_user to safely copy data from user to kernel and vice versa.

These functions are less efficient in case of copying small data items. You can use put_user/get_user for copying 1, 2, 4 or 8 bytes

If you only want to verify the address without transferring data, you can use access_ok

Header File: <asm/uaccess.h>

int access_ok(int type, void *addr, unsigned long size);

type -> VERIFY_READ/VERIFY_WRITE: depending on action: reading the user space memory or writing it

addr -> user space address

size -> Depends on the ioctl command.

If you need to both read and write, use VERIFY_WRITE, it is a superset of VERIFY_READ

Return value: 1 for success, 0 for failure in this case you should return -EFAULT

Note: The 5.0 kernel dropped the type argument to access_ok()

https://lkml.org/lkml/2019/1/4/418


