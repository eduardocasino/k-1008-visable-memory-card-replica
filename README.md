# K-1008 Visable Memory card replica

## Introduction

Welcome to my K-1008 Visable Memory card replica repository. This is a work in progress, please check out from time to time.

Board is now complete and sent for fabrication.

## About

This aims to be a faithful replica of the K-1008 Visable Memory card, a memory expansion and display board for the KIM-1 designed by MTU in the late 70's

I'm using the original K-1008 documentation from various sources on the net, as well as hi-res photos form [Hans Otten's Retro Computing website](http://retro.hansotten.nl/6502-sbc/kim-1-manuals-and-software/kim-1-related-hardware/mtu-k-1012-k-1008/).


![components](https://github.com/eduardocasino/k-1008-visable-memory-card-replica/blob/main/images/k-1008-visable-memory-comp.png?raw=true)
![front](https://github.com/eduardocasino/k-1008-visable-memory-card-replica/blob/main/images/k-1008-visable-memory-front.png?raw=true)
![back](https://github.com/eduardocasino/k-1008-visable-memory-card-replica/blob/main/images/k-1008-visable-memory-back.png?raw=true)

~~WARNING: I have not yet sent the board to fabrication, so it is untested!~~

The card has been built and is being tested. All the memory is accessible and passes the memory tests by ["The Glitch Works"](https://github.com/glitchwrks/kim1_memtest) without any error. The picture however has some color artifacts and is not steady. I'm suspecting that it could be because I'm using a modern LCD monitor with a crappy video converter. More tests are needed but, anyway, it does not seem that there is any fundamental problem with the board.

![finished board](https://github.com/eduardocasino/k-1008-visable-memory-card-replica/blob/main/images/board_completed.jpg?raw=true)

## Building

There is nothing special about building the board. As with any other PCB, start soldering by component height. I'm providing an interactive BOM to assist with the process, but please take in mind:

* There are no modern substitutes for the MM5280 memory chips, but it is still possible to find them as they were widely used for arcade machines. Even the slower MM5280-5 variant should work as they are within the 300ns access/470ns cycle specs for the board (they are 270/470 vs 200/400 for the faster version)
* All the logic ICs are still manufactured, except for the 74LS13 and, I think, the 74LS55, but they are still in stock in some places.
* I've left the regulators unpopulated (bridged) and I use regulated 5V and 12V (an option which the manual suggests), but the LM340T5 is still in production and the LM342P12 can be replaced by the LM340T12.
* the 2N3646/2N9416 used in the level shifters are obsolete and expensive if you find them. I'm using a PN2369A/2N4403 pair, see the schematic for the changes in the base resistors and speed-up capacitors.
* You can ues a 1K trimmer instead of the 512R one. The one in the original board is [this one](https://www.bourns.com/docs/Product-Datasheets/3339.pdf), which is a bit expensive for a pot, but you can use any other with the same pin arrangement.
* And, finally, a low Vf Schottky, like the BAT86, is a perfect replacement for the Ge 1N270 diode to simulate an open-collector gate for the VECTOR_FETCH (K7) signal.

To connect the board to your KIM-1, build a connector as instructed in the [K-1008 User Manual], or you can use [my adapter board](https://github.com/eduardocasino/kim-1-mtu-expansion-card)

### First setup

Make sure that the microswitches are in a valid position. For example, turn on switches 1, 3 and 6 and leave the rest off to map the video memory at $2000. Refer to the [user manual](http://retro.hansotten.nl/uploads/files/K-1008%20Visible%20Memory%20Manual.pdf) for valid configurations.

Pins 19 (VECTOR_FETCH) and 20 (DECODE_ENABLE) pins of the board connector must be connected to pins J and K of the KIM-1 Application Connector, respectively. If using my expansion board, there are a copule of pin headers for this purpose.

Use a multimeter and adjust the potentiometer until the voltage at pin 13 of U8 is 1.4V. Now you should be able yo read/write from memory addresses from $2000 to $3FFF and a clean image with a random pattern should be shown on the monitor.

## Licensing

This is a personal project that I am sharing in case it is of interest to any retrocomputing enthusiast and all the information in this repository is provided "as is", without warranty of any kind. I am not liable for any damages that may occur, whether it be to individuals, objects, KIM-1 computers, kittens or any other pets. **It should also be noted that everything in this repository is a work in progress, has not been tested and may contain errors, therefore anyone who chooses to use it does so at their own risk**.

[![license](https://i.creativecommons.org/l/by-nc/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc/4.0/)

This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](http://creativecommons.org/licenses/by-nc/4.0/).

See the LICENSE.md file for details.

## Acknowledgements

* Hans Otten and his [Retro Computing blog](http://retro.hansotten.nl/). A lot of information and high resolution pictures of a K-1008
* Dave Plummer of [Dave's Garage fame](https://www.youtube.com/c/DavesGarage). Nice hi-res photos and actual board dimensions.
* Budi Prakosa "badgeek" for the [svg2shenzhen](https://github.com/badgeek/svg2shenzhen) plugin for Inkscape
* qu1ck for his [interactive HTML BOM plugin](https://github.com/openscopeproject/InteractiveHtmlBom)
