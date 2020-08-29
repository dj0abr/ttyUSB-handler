# ttyUSB-finder
a common problem with serial-USB converters is the the randomly assigned number.
This number depends on the sequence the OS detects the USB adapter.
You can never be sure if your USBserial adapter got ttyUSB0 or ttyUSB1 and so on.
This makes it painful to write a program which reliably uses a serial port. With the next power down/up it may stop working.

This piece of software solves this problem by using the serialID and vendorID of a USBserial adapter.

These steps are required:


