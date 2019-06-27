# C64 Kernal Switcher

Originally started this design with the idea of using an Arduino as a way to switch between Commodore 64 kernal ROMs, but ended up adapting BWACKs design into it instead and like him opted for the PIC12F629 instead. This particular version of a quad kernal switcher for the Commodore 64 is only compatible with Commodore 64 "longboards" (usually breadbins, but you never really know what you get with Commodore so check first).

BWACKs design has been adapted into mine, changing along the way a few of the features to my liking - in particular, reusing the original power LEDs as well as support for manual switches (find it more adaptable that way). Original pinouts and RGB headers have been kept the same in order to not have to do a manual like he did, but note that I've rotated them for easier use with angled pin headers to save on space within the newer and tighter C64C-style cases. Reusing the original LED makes it easier because RGB LEDs in a size that fits a C64C case is harder to find, not to mention fiddly to wire up for beginners with access to a soldering iron.

With only the single LED available, the code supplied with this project has been rewritten so that when you hold down the RESTORE it counts the flashes - then when you let go it performs the actions according to the following list:

1. RESET
2. Next kernal
3. Kernal 0
4. Kernal 1
5. Kernal 2
6. Kernal 3

![Single LED](https://github.com/tebl/C64-Kernal-Switcher/raw/master/gallery/Build%20%236.jpg)

The board itself should be functionally identical to the one made by [bwack](https://github.com/bwack/C64-Switchless-Multi-Kernal-27C256-adapter), if you want the original behavior using the RGB header with an RGB LED - use the code provided with that project.

## Building the switcher
Soldering together the few components should be easy going as long as you have access to reasonable tools, personally I'm using a cheap soldering station with adjustable temperature so no need to go expensive if you don't have to. Use 60/40 soldering tin, the lead free makes to job a lot harder if you're new to the hobby.

Start by studying the PCB, both sides and perform dry fits to see that you have an idea of where everything goes since removing things is always a lot harder than getting it right in the first place (match orientation to symbols, see gallery images for reference).

With a lot going on for such a tiny board, you'd need to pay some attention to the sequence of components getting soldered in. The list below is the one I recommend, note that with some sockets you'll have less space underneath and it'll be a lot easier getting it into place if you trim the pins after they have been soldered into place. When aligning the two 12-pin (round) pin-headers I recommend using a round-pin socket to help keep them straight, that way you won't get issues trying to install it into the Commodore 64.

1. Resistors
2. 8-pin socket (solder on reverse-side)
3. 12pin-header on the right side (solder on reverse-side)
4. 28-pin socket
5. 12-pin header on the left side (solder on reverse-side)
6. Capacitor
7. Remaining pin headers as needed

![Topside](https://github.com/tebl/C64-Kernal-Switcher/raw/master/gallery/Build%20%233.jpg)
![Underside](https://github.com/tebl/C64-Kernal-Switcher/raw/master/gallery/Build%20%234.jpg)

## Installation
First of all, check that you have a C64 with a "longboard", these are physically larger - the later common C64C boards had combined basic and kernal ROMs on a single chip, requiring a different solution altogether! First locate the kernal ROM, it should be marked 901227-03 and preferably already socketed.

If it is not socketed and you don't have experience desoldering ICs from older PCBs, I would suggest that you have someone with more experience perform this task for you - if you still go through with it, you live with the consequences! If you are really doing it anyway, cut off all the legs as close to the IC as possible and then remove leftovers with tweezers and solder-braid - IC will be dead, but the board itself will probably be happier!

When installing in the computer, the pin on the bottom are inserted into the socket. You'll now need to find suitable places to attach the signal wires to the mainboard, you'll need to find a spot for the RESET and the RESTORE lines. RESET will have continuity to pin 40 on the 6510 processor, a spot for RESTORE can be found by tracing from pin 3 of the keyboard connector (pin 2 is missing). As with all things Commodore, Ray Carlsen will probably have a picture of those points for your specific revision so take a look [http://personalpages.tds.net/~rcarlsen/cbm/switchless%20JiffyDOS/](http://personalpages.tds.net/~rcarlsen/cbm/switchless%20JiffyDOS/).

![Installed](https://github.com/tebl/C64-Kernal-Switcher/raw/master/gallery/Build%20%235.jpg)

## Kernals
There have been made several kernals for the Commodore 64, this solution allows you to add 3 other kernals in addition to the original one (you'll need it for compatibility). Among my favourites are the [SD2IEC Kernal ROM](https://csdb.dk/release/?id=159050), [Turbo Tape Kernal ROM](https://csdb.dk/release/?id=47403) and [JiffyDOS](http://www.go4retro.com/products/jiffydos/). Note that JiffyDOS, while a popular choice is still under license so you should therefore seek to obtain a registered license for it!

On windows you can generate a 32kb file with your selected kernals by using the copy command, this can then be flashed to a blank 27C256 EPROM. Substitute kernals 2-4 with those of your choice:

`copy /b kernal.901227-03.bin+kernal2.bin+kernal3.bin+kernal4.bin 27C256_breadbin.bin`

![Custom ROM](https://github.com/tebl/C64-Kernal-Switcher/raw/master/gallery/Build%20%237.jpg)

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

Pin headers you order in bulk and snap off parts as needed, but note that you should get round pin headers for the part that goes into the socket - while you can use the regular kind, you may easily wear out or break the socket.

Components in parenthesis are those used for extra features, you can omit these if you want to or have no need of those features (adding switches makes no sense if using MCU). RGB header can be left off, this is optional if you wish to use code from the original project! Sockets are always recommended though technically not needed.

| Reference    | Item                                  | Count |
| ------------ | ------------------------------------- | ----- |
| PCB          | Fabricate using Gerber files ([order](https://www.pcbway.com/project/shareproject/Commodore_64_Quad_Kernal_Switcher.html?inviteid=88707))          |     1 |
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