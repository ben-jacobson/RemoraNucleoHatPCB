# Remora Nucleo-144 Hat PCB.
Work in progress design for a cost-effective, highly customisable LinuxCNC motion control unit.

The form factor will be a hat/shield for ST Nucleo-144 evaluation boards using a WIZNet TOE for Ethernet control or alternatively can mount an entire Rasperry Pi onto the board with LinuxCNC loaded. The Nucleo can be loaded with a custom port of [Remora](https://github.com/scottalford75/Remora), link to specific recommended firmware below. This designed should work for CNC milling machines, routers and plasma cutters. Lathes and laser cutters are in plan for future support.

Schematics and board layout can be read with Kicad 9. Gerbers and PDF's of the schematics will become available on initial V1 release. At this stage the design is pre-release with a lot of validation pending. 

## Proposed Features
- **Low cost**: Board can be fabricated via JLCPCB/PCBWay, parts can be ordered from Digikey/Mouser. 
- **Approachable**: Goal is to be well documented, providing step by step build guides.
- **Moderate skill requirement**: SMT soldering skills are required but the pad sizes will be forgiving enough for hand soldering. Hot air soldering will be possible but not required. Skills and knowledge requirements will be listed up front. 

## Specifications
- Nucleo-144 Hat for 6 axis LinuxCNC motion control using custom port of Remora built for STM32.
- Up to 6 axes of isolated, step generation. Default max step gen rate in Remora is 40Khz but the driver circuitry has been tested up to 100Khz. Can be used with any 5V single ended or differential stepper driver card. Unused axes can be reconfigured as differential digital outputs.   
- IO: 16x digital inputs, 8x digital outputs. All 8 outputs can be configured as PWM, see the readme in the firmware below for configuration details. 
- Console logging is available via a UART header (TX only, RX is not implemented in firmware).

## Design spec goals to be completed
- IO: add 2x analog inputs
- Digital Outputs can be configured as high/low sink logic or PWM. Can sink up to 40mA.
- 1x extra input for high speed differential AB encoders. Max RPM TBC. 
- 1x non-isolated 0-10v DAC for spindle control. Additional indexing or direction control to be done with digital outputs.
- 12-24V DC power input for powering Nucleo and supplying 3.3V to sections of the board that are isolated. Galvanic isolation between Nucleo and external devices is achieved by supplying your own isolated 5V supply. Or you can set a jumper and have the board supply 5V to your external devices. 

## Todos
- Finish Spindle DAC design
- Design high speed and analog inputs
- Verify a sample of each remaining peripheral designs before committing to laying out PCB: Digital Input, Analog Input, Digital Output + PWM, Spindle DAC, regulators, console logging, programmable button, reset button, user LED with default blinky program loaded into PRU.  
- Test encoder usage, what is max speed? 
- After verification, estimate current draw. Redesign 12V, 5V and 3.3V switch mode supplies for peak efficiency and ripple rejection. Add in some thermal resets.
- Once physical hardware tested and verified, commit Gerber files
- Put up some photos of the completed PCB as well as a layout guide. 
- Write a build guide. Don't forget J1 and J3 settings from Nucleo Manual needed to use onboard power supplies.
- Research if we can support Servos

## If you'd like to contribute into this project
Reach out, would love some help especially with testing

## Firmware
Firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-PIO