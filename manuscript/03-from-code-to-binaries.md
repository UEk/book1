# Going from code to binaries

## Compiling and linking - a two step process

## Controlling memory usage
Memory is not an infinite resource, and most small operating systems and real-time kernels don't have reserved emery space for each thread, hence you will not only crash a single thread of it uses too much memory, it will most likely crash the entire system.

### The stack

### Dynamic allocation and why to avoid it

### Downloading the software to the device

#### Flash programming

#### Bootloader
The embedded bootloader preprogrammed to an microcontroller receives an application image over serial interface and writes it to the internal MCU flash.

The embedded bootloader occupies a small amount of memory.
It serves the only purpose, to load an application image from a serial interface and write it to the MCU’s internal flash and/or EEPROM.
A simple communication protocol is used to ensure proper programming.



#### Over the air programming