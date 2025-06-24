# Remora Nucleo F446ZE Hat PCB.
Work in progress design for a cost-effective, highly customisable six axis LinuxCNC compatible motion control unit that an average electronics hobbyist can build at home without specialised skills. 

The form factor will be a hat/shield for the ST Nucleo-144 evaluation board using a WIZNet TOE for Ethernet control. At this stage the firmware targets the F446ZE but may target other boards in future. The firmware was originally built and tested with a smaller Nucleo-64 F446RE and showed signs of life but found it lacked GPIO for high IO requirements. This unit uses a custom port of [Remora](https://github.com/scottalford75/Remora) with a link to the specific firmware below. This is primarily designed for CNC milling machine builds, but in theory should work for for routers and plasma cutters too. 

This is a Kicad 9 Project but will have Gerbers and PDF's of the schematics available on initial release. At this stage the design is pre-release with a lot of validation pending.  

## Project goals
I faced a number of challenges trying to source the right CNC motion controller system for a LinuxCNC 5-Axis CNC Milling machine build I was working on in 2025. There are plenty of options for CNC controllers but I never seemed to find a solution that ticked all of the boxes, or I had to make unusual trade offs to make it work. In my search I found:  
- Battle hardened, well-rated and reviewed systems that looked amazing, but seemed to be aimed at professionals. They had hefty price tags and would force you into their opinionated ecosystems.
- Medium cost devices that are also well rated but only support paid software - no LinuxCNC compatability
- Low cost units that could be made to work with LinuxCNC but lacked enough documentation, no real way to gain enough confidence to push the buy button
- Ever lower cost units that were worth a gamble, only to be reminded of the law of "you get what you pay for" when you find out the unit is full of manufacturing defects that aren't fixable - like shorted BGA solder joints under ICs. 
- Additional assorted issues associated with high cost of shipping, poor exchange rates and tarrifs. 

After what seemed like brick wall after brick wall I decided it'd be fun to try and see if I could offer an alternative for the hobbyist. The goal is to offer a flexible DIY CNC controller solution that solves for a number of the above problems.

## Features
- **Flexibile**: Lots of IO and flexibility on how it can be used. No hardware/firmware restrictions on number of joints up to 6 axes. Flexible enough for various machine types.  
- **Low cost**: You should be able to fabricate this board with JLCPCB/PCBWay, and order all parts from Digikey/Mouser for total of $100 USD or less. Cost will not include Nucleo board or tools needed to build such as soldering equipment. 
- **Medium form factor**: Ideally less than 140x140mm overall footprint to suit DIN rail mounting in electrical enclosures 
- **Approachabile**: Well documented and enough information to give you step by step guides on how to build, with adequate info on the skills and knowledge you will need to fill before building
- **Moderate skill requirement**: SMT soldering skills are required but the pads should be forgiving enough for hand soldering. Hot air soldering should be possible but not required.
- **Quality**: Provided soldering has been done properly, the build quality should be equal to or better than the cheap mass produced low cost units sold on Ali Express, e.g NVEM/EC300/EC500 boards.

## Design spec goals - To be revised as design progresses.
- Nucleo F446ZE Hat/Shield for 6 axis LinuxCNC motion control using custom port of Remora built for STM32.
- Unopinionated design, enables the user to configure the IO the way they want. 
- Up to 6 axes of isolated, real time hardware step generation. Max step gen TBC (Aiming for >200Khz). Can be used with any 5V single ended or differential stepper drivers. Unused axes can be reconfigured as differential digital outputs.   
- IO: 4x analog inputs, 28x digital inputs, 10x digital outputs. 
- Digital Outputs can be configured as high/low sink logic or PWM. Can sink up to 40mA.
- 2x high speed encoder inputs for ABZ encoders. Max RPM TBC (Aiming for up to 10K RPM). 
- 1x Isolated 0-10v DAC for spindle control. Additional indexing or direction control to be done with digital outputs.
- Console logging available via the STLink Virtual Comm port to view and debug Remora's console logging.
- 24V DC power input, configurable isolation via jumpers of 5V and GND lines used for stepper drivers and IO.
- 1x User programmable button

## Todos
- Validate mechanical fit of pin headers and mounting screw locations against physical hardware.
- Validate isolated stepper driver design, min 200Khz, ideally up to 1Mhz. What is LinuxCNC / Remora maximum? Ensure we can exceed it and update specs once cap is set.
- Design inputs: low/high speed digital, analog ins
- Verify a sample of each remaining peripheral designs before committing to laying out PCB: Digital Input, Analog Input, Digital Output + PWM, Spindle DAC, regulators, console logging, programmable button, reset button, user LED with default blinky program loaded into PRU.  
- Create a test Remora configuration to determine maximum number of IO. Validate we have enough IO for the spec and start on wiring these IO.
- Test if USART LED design will work without changing jumpers on a factory Nucleo. If resoldering is required, the feature will be deleted as it is only a nice to have. 
- Test encoder usage, what is max speed? 
- After verification, estimate current draw. Redesign 12V, 5V and 3.3V switch mode supplies for peak efficiency and ripple rejection. Add in some thermal resets.
- PCB Layout of verified design along with new PSUs. Send for prototyping.
- Once physical hardware tested and verified, commit gerbers
- Issue a BOM with Digikey part numbers.
- Put up some photos of the completed PCB as well as a layout guide. 
- Write a build guide. Don't forget J1 and J3 settings from Nucleo Manual needed to use onboard power supplies.
- See if we can also support laser cutting and lathe designs too 
- Research if we can support Servos

## If you'd like to contribute into this project
This section will eventually be filled with specific needs, for now - any feedback or offers to help with testing would be very welcome. 

## Firmware
WIP firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-W5500