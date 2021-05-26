![Alt text](/images/ML7280_clone.jpg?raw=true)

# ml7280_clone
Schematics and documentation for the ML7280 Sinewave Controller "clone" for BLDC motors

## Contents and history
This repository contains the result of my reverse engineering efforts on the ML7280 controller clone.
I call it the ML7280 clone, as that is the closest I can get to a "real" name.
This controller is available in many variants from AliExpress and other sources, at a cost of about $70.
There is no proper documentation, even the cables are marked in Chinese and connections are unclear.
It _seems_ to be a clone of the Sabvoton controller, and as it's a 72V version capable of 80A (at least) I therefore call it the ML7280 clone.

## Quick overview of the controller
The controller is relatively large, 220x110x50mm.
It's originally intended for scooters and rated for 3kW motors.
The version I have, can handle 72V and 80A.
The build quality of both enclosure and board is some of the best I've seen.
Very well laid out PCB, solid high capacity copper bars for high currents and a well cleaned up board. (The latter is more important than you might think. I've had TWO KT controllers break, because of lousy quality control, solder balls inside the enclosure and cable ends that were too long and touched the enclosure walls.)

The controller has 18 FETS, and is controlled by a STM32F030C8T6 microcontroller. This BEGS for custom firmware ;)
Original firmware seems to have no support for a LCD, and a lot of the I/O is not supported (although the HW is there).

The board has a main shunt, but does NOT have any phase shunts.
It does, however have a circuit for BEMF, so sensorless firmware can be made.


![Alt text](/images/track_details/semi-transparent_rev_eng.png?raw=true)
## How the reverse engineering was done
I took high-resolution pictures of both sides of the board.
I then processed these in Photoshop, raising contrast, colorized and made the semi-transparent.
I could then overlay the images and follow tracks on both the top and bottom layer.
Sounds easier than it is, as some tracks were hidden under components and had to be measured too.
Also, ground vias are hard to see.
I made VERY good use of the conductivity "beep" function on my multimeter, to verify the results.
I Googled components along the way and collected datasheets.
As I moved along, I redraw the whole schematic in EAGLE. I just used basic components and didn't care for a physical match of each, so there is no PCB file for this.
Almost all of the SMD caps does not have a value. It was simply too much work to unsolder every one of them to measure them. Most of the values are not critical anyway.
I used the original component numbering, so it was easier to relate the schematic to the actual board.
It took about 3 full days, but I think I got everything done. Phew!


## Simulation
To verify some parts of the schematic (and out of curiosity) I simulated some parts of the design in LTSpice.
The output stages and the power supply have been simulated so far and worked as it should.

## The future
The plan is now to write new firmware for this controller. (I haven't even been running it with whatever firmware is on it, as I don't know it's capabilities and documentation is severely lacking.)

If you are interested and would like to join in on this project, please let me know.
The repository for the firware is here: https://github.com/magicmicros/ml7280_clone_firmware



## The distant future
After playing around with this and making some (hopefully) working firmware, the plan is to make a smaller board using integrated FET drivers (LTC4444, MIC4100, UCC2720X or similar) and Bluetooth communication.


Stay tuned!
