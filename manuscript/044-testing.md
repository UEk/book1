# Testing code

## Unit testing embedded devices
Test-drive development (TDD) is a systematic way to develop code. The basic principle is that every function (unit) will have test cases when you are done.

TDD is popular in agile software development, but is not as common in development of embedded systems. However having a nearly complete set of automated test cases could be consider ”state-of-the-art development”. Since every function has a set of test cases I can clean or optimise the code without risking something stops working (assuming that I have committed the latest working version to the repo).

This will just be a short introduction to TDD, for a full in-depth treatment read James Grennings excellent book. However I will focus on some aspects of doing TDD on the target hardware, which is usually not recommended, but sometimes necessary.

![The cycle of test-driven development](pics/TDDcycle.png)

### Test project

![An example of how a project is organised for TDD](pics/TDDproject.png)

### The test list

The test list is a quick (?) list of what the function should be capable of. It should match the requirements specification. As soon as it becomes difficult to think of new test cases that adds new insights you stop. A first draft of a test list for a function should probably take less than 20 minutes.

### Example of a digital output test list

1. Port B pin 27 initialised as a digital output
1. Set pin 27 to high
1. Pin 27 to low
1. Pin 22 initialised as a digital output
1. Pin 22 to high
1. Pin 22 to low
1. Pin 27 and pin 22 initialised as outputs
1. Pin 13 and pin 22 both set to high
1. Pin 13 and pin 22 both set to low

### Pattern for an embedded test case


1. Assure that the observed state/output/whatever is in a usable starting point, 
2. Call the function to be tested through the API
3. Assure that the state/output/whatever have changed to the expected value.

An easy example of the testing pattern above when testing digital I/O . This particual test case evaluates if the output pin can be set to high level, and is done in three steps with the support of a unit test framework. 

1. Make sure pin has low level (read register)
1. Use API to set pin to high level
1. Make sure pin has high level (read register)

The test sequence above can be automated on the target hardware since it only relies on accessing the devices through the internal registers on the MCU.

Additional hardware testing, such as measure pin levels with a multimeter or LED, must the manual or have dedicated test benches.


#### Example unit test for analog-to-digital initialisation

In the following test step 1 is omitted since in some cases the external device is automatically enabled when resetting the MCU.

```c
void test_ACConverterIsInitialisedCorrectly(void)
/* Is the A/D converter initialised? */
{
	/* defining a pointer to the address of the ADC Channel Status Register ADC_CHSR */
	uint32_t *const p_ADC_CHSR = (uint32_t *) (0x400C0018U);

	/*Calling the function to be developed with a pin as argument */
	ADCSetup(11);

	/* checking that the corresponding ADC channel is enabled */
	TEST_ASSERT_BIT_HIGH(13, *p_ADC_CHSR);
}
```



### Mocking hardware