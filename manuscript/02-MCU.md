# The heart of the system, the microcontroller

A CPU (as in a common computer) typically consist of 

- ...
- ... 


A micro controller unit (MCU) in an embedded system usually has a lot more diverse hardware included in the silicon package: RAM, flash memory, I/O, communication controllers, etc.

## A 32-bit processor from an application programmers perspective
8, 16, or 32-bit?

Traditionally embedded systems tend to use the smallest possible processor that can solve the task, due to cost optimisation of the electronic hardware and mechatronics. But if you look at the trends over the last twenty years you will see that Moore's law is applicable also for embedded MCUs, while the trend for mechatronics does not evolve that fast. In practice the part that is the CPU or MCU cost for an embedded systems goes down, while the system as a whole may cost the same as the years ago.

_How much do you need to know outside of your code?_

### von Neumann architecture
Most modern 32-bit MCUs use an architecture where everything is accessed through same memory area.  
This means not only program and data, but also hardware is accessed through what the programmer sees as memory.  
Accessing a specific I/O device means accessing a specific memory address, typically a 32 bit address on the form `0xDDCCBBAA`, e.g. accessing a digital I/O-port is done by accessing memory at address `0x400E1000-...`

The key to understand embedded software is to understand how this memory map works for the processor you are developing on. While it is possible to be a productive Java or Python programmer (But you will probably be a _better_ programmer if you understand how these languages handles memory) without thinking about memory it is impossible for an embedded programmer.





# Common devices

## Digital I/O

## PWM
## A/D-converter

```c
int main(void)
{
	uint32_t result;

	board_init();	/* general initializations */
	sysclk_init();	/* Starts the clock used for A/D conversion
	ADCSetup(0);	/* self-written function to get the A/D input 0 set up correctly */
	adc_start(ADC);	/* Starts the conversion */
	/* wait some time */
	result = adc_get_latest_value(ADC);	/*reads the 	latest analog value in the register */
}
```
## D/A-converter
## Power manager
## Timers

# Multi-core processors
To be adressed in the future...