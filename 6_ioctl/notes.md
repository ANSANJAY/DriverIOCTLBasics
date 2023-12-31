===========================================
Defining ioctl() commands
==========================================

Programmers much choose a number for the integer command representing each command implemented through ioctl.

Normally many programmers choose a set of small numbers starting with 0 or 1 and go up from there.


Picking arbitrary number is a bad idea, because:

        Two device nodes may have the same major number

        An application could open more than one device and mix up the file descriptors,  thereby sending the right command to the wrong device.

        Sending wrong ioctl commands can have catastrophic consequences, including damage to hardware.

Example: Program might find itself trying to change the baud rate of non-serial port input stream, such as FIFO or an audio device.

To help programmers create unique ioctl command codes, ioctl codes have been divided into four bitfields.

1. type/magic number:
	
	8 - bit Wide
	Choose one number after looking into  Documentation/ioctl-number.txt and use it throughout the driver

2. number:
	8-bits wide
	sequential number you assign to your command

3. direction:
	Direction of data transfer.
	Possible values:
		_IOC_NONE(NO Data Transfer)
		_IOC_READ 	--> Reading from the device, driver must write into userspace
		_IOC_WRITE
		_IOC_READ|_IOC_WRITE

4. size:

	Size of the user data involved.
	Width depends on the architecture: usually 13 or 14 bits
	You can find its value for your specific architecture in the macro _IOC_SIZEBITS

Header File: <linux/ioctl.h>

This above header file defines macro that help set up the command numbers as follows:

_IO(type, nr) (for a command that has no argument)
_IOR(type, nr, datatype) (for reading data from the driver)
_IOW(type, nr, datatype) (for writing data to the driver)
_IOWR(type, nr, datatype) (for bidirectional data transfer)

Type and number fields are passed as arguments and size field is derived by applying sizeof to the datatype argument.
