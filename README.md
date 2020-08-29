# ttyUSB-finder
a common problem with serial-USB converters is the randomly assigned number.
This number depends on the sequence the OS detects the USB adapter.
You can never be sure if your USBserial adapter got ttyUSB0 or ttyUSB1 and so on.
This makes it painful to write a program which reliably uses a serial port. With the next power down/up it may stop working.

This piece of software solves this problem by using the serialID and vendorID of a USBserial adapter.

These steps are required:

## 1) find the serial ID and vendor ID of your adapter. 
Connect ONLY ONE serialUSB adapter to your computer!
This is done with these commands in the linux terminal:

> udevadm info -a -p  $(udevadm info -q path -n /dev/ttyUSB0) | grep '{serial}' | cut -d \" -f2 | head -n 1

> udevadm info -a -p  $(udevadm info -q path -n /dev/ttyUSB0) | grep '{idVendor}' | cut -d \" -f2 | head -n 1

manually put the result of above commands into a static string or a #define statement

## 2) open the serial interface:
make a call to:

> init_serial_interface(char *idserial, char *idVendor, int speed)

and use the output of above commands as parameters, also specify the serial speed as parameter i.e: B9600

this init function automatically creates a new thread and a communication pipe.

3) the get the received data from the serialUSB port simply check if the receive pipe is filled with data:

> read_pipe(idx, 'r')

for more details see the description at the beginning of the C files.

good luck
Kurt, DJ0ABR

