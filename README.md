# Remora Nucleo F446ZE Hat PCB.
Work in progress design for a cost-effective, highly customisable LinuxCNC motion control unit.

The form factor will be a hat/shield for ST Nucleo-144 evaluation boards using a WIZNet TOE for Ethernet control. At this stage the firmware targets the F446ZE but may target other boards in future. The firmware was originally built for the smaller Nucleo-64 F446RE but lacked the GPIO for high IO requirements. The unit uses a custom port of [Remora](https://github.com/scottalford75/Remora), link to specific firmware below. This designed should work for CNC milling machines, routers and plasma cutters. Lathes and laser cutters are in plan for future support.  

Schematics and board layout can be read with Kicad 9 Project. Gerbers and PDF's of the schematics will become available on initial release. At this stage the design is pre-release with a lot of validation pending.  

## Proposed Features
- **Flexibile**: Lots of flexible IO. Minimal hardware/firmware restrictions on number of joints up to 6 axes. Could theoretically create more axes pending testing.
- **Low cost**: Board can be fabricated via JLCPCB/PCBWay, parts can be ordered from Digikey/Mouser. 
- **Approachable**: Goal is to be well documented, providing step by step build guides.
- **Moderate skill requirement**: SMT soldering skills are required but the pad sizes will be forgiving enough for hand soldering. Hot air soldering will be possible but not required. Skills and knowledge requirements will be listed up front. 

## Design spec goals - To be revised as design progresses.
- Nucleo F446ZE Hat/Shield for 6 axis LinuxCNC motion control using custom port of Remora built for STM32.
- Up to 6 axes of isolated, real time hardware step generation. Max step gen TBC (Aiming for >200Khz). Can be used with any 5V single ended or differential stepper drivers. Unused axes can be reconfigured as differential digital outputs.   
- IO: 4x analog inputs, 28x digital inputs, 10x digital outputs. 
- Digital Outputs can be configured as high/low sink logic or PWM. Can sink up to 40mA.
- 2x high speed encoder inputs for ABZ encoders. Max RPM TBC (Aiming for up to 10K RPM). 
- 1x non-isolated 0-10v DAC for spindle control. Additional indexing or direction control to be done with digital outputs.
- Console logging available via the STLink Virtual Comm port to view and debug Remora's console logging.
- 12-24V DC power input for powering Nucleo and supplying 3.3V to sections of the board that are isolated. Galvanic isolation between Nucleo and external devices is achieved by supplying your own isolated 5V supply. Or you can set a jumper and have the board supply 5V to your external devices. 
- 1x User programmable button

## Todos
- Finish Spindle DAC design
- Test if we still need 5V for WIZNET? What does this do for logic and peripheral side isolation?
- Research speed limitations of Remora/LinuxCNC to validate desired specs
- Design high speed and analog inputs
- Fix the break in isolation for spindle DAC. Do we need a separate power in for this? How common is 0-5V? 
- Test to see if the all of the 3.3V powered components can be powered off internal 3.3V, and cut this regulator to save bom cost and space 
 parts. Use of a chassis SMPS that is not connected to the same ground, and is not mains earth referenced will create the isolation. 
- If we can cut 3.3V, consider switching to powering the device of E5V instead, then cut 12V regulator too. If so, change design to need 12V but only for Spindle DAC. 
- Validate mechanical fit of pin headers and mounting screw locations against physical hardware.
- Validate isolated stepper driver design, aim for >=200Khz, as high as 1Mhz. What is LinuxCNC / Remora maximum? Ensure we can exceed it and update specs once cap is set.
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