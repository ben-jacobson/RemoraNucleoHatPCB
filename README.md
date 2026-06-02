# Remora Nucleo-144 Hat PCB.
Work in progress design for a cost-effective, highly customisable LinuxCNC motion control unit.

Form factor is a hat/shield for ST Nucleo-144 evaluation board running [Remora](https://github.com/scottalford75/Remora). Requires a WIZNet TOE for Ethernet control. A link to a specific recommended version of Remora can be found below but other versions should work. This unit is capable of controlling a variety of machine types including CNC milling machines, routers, lathes, laser and plasma cutters. 

Schematics and board layout are editable with Kicad 9. Gerbers and PDF's of the schematics will become available on release. At this stage the design is pre-release with a lot of validation/testing/design work pending. 

## Proposed Features
- **Low cost**: Board can be fabricated via PCBWay, parts can be ordered from Digikey/Mouser/Element14. Digikey part numbers are written into the BOM for easy ordering. My latest build was sponsored by PCBWay but their estimated cost was just under the $100USD mark not including shipping 
- **Approachable**: Goal is to be well documented, providing step by step build guides.
- **Moderate skill requirement**: SMT soldering skills are required but the pad sizes are forgiving enough for hand soldering. Hot air or reflow oven soldering is possible but not required. 

## Current spec
- Nucleo-144 Hat for 6 axis LinuxCNC motion control using custom port of Remora built for STM32. Board may also support GrblHAL but is not yet tested. 
- Up to 6 axes of isolated, step generation. Default max step gen rate in Remora is 40Khz but the driver circuitry has been tested to generate clean step pulses up to 100Khz. Can be used with any 5V single ended or differential stepper driver. Unused axes can be reconfigured as differential digital outputs. 
- IO: 16x digital inputs, 8x NPN digital outputs. Outputs are sink logic/open collector, protected by a fuse and can sink up to 40mA of current. 
- Most outputs can be configured to drive PWM signals, see the readme in the firmware below for available pins and how to configure this.
- IO: 2x analog inputs (non isolated)
- 1x 0-5v / 0-10v DAC for spindle control. Additional spindle control such as direction or indexing can be achieved with IO.
- 24V DC power input for powering the Nucleo which in turn supplies 5V and 3.3V to sections of the board that are isolated. Galvanic isolation between Nucleo and external devices is achieved by supplying your own isolated 24V supply to the separate input. A jumper can be configured on board to powering the board with only one supply, but will break the isolation.  
- Console logging is available via a UART header (TX only, RX is not used by firmware).

## Future Specs
- PSU's seem to be fine handling 18-28V, need to test this before officially marking this as in spec. 
- There is an experimental single ended ABZ Rotary Encoder Input, it was hobbled together from parts already available on the BOM as an experiment. Predictably it does not perform any high speed task, it would probably even struggle with a slowly moved rotary encoder pot. Will eventually replace with a real design. 

## Build guide
This is intended to be a DIY project, not as a complete product.
A link will soon be provided to a place to order on PCBWay, or you can self source the parts using the DigiKey part numbers.
Please see the jumper settings and connecting to USB section as they are contain important information needed to get started.

**Jumper settings:**
Before powering on your Nucleo hat, ensure that the following two jumpers are set: 
JP1: Please remove this jumper entirely
JP3: Place to the far right position, indicating VIN as per the picture in JP3Setting.png

**Connecting to USB:**
Take care when connecting the device to USB. Please make sure that the board is fully powered up before connecting to USB. Failing to do so could result in damage to your computer. This is not an issue with our design, but in the Nucleo itself. For more info see 7.4.2 in the Nucleo 144 datasheet. The device does not need USB to run. USB can be used to flash new firmware or monitor serial output. For serial output, the provided TX pin header is a better choice if you'd like constant serial monitoring during use.

## Todos
- Perform full board testing with a real load and measure current draws, re-design the PSU's for beter efficiency, line/load regulation, ripple rejection, etc. 
- Add PTC resettable fuses to PSU
- Commit release Gerber files to repo and PDF
- Put up some photos of the completed PCB.
- Put up marketplace product on PCBWay
- Research how we might be able to support Servo drives
- Test GRBLHal

## If you'd like to contribute into this project
Reach out - would love some help with any improvement. Would be especially grateful for anyone willing to help with testing, further engineering support, etc.

## Firmware
Firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-PIO