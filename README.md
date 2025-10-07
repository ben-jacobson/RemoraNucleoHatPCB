# Remora Nucleo-144 Hat PCB.
Work in progress design for a cost-effective, highly customisable LinuxCNC motion control unit.

The form factor will be a hat/shield for ST Nucleo-144 evaluation boards using a WIZNet TOE for Ethernet control. The Nucleo can be loaded with a custom port of [Remora](https://github.com/scottalford75/Remora), link to specific firmware below. This designed should work for CNC milling machines, routers and plasma cutters. Lathes and laser cutters are in plan for future support.  

Schematics and board layout can be read with Kicad 9. Gerbers and PDF's of the schematics will become available on initial release. At this stage the design is pre-release with a lot of validation pending. At times during pre-release a preview of the schematics can be found in the PreviewSchematicMonthYear folder. 

## Proposed Features
- **Flexibile**: Lots of IO. Support for up to 6 axes.
- **Low cost**: Board can be fabricated via JLCPCB/PCBWay, parts can be ordered from Digikey/Mouser. 
- **Approachable**: Goal is to be well documented, providing step by step build guides.
- **Moderate skill requirement**: SMT soldering skills are required but the pad sizes will be forgiving enough for hand soldering. Hot air soldering will be possible but not required. Skills and knowledge requirements will be listed up front. 

## Design spec goals - To be revised as design progresses.
- Nucleo-144 Hat for 6 axis LinuxCNC motion control using custom port of Remora built for STM32.
- Up to 6 axes of isolated, hardware step generation. Default max step gen rate is 40Khz. Can be used with any 5V single ended or differential stepper drivers. Unused axes can be reconfigured as differential digital outputs.   
- IO: 2x analog inputs, 16x digital inputs, 8x digital outputs. 
- Digital Outputs can be configured as high/low sink logic or PWM. Can sink up to 40mA.
- 1x extra input for high speed differential AB encoders. Max RPM TBC. 
- 1x non-isolated 0-10v DAC for spindle control. Additional indexing or direction control to be done with digital outputs.
- Console logging available via UART port (TX only).
- 12-24V DC power input for powering Nucleo and supplying 3.3V to sections of the board that are isolated. Galvanic isolation between Nucleo and external devices is achieved by supplying your own isolated 5V supply. Or you can set a jumper and have the board supply 5V to your external devices. 

## Todos
- Finish Spindle DAC design
- Test if we still need 5V for WIZNET? What does this do for logic and peripheral side isolation?
- Research speed limitations of Remora/LinuxCNC to validate design specs
- Design high speed and analog inputs
- Fix the break in isolation for spindle DAC. Do we need a separate power in for this? How common is 0-5V? 
- Test to see if the all of the 3.3V powered components can be powered off internal 3.3V, and cut this regulator to save bom cost and space 
 parts. Use of a chassis SMPS that is not connected to the same ground, and is not mains earth referenced will create the isolation. 
- If we can cut 3.3V, consider switching to powering the device of E5V instead, then cut 12V regulator too. If so, change design to need 12V but only for Spindle DAC. 
- Validate mechanical fit of pin headers and mounting screw locations against physical hardware.
- Verify a sample of each remaining peripheral designs before committing to laying out PCB: Digital Input, Analog Input, Digital Output + PWM, Spindle DAC, regulators, console logging, programmable button, reset button, user LED with default blinky program loaded into PRU.  
- Create a test Remora configuration to determine maximum number of IO. Validate we have enough IO for the spec and start on wiring these IO.
- Test if USART LED design will work without changing jumpers on a factory Nucleo. If resoldering is required, the feature will be deleted as it is only a nice to have. 
- Test encoder usage, what is max speed? 
- After verification, estimate current draw. Redesign 12V, 5V and 3.3V switch mode supplies for peak efficiency and ripple rejection. Add in some thermal resets.
- PCB Layout of verified design along with new PSUs. Send for prototyping.
- Once physical hardware tested and verified, commit Gerber files
- Issue a BOM with Digikey part numbers.
- Put up some photos of the completed PCB as well as a layout guide. 
- Write a build guide. Don't forget J1 and J3 settings from Nucleo Manual needed to use onboard power supplies.
- See if we can also support laser cutting and lathe designs too 
- Research if we can support Servos

## If you'd like to contribute into this project
This section will eventually be filled with specific needs, for now - any feedback or offers to help with testing would be very welcome. 

## Firmware
WIP firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-W5500