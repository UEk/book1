# Introduction

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris non erat maximus, vestibulum ante et, tempus velit. Morbi efficitur vel quam id pellentesque. Aenean commodo laoreet magna nec vehicula. Nam quis volutpat neque. Curabitur eu consectetur velit. Praesent at erat sagittis, ornare nisl sed, finibus leo. Donec ut mattis libero. Fusce semper, est eu luctus aliquam, nunc eros laoreet arcu, eu sodales nisi ante sed turpis. Praesent tristique neque congue felis lacinia, eu consectetur purus malesuada. Suspendisse ut pellentesque neque. Nullam laoreet odio risus, a laoreet odio rutrum quis. Praesent arcu felis, posuere sed massa quis, placerat iaculis neque. Praesent facilisis lectus ex, sit amet bibendum odio vehicula eget. Nullam non erat ac dolor vestibulum tristique et at dui.

Maecenas ante odio, pellentesque et tellus a, malesuada semper nulla. Duis tempor porttitor nisl, non feugiat ligula aliquet eget. Etiam sollicitudin lacinia neque. Praesent faucibus ipsum velit, et ultricies mauris vestibulum sit amet. Mauris placerat dui a ipsum lobortis, vitae ullamcorper urna porttitor. Sed id turpis laoreet, rhoncus neque nec, pellentesque felis. Nullam eu imperdiet enim. Donec non arcu venenatis, rhoncus mauris ut, consequat mi. Sed dignissim blandit lacus, sit amet pulvinar metus tincidunt rutrum. Suspendisse potenti. In justo risus, lacinia at libero id, maximus pharetra ex. Donec convallis est nec massa gravida condimentum.

## Overview of embedded systems
Embedded systems have a wide range of applications, but typical share some common characteristics:

- Deep integration between hardware and software for significant parts of the functionality
- Often mass-produced
- Strong focus on manufacturing aspects
- Supplier involvement
- Some parts may realise safety-critical functionality

### A classical domain of embedded systems: Automotive

Car manufacturers focus on the physical product, with an emphasis on manufacturing and maintenance/service. These aspects in turn drives the entire R&D process. The cost for the electrical system is 20 % - 40 % of the complete car.

A vehicle model is manufactured 105 products manufactured each year. A high end vehicle is typical made to customer order, which means that there could be more than 106 possible configurations of software parts, and order of magnitude higher than the actual number built.

A vehicle platform in is production 7-10 years. This means a new architecture, including software, for the electrical system is updated every 10th year. Changes in the design of software and hardware during this time are driven by e.g:

- new features
- legal requirements
- cost reductions

These changes are usually managed in projects targeted at a certain model year, or in some cases a new car model on an existing platform.

Even if  almost all functions are implemented and controlled by software the electrical distribution system (cable harness) still has traditional quality issues as well:

- Noise (vibration, rattle, squeek)
- Chafing
- Squashed cables
- Loose connector, terminals
- Fretting (plating)

## Characteristics: Functionality and qualities

### Requirements in vehicles

#### Cost
In mass-produced embedded systems the dominating cost is piece cost, i.e. what each component costs at assembly in the factory:

- A car model is manufactured in 200 000 each year
- The typical life-span for a car model is 7 years
- A saving of $1.50 on one component means a profit of $2 million

Other costs are

- Development cost, including testing
- Investment costs (e.g. manufacturing & testing tools)
- After-market costs (i.e. warranty)

The most common way is that development and tool costs are included in the piece cost by a supplier in mass production.
So the piece cost will go down the more components are manufactured, i.e. piece cost will decrease throughout the model life-cycle.


#### Safety

Many electrical functions enhance the safety of the vehicle:

- Passive safety mitigate the effects of an accident

	- Safety belts
	- Air bags
	- Pedestrian protection

- Active safety prevent accidents to happen

	- Exterior lights
	- ABS / traction control / ESP
	- Forward collision warning
	- Lane keeping aid
	- Collision avoidance

But, this put requirements both that the systems work when needed, e.g. the steering servo does not suddenly stop, and that they don’t have any unintended behaviour, e.g. air bags going off at the wrong time

Most of the safety requirements are solved by reconfigure/degrade the embedded function to a safe state when error occurs.
In some cases this is implemented by relying on a purely mechanical solution (e.g. hydraulic brakes versus ABS), or by just shutting the function down (e.g. air bags).
But the more complex the “system state” is, the more necessary it is to design a robust electrical system.

Almost all cars have throttle-by-wire, there is no mechanical connection between the pedal and the throttle, to be able to fulfil emission requirements at all driving situations.

_Safety requirement: Pedal failures must be detected_

This is implemented by having two position sensors (potentiometers). Using them there several plausibility checks for error detection are used:

- Min, is the measure value always over a certain value (above zero)?
- Max, is the measured value always under a certain value (typically VCC)?
- Do the two sensors have the same value?
- Correct sensor resistance at idling?
- Do the two sensor values change in the same direction?

Some statistics for Sweden

In August 2013 there were 4 622 422 registered vehicles in Sweden. Let's say they drive on average 15000 km a year, which is about 500 hours / year.
That means that the entire vehicle fleet runs 2,3x109 hours in a year. 289 persons died in traffic in 2012 in Sweden, 2976 were severely hurt.

So the probability to be killed in an accident is 1,4x10-6 / hour. Less than 10 % of all accidents are caused by technical errors (i.e. human error's are the cause for > 90%). So the probability of  technical error which causes a fatal accident in a vehicle is about 10-7 / hour. Pretty good engineering and software development...


#### Performance

_Performance requirement: Response time at “kick down” < 100 ms from “pedal to the metal” to torque increase, which includes physical inertia._

_Real-time requirement: Engine speed determines the hardest timing requirement_

When the vehicles is driving with 6000 rpm of the engine -> 1 crank shaft revolution takes 10 ms.

“Ballpark” accuracy necessary for diesel fuel injection: 7 injections during 30° of the full revolution -> 1 % resolution of position. 

The cylinder position is determined by crank shaft angle, and this means the crank shaft angle must be known within 0.1 ms based on a full revolution taking 1 ms. To avoid aliasing it is necessary to sample at twice that rate, this means crank shaft sampling must be done every 50 µs!





