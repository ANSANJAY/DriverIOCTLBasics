===================================================
Macros to decode information from the ioctl command
===================================================

_IOC_TYPE(cmd) /* gets the magic number of the device this command targets */

_IOC_NR( cmd) /* gets the sequential number of the command within your device */

_IOC_SIZE(cmd) /* gets the size of the data structure */

_IOC_DIR( cmd) /* gets the direction of data transfer,
                                can be one of the following:
                                _IOC_NONE
                                _IOC_READ
                                _IOC_WRITE
                                _IOC_READ | _IOC_WRITE
                                */

