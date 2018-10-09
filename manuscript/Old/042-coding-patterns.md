# C-coding patterns

## Code for accessing hardware

What if a pointer could point to a specific memory address?
Then I can control those memory registers controlling various hardware devices by writing to and reading from the pointee.

The declaration of a pointer to access a certain hardware address (in this example the A/D conversion control register) is quite straight forward:

```c
uint32_t *const p_ADC_CR = (uint32_t *) 0x400C0000U;
```

The declaration contains several elements

- `uint32_t` corresponds to the word-size of the processor, in this case 32 bits. Naturally it is unsigned.
- `*` states that the variable is a pointer to a 32-bit word
- `*const` states that the pointer will not change, i.e. this pointer variable will always point to the same memory address 
- `p_ADC_CR` is the pointer variable that vill be used in the program to access the hardware register 
- `(uint32_t *)`is an explicit typecasting for
- `0x400C0000U`, which is the address for the hardware register in the memory
- `=` assigns the value of pointing to an explicit memory address to the pointer variable at declaration time

_Note:_ In this particular case it is ok not to assign the pointer to a variable since we explicitly have stated it should point to a specific known memory adress, in this case A/D hardware.

With a pointer defined as above it is easy to start the analog-to-digital conversion in a program

```c
#define STARTADC 0x0002U /* bit 1 starts ADC */
*p_ADC_CR |= STARTADC;
```

With a nice `#define`

```c
#define ADC_CR (*p_ADC_CR)
```
It is possible to write

```c
ADC_CR |= STARTADC;
```



## Converting physical values to internal software representation

## Floating point variables and processors without

## Delays, timers and clocks

## State machines

## Buffers

## Software filters

## Interrupts