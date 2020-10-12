# lm3481-boost-converter
# Overview
This project started when I needed a small footprint boost converter for a single cell lithium ion battery. I couldn't find anything that could deliver the current I needed in a small form factor, so I created this project with the help of Texas Instrument's [Webench tool][1]. This boost topology uses the [LM3841][2] boost controller to step up from 3-4.2v to 5v with a theoretical max current of 10A (WIP). The board is designed with a small footprint measuring 1.5" x 0.72"(38mm x 18.5mm) and an overall height under 0.75". **This is a work in progress and is not finished.**

# Specs and Adjusting Functionality
The controller is versitile and can be easily altered to meet your own requirement specs. I'd advise using Webench for design, and refer to my schematic for a sample layout or use it as a starting point. 
## Vin
The Vin pin requires a minimum of 2.97v to function and a maximum of 48v. If you want to add an under-voltage lockout, see UVLO.
## UVLO
The under-voltage lockout pin forces the controller off if a minimum voltage (set by the user) at Vin is not met. The lockout voltage is determined by a voltage divider created by Rivp1 and Rivp2. More detail regarding how these values are determined can be found in 7.3.5 (p17) of the datasheet.
## Vout
The output voltage is determined by the voltage created by a resistor divider at the feedback pin. Resistors Rfb1 and Rfb2 serve to create the divider, while Rfb3 is a 500ohm trimpot for fine tuning the output. Info about how to choose the values of these resistors can be found in 8.2.1.2.3 (p22) of the datasheet.
## Current Limiting
The voltage drop across the Rsense resistor determines the max current. The value of this resistor can be found in 8.2.1.2.3 (p22) of the datasheet.
## Cin & Cout
To save space, height, and ESR, I opted to use banks of ceramic capacitors. Since I couldn't find any existing stacked MLCC arrays, I manually soldered two rows stacked on each other. On Kicad, their footprints are single 1206s, but the schematic has some exposed power rails to accomodate for capacitor arrays. High capacitance MLCCs are not available in higher voltages, so it may not work for all designs.
## Current Limiting on the Drive Pin
Although the datasheet does not mention any resistor at the mosfet gate, I found one necessary since I was seeing ringing. Anything from 10-30ohm cut down on the ringing for me.

[1]: https://webench.ti.com/power-designer/
[2]: https://www.ti.com/product/LM3481
