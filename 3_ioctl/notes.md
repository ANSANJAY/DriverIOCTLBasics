The ioctl driver method has a prototype that differs somewhat from the user space version:

long (*unlocked_ioctl) (struct file *filp, unsigned int cmd, 
                            unsigned long arg);


The filp pointer is the value corresponding to the file descriptor fd passed on by the application and is the same parameters to the open method.

The cmd argument is passed from the user unchanged, and the optional arg argument is passed in the form of an unsigned long
