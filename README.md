# midi2cv v2 (modified from Elkayem's midi2cv design)

<img src="/images/03.jpg" alt="midi2cv" width="400"> <img src="/images/04.jpg" alt="midi2cv" width="400">

This is an modified version of Elkayem's midi2cv design. I have changed it from using banana jacks to 1/8" mono jacks and converted it to a pcb design better suited to eurorack format. A massive Thankyou to Elkayem for putting this code and project out there.

This repository contains the code and schematic for a DIY MIDI to CV converter.  I installed this converter into a home-built analog synthesizer, allowing me to play the synthesizer over MIDI.

The MIDI to CV converter includes the following outputs:

* Note CV output (88 keys, 1V/octave) using a 12-bit DAC
* Note priority (highest note, lowest note, or last note) selectable with jumper or 3-way switch
* Pitch bend CV output (0.5 +/-0.5V)
* Velocity CV output (0 to 4V)
* Control Change CV outout (0 to 4V)
* Trigger output (5V, 20 msec pulse for each new key played)
* Gate output (5V when any key depressed)
* Clock output (1 clock per quarter note, 20 msec 5V pulses)

## Parts
* Arduino Nano
* Optocoupler (I used a Vishay SFH618A, but there are plenty of alternatives out there)
* 2x MCP4822 12-bit DACs
* LM324N Quad Op Amp 
* Diode (e.g., 1N917)
* 2x 220, 500, 3x1K, 10K Ohm resistors
* 10K trim pot
* 3x 0.1 uF ceramic capacitors
* 5 pin MIDI jack
* 7x 1/4" (3.5mm) mono plug jacks
* 3-pin header or jumper (i used a JTS header)
* 3x 4-pin headers male and female
* 3-way switch SPDT
* 3mm LED
* 78L05

The Arduino code uses the standard MIDI and SPI libraries, which can be found in the Arduino Library Manager. 

The schematic is illustrated at the bottom of this page (Eagle file included).  Input power (VIN) is 9-12V.  This is required for the Note CV op amp, used for the 0-7.3V note output.  1% metal film resistors are recommended for the 10K resistors, for a constant op-amp gain that does not change with temperature. The 10k trim pot needs to be tuned to 7.7K between the center and inter leg.

The note priority options and jumper configuration are as follows:
* **Highest Note (+):** When multiple notes are sounded simultaneously, the highest note being held will be sounded.  When the highest note is released, the next highest note will be played, and so on.
* **Lowest Note (-):** Analagous to highest note, except the lowest note being held will be sounded. 
* **Last Note (L):** The most recent note played will be sounded.  When that note is released, the next most recent note still being held will be sounded.

<img src="/images/schematic.JPG" alt="schematic" width="800">
I used Elkayem's schematic to build my first iteration on proto board, as he had. I 3-d printed a face panel and it worked pretty well.

I had a few problems with bad wires and cruddy solder joints, as well as a bad arduino which led me to converting the design to a pcb with a few changes. I removed the 7.7k (3k and 4.7K combined) resistors and replaced them with a 10k trim pot allowing some fine tuning if required. I also added an LED to the input to indicate whether the module was recieving signal or not.

<img src="/images/01.jpg" alt="midi2cv" width="400"> <img src="/images/02.jpg" alt="midi2cv" width="400">

<img src="/images/05.jpg" alt="midi2cv" width="400"> <img src="/images/06.jpg" alt="midi2cv" width="400">

<img src="/images/08pcb.jpg" alt="pcb">

I have added to this repository the gerber files for the PCBs so anyone can print them if they want them. I will also attach 3d model I did for my first design if anyone whats to use that also, note that the PCB and 3d printed face don't fit together.

Updates I have done to this PCB: 
* Fixed some alignment issues with the first version. 
* Made the MIDI jack hole the right size.
* Fixed the wiring for the LED.
