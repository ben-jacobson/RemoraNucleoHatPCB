# Remora Nucleo F446ZE Hat PCB.
Kicad 9 Project. 

Cost effective 6 Axis CNC motion controller card PCB design. Designed to be a hat for the ST Nucleo F446ZE which can be purchased from Digikey, Mouser or Element14 inexpensively. Uses a custom port of [Remora](https://github.com/scottalford75/Remora), making this a fully programmable real time motion control system, primarily designed for complex milling our router machines.

Note this repo is very much WIP, large chunks of the design have yet to be designed. 

## Design specifications / features
- Nucleo F446ZE Hat for 6 axis CNC control
- Isolated Programmable IO for digital inputs, outputs and PWM
- Up to 6 axis of isolated step generators
- *Specs TBC* - Mosfet driven outputs
- *Specs TBC* - 0-10v DAC for isolated spindle control
- Uses custom port of Remora, see link to separate repo. 
- *Specs TBC* - up to XX Inputs, XX Outputs
- Console logging available via the STLink Virtual Comm port, simply connect a USB and you should be able to view

## Todos
- Validate mechanical fit of pin headers and screw locations
- Validate the isolated stepper driver design, up to 1Mhz
- Create a test configuration and determine maximum number of IO to complete spec
- Redesign 12V, 5V and 3.3V switch mode supplies for better efficiency and ripple rejection after calculating the overall current draw.
- Isolated spindle control DAC circuitry for 0-10V DAC and direction control.
- Digital IO: Design for isolated GPIO input and output drivers. May be sufficient to use same as steppers
- Digital IO: Allocate 8x IO for MosFet driver boards, enable up to 5-24v 500mA current sink for inductive loads (solenoids, )
- Digital IO: Allocate 4x inputs to be high speed isolated input, such as spindle encoder / MPG jog wheels
- Reset button that connects to underlying Nucleo reset button
- Programmable user button
- User LED

## Firmware
WIP firmware can be found in separate repo: https://github.com/ben-jacobson/Remora-STM32F4xx-W5500

