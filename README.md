# Remora Nucleo F446ZE Hat PCB.
Design for a cost effective 6 Axis CNC motion controller card PCB. Designed to be a hat or shield for the ST Nucleo F446ZE. Uses a custom port of [Remora](https://github.com/scottalford75/Remora), making this a fully programmable real time motion control system for LinuxCNC with a lot of IO flexibility. Primarily designed for complex CNC milling our router machine builds. 

Kicad 9 Project. Note this repo is pre-release, large chunks of this circuit are still in design stages.  

## Goals - Our target design spec - To be revised as design progresses
- Nucleo F446ZE Hat/Shield for 6 axis LinuxCNC motion control using custom port of Remora built for STM32.
- Up to 6 axes of isolated, real time hardware step generation, configurable up to 200Khz. Can be used with any 5V single ended or differential stepper drivers. Unused axes can be reconfigured as differential digital outputs.   
- IO: 4 analog inputs, 28 digital inputs, 10 digital outputs (up to 30mA Sink Logic) - Outputs are configurable to be sink logic GPIO or PWM. Max 30mA sinking or sourcing capability. 
- 1x Isolated 0-10v DAC for spindle control. Additional indexing or direction control can be done with existing GPIO.
- Console logging available via the STLink Virtual Comm port to view and debug Remora's console logging.
- 24V DC power input, configurable isolation via jumpers of 5V and GND lines used for stepper drivers and IO.
- 1x User programmable button

## Todos
- Validate mechanical fit of pin headers and mounting screw locations against physical hardware.
- Validate the isolated stepper driver design, min 200Khz, ideally up to 1Mhz. What is LinuxCNC / Remora maximum? Ensure we can exceed it and update specs once cap is set.
- Create a test Remora configuration and determine maximum number of IO to complete the spec and inform physical wiring.
- Test if USART LED design will work on standard vanilla Nucleo jumper configuration, if it requires alteration, the feature will be deleted. 
- Verify a sample of each peripheral design before committing to laying out PCB: Stepper driver, Digital Input, Analog Input, Digital Output + PWM, Spindle DAC, regulators, console logging, programmable button, reset button, user LED with default blinky program loaded into PRU.  
- After verification, estimate current draw. Redesign 12V, 5V and 3.3V switch mode supplies for peak efficiency and ripple rejection. Add in some thermal resets.
- PCB Layout of verified design along with new PSUs. Send for prototyping
- Once physical hardware tested and verified, commit gerbers
- Issue a BOM with Digikey part numbers
- Put up some photos of the completed PCB
- Write a build guide. Including J1 and J3 settings from Nucleo Manual needed to use on board power supplies. 

## Firmware
WIP firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-W5500

