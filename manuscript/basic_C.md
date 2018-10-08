# Basic things about C you need to know

- Fixed size variable types in C
- Masking to access single bits
- Memory organisation of 32 bit processor
- Accessing registers in memory with pointers
- Multiple files - the project structure

## Variable sizes in C

Since int does not have a standardised size C99 introduced a library with fixed size variable types

```C
#include <inttypes.h>
```

Make sure that you add this library if you are using a processor-specific IDE!

Examples:
```C
uint32_t LongVariable;
uint8_t ByteVariable; /* 0..255 */
int16_t SignedVariable /*−32,768..32,767 */
```

## Masking

Masking is when you want to access single bits in e.g. a memory register.

Masking is necessary if you want to know the value of a single bit in `uint16_t statusRegister;

````C
if (statusRegister & 0x0100) {
    /* False if bit 8 is 0 */
    /* True if bit 8 is 1 */
}
```

All the ways below are equal in saying bit 8 is set to 1
```C
0b00000000100000000
0x0100U
(1 << (8))
```

*Note! The rightmost bit is bit 0! Not bit 1!*

But what if you want to check if exactly the wanted bits are set?

```C
if (statusRegister & 0x0102) {
    /* True if bit 8 and bit 1 is 1 */
    /* True if bit 8 is 1 and bit 1 is 0 */
    /* True if bit 8 is 0 and bit 1 is 1 */
}
```
Obviously not correct! The solution is to mask the register, and then compare with the mask

```C
if ((statusRegister & 0x0102) == 0x0102) {

}
```

If I want to set the value of a single bit in an I/O-register `uint16_t controlRegister;`

All these expressions are equal in identifying bit 6
```C
0b00000000001000000
0x040U
(1 << (6))
```
The following two lines of code are equivalent in C
```C
controlRegister = controlRegister | 0x0040;
controlRegister |=  0x0040;
```
and both forces bit 6 to 1, all other bits keep their values. *Note that this is tricky since you can be led to beleive that you acutally set the register with a single assembly instruction, but most processors will have to use several instrucitons to accomplish this.* We will talk more about this in the chapter in on interrupts.




