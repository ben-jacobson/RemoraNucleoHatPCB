# Remora Nucleo-144 Hat PCB.
Work in progress design for a cost-effective, highly customisable LinuxCNC motion control unit.

Form factor is a hat/shield for ST Nucleo-144 evaluation board running [Remora](https://github.com/scottalford75/Remora). Either a WIZNet TOE can be used for Ethernet control or alternatively you can mount an entire Rasperry Pi 3/4/5 onto the board and run LinuxCNC on that. A link to a specific recommended version of Remora can be found below but other versions should work. This unit is capable of controlling a variety of machine types, predominantly CNC milling machines, routers, lathes, laser and plasma cutters. 

Schematics and board layout are editable with Kicad 9. Gerbers and PDF's of the schematics will become available on release. At this stage the design is pre-release with a lot of validation/testing/design work pending. 

## Proposed Features
- **Low cost**: Board can be fabricated via JLCPCB/PCBWay, parts can be ordered from Digikey/Mouser. a Digikey BOM is included for easy ordering. 
- **Approachable**: Goal is to be well documented, providing step by step build guides.
- **Moderate skill requirement**: SMT soldering skills are required but the pad sizes are forgiving enough for hand soldering. Hot air or reflow oven soldering is possible but not required. 

## Current specs
- Nucleo-144 Hat for 6 axis LinuxCNC motion control using custom port of Remora built for STM32. Board may also support GrblHAL but is not yet tested. 
- Up to 6 axes of isolated, step generation. Default max step gen rate in Remora is 40Khz but the driver circuitry has been tested to generate clean step pulses up to 100Khz. Can be used with any 5V single ended or differential stepper driver. Unused axes can be reconfigured as differential digital outputs. 
- IO: 16x NPN digital inputs, 8x NPN digital outputs. Outputs are sink logic, protected by a fuse and can sink up to 40mA of current. 
- Most outputs can be configured to drive PWM signals, see the readme in the firmware below for available pins and how to configure this.
- IO: 2x analog inputs (non isolated)
- High speed, single ended ABZ Rotary Encoder Input
- 1x 0-5v / 0-10v DAC for spindle control. Additional spindle control such as direction or indexing can be achieved with IO.
- 24V DC power input for powering Nucleo and supplying 3.3V to sections of the board that are isolated. Galvanic isolation between Nucleo and external devices is achieved by supplying your own isolated 24V supply to the separate input. A jumper can be found on board to configure powering the board with one supply only, breaking the isolation.  
- Console logging is available via a UART header (TX only, RX is not used by firmware).

## Future Specs
- PSU's seem to be fine handling 18-28V, need to test this before officially marking this as in spec.

## Set up Guide
A full build guide will be provided. In the mean time, please see the jumper settings and connecting to USB section as they are contain important information needed to get started.  

**Jumper settings:**
Before powering on your Nucleo hat, ensure that the following two jumpers are set: 
JP1: Please remove this jumper entirely
JP3: Place to the far right position, indicating VIN as per the picture in JP3Setting.png

**Connecting to USB:**
Take care when connecting the device to USB. Please make sure that the board is fully powered up before connecting to USB. Failing to do so could result in damage to your computer. This is not an issue with our design, but in the Nucleo itself. For more info see 7.4.2 in the Nucleo 144 datasheet. The device does not need USB to run. USB can be used to flash new firmware or monitor serial output. For serial output, the provided TX pin header is a better choice if you'd like constant serial monitoring during use.

## Todos
- Ensure a sample of each remaining peripheral design has been verified before committing to laying out PCB
- After verification, estimate current draw. Redesign 12V, 5V and 3.3V switch mode supplies for peak efficiency, line/load regulation and RR. Add in some PTC resettable fuses in line too. 
- Once physical hardware tested and verified, commit Gerber files to repo
- Put up some photos of the completed PCB.
- Write a build guide and include the details above from Jumper and USB settings. 
- Research how we might be able to support Servo drives
- Test GRBLHal

## If you'd like to contribute into this project
Reach out - would love some help with any improvement. Would be especially grateful for anyone willing to help with testing.

## Firmware
Firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-PIO