# C64 Kernal Switcher

Originally started this design with the idea of using an Arduino as a way to switch between Commodore 64 kernal ROMs, but quickly ran out of space and turns out BWACK already did a better one - see further below for notes and information for that design. Note that this function is only used with Commodore 64 computers with "longboards".

I've adapted his designs into mine, changing a few of the features to my liking with the intent of reusing the original power LEDs as well as support for manual switches (find it easier that way). Original pinouts and RGB headers have been kept the same in order to not have to do a manual like he did, but note that I've rotated them for easier use with angled pin headers to save on space within the newer C64C-style cases.

With only the single RGB available, the updated code supplied with this project has been rewritten so that when you hold down the RESTORE it counts the flashes. The following sequence is performed after X flashes:

1. RESET
2. Next kernal
3. Kernal 0
4. Kernal 1
5. Kernal 2
6. Kernal 3

The board itself should be functionally identical to the one made by [bwack](https://github.com/bwack/C64-Switchless-Multi-Kernal-27C256-adapter), if you want the original behavior using the RGB header with an RGB LED - use the code provided with that project.

## Installation
First of all, check that you have a C64 with a "longboard", these are physically larger - the later common C64C boards had combined basic and kernal ROMs on a single chip, requiring a different solution altogether! First locate the kernal ROM, it should be marked 901227-03 and preferably already socketed.

If it is not socketed and you don't have experience desoldering ICs from older PCBs, I would suggest that you have someone with more experience perform this task for you - if you still go through with it, you live with the consequences! If you are really doing it anyway, cut off all the legs as close to the IC as possible and then remove leftovers with tweezers and solder-braid - IC will be dead, but the board itself will probably be happier!

Due to the space constraints, the following sequence of component installation is recommended:

1. Resistors
2. 8-pin socket (solder on reverse-side)
3. 12pin-header on the right side (solder on reverse-side)
4. 28-pin socket
5. 12-pin header on the left side (solder on reverse-side)
6. Capacitor
7. Remaining pin headers as needed

When installing in the computer, the pin on the bottom are inserted into the socket. You'll now need to find suitable places to attach the signal wires to the mainboard, you'll need to find a spot for the RESET and the RESTORE lines. RESET will have continuity to pin 40 on the 6510 processor, a spot for RESTORE can be found by tracing from pin 3 of the keyboard connector (pin 2 is missing). As with all things Commodore, Ray Carlsen will probably have a picture of those points for your specific revision so take a look [http://personalpages.tds.net/~rcarlsen/cbm/switchless%20JiffyDOS/](http://personalpages.tds.net/~rcarlsen/cbm/switchless%20JiffyDOS/).

## Kernals
There have been made several kernals for the Commodore 64, this solution allows you to add 3 other kernals in addition to the original one (you'll need it for compatibility). Among my favourites are the SD2IEC kernal, TurboTape ROM and JiffyDOS - most of these you'll find online, usually in the form of an 8kb bin-file. Note that JiffyDOS, while a popular choice, is still under license so you should therefore obtain a registered license for it!

On windows you can generate a 32kb file with your selected kernals by using the copy command, this can then be flashed to a blank 27C256 EPROM. Substitute kernals 2-4 with those of your choice:

`copy /b kernal.901227-03.bin+kernal2.bin+kernal3.bin+kernal4.bin 27C256_breadbin.bin`

# Original design
As a large part of this project, schematic and code, was based on the one originally made by bwack, I've included the following section from that projects README.txt here in accordance with the license specified.

> C64 Switchless Multi Kernel Switch
> \- 27C256 rom adapter for C64's with long motherboard

> Designed by BWACK.
> CERN OPEN HARDWARE LICENSE v1.2
> http://www.ohwr.org/

> The Eagle CAD files are available on GitHub:
> https://github.com/bwack/C64-Switchless-Multi-Kernal-27C256-adapter

> All text above must be included in any redistribution

# Schematic
The supplied KiCad files should be sufficient as both a schematic and as a  starting point for ordering PCBs (basically you could just zip the contents of the export folder and upload that on a fabrication site), the schematic is also available in [PDF-format](https://github.com/tebl/C64_Kernal_Switcher/raw/master/export/C64%20Kernal%20Switcher.pdf) and this is what you'll need to print and work your way through this things don't work as expected after assembly.

# BOM
Most parts should be easy to get a hold of from your favourite local electronic component shop, but given that I don't have access to such shops where I live so everything was based on whatever I could get cheapest from ebay/AliExpress (free shipping, plan on usually waiting 3-4 weeks though). The list below should be everything you'll need in addition to a workable soldering iron and some 60/40 soldering tin. Other tools needed for this project is an EPROM-ereaser as well as an EPROM-programmer for the two ICs (I use MiniPro TL866 for both).

Components in parenthesis are those used for extra features, you can omit these if you want to or have no need of those features (adding switches makes no sense if using MCU). RGB header can be left off, this is optional if you wish to use code from the original project! Sockets are always recommended though technically not needed.

| Reference    | Item                                  | Count |
| ------------ | ------------------------------------- | ----- |
| PCB          | Fabricate using Gerber files ([order](https://www.pcbway.com/project/shareproject/Sega_Master_System_II_Composite_Video_Board.html=88707))  |     1 |
| C1           | 100nF capacitor                       |     1 |
| R1           | 1k ohm resistor                       |   (1) | 
| R2           | 3k3 ohm resistor                      |   (1) |
| R3           | 560 ohm resistor                      |     1 |
| U1           | 12-pin straight round header          |     2 |
| U2           | PIC12F629 DIP-8                       |     1 |
| U2 (socket)  | 8-pin socket                          |   (1) |
| U3           | 27C256 EPROM DIP-28                   |     1 |
| U3 (socket)  | 28-pin wide socket                    |   (1) |
| A13,A14      | 3-pin straight header                 |   (2) |
| Signal, LED  | 3-pin angled header                   |     2 |
| RGB          | 2x3-pin straight header               |   (1) |