# LED Strip Controller
## Summary
Hardware + software project (from scratch)
Addressable LED strip controller with 1S Li-Ion battery charging, controlled by an 8-bit AVR microcontroller
Not yet finished, currently on hardware revision 3.0

## Motivation
I started rollerblading in July 2022 and saw somebody with LEDs attached to their skates. This project started as an excuse to learn how to program a microcontroller from scratch (i.e. no Arduino libraries). I ended up going through the entire product lifecycle -- schematic design, component selection, PCB manufacture and assembly, programming, and enclosure design.

## Hardware Revisions
The schematics went through some iterations, but didn't change significantly once it was first finished. Hardware revisions were mostly changes to layout, or component selection.

### Rev 1.0 (ATMEGA328PB)
![Rev 1.0 (first attempt)](./images/rev10.jpg)
First time working with SMD components, so I chose 0806. I also decided to try using a frying pan as a hotplate; if you look closely you can see where some of the flux has burnt slightly, but the electrical connections were still okay. U7 (3V3 to 5V level shifter) is missing because I ordered one with a different footprint by accident. It was also at this stage that I realised that putting the USB-C connector on the bottom meant that I had to hand-solder it.

![Rev 1.0 (second attempt)](./images/rev10_1.jpg)
I waited for the new level shifter to arrive, and this time I populated the through-hole parts too. You can see that the board is covered in flux residue, even after a huge amount of effort to clean it off. I couldn't successfully solder the USB-C connector, even with a hot air gun, and this board never powered on successfully.

### Rev 1.1 (ATMEGA328PB)
![Rev 1.1](./images/rev11.jpg)
The biggest change was that I moved all components to the top, and I increased the length of the important USB-C pads just incase I needed to do any touchups with an iron (thankfully I didn't). I was able to program the MCU, but there was a problem with the USB-to-serial bridge and the USB switching IC (the jumper wire going off-image was for bypassing the switch).

### Rev 2.0 (ATSAMD21)
![Rev 2.0](./images/rev20.jpg)
I wasn't satisfied with the cost of FTDI chips, and I wanted to simplify the board so I redesigned it to use an ATSAMD21. I had to change my mind while the PCBs were in transit because I found it impossible to get a J-Link EDU. I changed from 2-layers to 4-layers here, and having power + GND planes helped massively with routing.

### Rev 3.0 (ATMEGA32U4)
![Rev 3.0](./images/rev30.jpg)
I was having a good experience using the Pololu USB AVR Programmer (ISP), so I went for the ATMEGA32U4. I had also dialed in my soldering to the point that I felt comfortable switching to 0603 components. Unfortunately I accidentally coupled P-channel MOSFETs with the AP9101CK6 battery protection IC when I should have used N-channel.

### Rev 3.1 (ATMEGA32U4)
![Rev 3.1](./images/rev31.jpg)
I had hoped that implementing USB wouldn't be that difficult because of the ATMEGA32U4's USB capability, but I was mistaken. Once I realised that I would have to use up a significant amount of flash on a USB stack (e.g. LUFA) I decided to go back to having a dedicated USB-UART bridge (CP1202N). This had the added benefit of USB current detection. I also swapped out the JST connectors for Molex Pico-SPOX which are easier/cheaper to source. I also incorporated an 18650 holder.

## Schematics
Todo: cleanup + publish schematic

## Code
Todo: publish to GitHub
