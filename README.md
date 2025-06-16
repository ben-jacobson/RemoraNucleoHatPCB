# Remora Nucleo F446ZE Hat PCB.
Kicad 9 Project. 

Cost effective 6 Axis CNC motion controller card PCB design. Designed to be a hat for the ST Nucleo F446ZE which can be purchased from Digikey, Mouser or Element14 inexpensively. Uses a custom port of [Remora](https://github.com/scottalford75/Remora), making this a fully programmable real time motion control system, primarily designed for complex milling our router machines.

Note this repo is very much WIP, large chunks of this have yet to be designed. 

## Design specifications / features
- Nucleo F446ZE Hat for 6 axis CNC control using custom Remora firmware port. 
- Up to 6 axis of isolated step generators
- Programmable IO: *Specs TBC* - up to XX analog inputs, xx digital inputs, XX digital outputs, xx high current MOSFET driven outputs, XX PWM outputs
- *Specs TBC* - 0-10v DAC for isolated spindle control
- Console logging available via the STLink Virtual Comm port, simply connect a USB and you should be able to view

## Todos
- Validate mechanical fit of pin headers and screw locations against physical hardware
- Convert isolated stepper drivers to use heirarchical pins and variables, rather than an entire dedicated monolithic sheet.
- Validate the isolated stepper driver design, ensure can deliver up to 1Mhz
- Create a test configuration and determine maximum number of IO to complete spec
- Isolated spindle control DAC circuitry for 0-10V DAC and direction control.
- Digital outputs: Finish design for output driver using sink logic with at least 50mA sinking capabilities.
- Digital outputs : Allocate 8x IO for MosFet driver boards, enable up to 5-24v 500mA current sink for inductive loads (solenoids, )
- Inputs: make some decisions around how we can allow for analog inputs and isolated digital inputs. Ensure speed on digital inputs is sufficient enough for spindle encoder / MPG jogging. 
- Verify design before committing to PCB Layout build. 
- After verification, measure current draw
- Redesign 12V, 5V and 3.3V switch mode supplies for better efficiency and ripple rejection after calculating this current draw.
- Export gerbers for JLCPCB or PCBWay production
- Issue a BOM for Digikey ordering of parts
- Put up some photos of the completed design
- Write a build guide

## Firmware
WIP firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-W5500

