# Remora Nucleo-144 Hat PCB.
Work in progress design for a cost-effective, highly customisable LinuxCNC motion control unit.

The form factor is a hat/shield for ST Nucleo-144 evaluation board running [Remora](https://github.com/scottalford75/Remora). Either a WIZNet TOE can be used for Ethernet control or alternatively you can mount an entire Rasperry Pi onto the board and run LinuxCNC from that. Link to specific recommended version of Remora below. This unit is compatible with a variety of machine types, predominantly CNC milling machines, routers and plasma cutters. Lathes and laser cutters are in plan for future support too. 

Schematics and board layout are editable with Kicad 9. Gerbers and PDF's of the schematics will become available on initial V1 release. At this stage the design is pre-release with a lot of validation pending. 

## Proposed Features
- **Low cost**: Board can be fabricated via JLCPCB/PCBWay, parts can be ordered from Digikey/Mouser. a Digikey BOM is included 
- **Approachable**: Goal is to be well documented, providing step by step build guides.
- **Moderate skill requirement**: SMT soldering skills are required but the pad sizes are forgiving enough for hand soldering. Hot air or reflow oven soldering will be possible but not required. 

## Current specs
- Nucleo-144 Hat for 6 axis LinuxCNC motion control using custom port of Remora built for STM32.
- Up to 6 axes of isolated, step generation. Default max step gen rate in Remora is 40Khz but the driver circuitry has been tested to generate clean step pulses up to 100Khz. Can be used with any 5V single ended or differential stepper driver unit. Unused axes can be reconfigured as differential digital outputs.   
- IO: 16x digital inputs, 8x digital outputs. All 8x outputs can be configured as PWM, see the readme in the firmware below for how to configure this. 
- Console logging is available via a UART header (TX only, RX is not implemented in firmware).
- Digital Outputs utilise sink logic, are fuse protected and can sink up to 40mA of current.

## Future Specs
- IO: add 2x analog inputs (non isolated)
- 1x extra input for high speed differential AB encoders. Max RPM TBC. 
- 1x non-isolated 0-10v DAC for spindle control. Additional indexing or direction control to be done with digital outputs.
- 12-24V DC power input for powering Nucleo and supplying 3.3V to sections of the board that are isolated. Galvanic isolation between Nucleo and external devices is achieved by supplying your own isolated 5V supply. Or you can set a jumper and have the board supply 5V to your external devices. 

## Todos
- Finish spindle design
- Work on high speed differential AB encoder, calculate the max speed given 40Khz thread
- Work on analog inputs
- Ensure a sample of each remaining peripheral design has been verified before committing to laying out PCB
- After verification, estimate current draw. Redesign 12V, 5V and 3.3V switch mode supplies for peak efficiency and ripple rejection. Add in some PTC resettable fuses.
- Once physical hardware tested and verified, commit Gerber files to repo
- Put up some photos of the completed PCB as well as a layout guide. 
- Write a build guide. Don't forget J1 and J3 settings from Nucleo Manual needed to use onboard power supplies.
- Research how we might be able to support Servo drives

## If you'd like to contribute into this project
Reach out - would love some help with any improvement. Would be especially grateful for anyone willing to help with testing

## Firmware
Firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-PIO