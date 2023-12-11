# ZX128 Interface 1 Development Board

This is an Altera based Interface 1 development board for the RC2014 [(link)](https://rc2014.co.uk). The primary purpose is to provide a prototyping environment to develop a ZX Interface 1 replacement.  It is intended for use either with the ZX128 Spectrum board [(link)](https://github.com/ZXQuirkafleeg/ZX128) or with a real Spectrum using the RC2014 adapter board [(link)](https://github.com/ZXQuirkafleeg/ZX-RC2014-Adapter).

Notable features are:

* Altera EPM71XXSLC CPLD development environment
* Onboard 32K ROM (in 8K pagaes) for test ROMs
* Onboard oscillator and Interface 1 style address decoding
* Oqtadrive and microdrive edge connector
* Prototyping area

![top view of ZX Interface 1 development board](https://github.com/ZXQuirkafleeg/ZX-Interface-1-Development-Board/blob/main/Images/IMG_20231211_170955.jpg)

![ZX Interface 1 development board connected to ZX Spectrum via RC2014 Adapter](https://github.com/ZXQuirkafleeg/ZX-Interface-1-Development-Board/blob/main/Images/IMG_20231211_170443.jpg)

## ROM

The board takes a 28C256 ROM which is split into 8K pages.  A13 and A14 are driven by either the CPLD or the ROM jumpers. 0-8K is the interface 1 ROM.

## Prototyping area

The top half of the board provides a protyping area.  Left and right edge most vertical columns are 0V and 5V respectively.  

## RC2014 Bus

There are some differences between the RC2014 bus and the Spectrum edge connector signals.  Notably the CPU clock is inverted on the edge connector.  Spectrum peripherals also use ROMCS, NMI and WAIT (e.g. DIVMMC, Multiface and Inferface 1), so these are brought out to the user pins on the RC2014 bus:

*	Pin 37 – User 1 – ROMCS (required)
*	Pin 38 – User 2 – NMI 
*	Pin 39 – User 3 – WAIT (required)
*	Pin 40 – User 4 – (unallocated)

## VHDL Code

The Quartus 13.1 project can be found [here](https://github.com/ZXQuirkafleeg/ZX-Interface-1-Development-Board/tree/main/CPLD).  The code is under development. 

Current status is:

Mode          | Storage Device | Status
:---:         | :---:          | :---: 					
Read          | Octadrive      | Working
Read          | Microdrive     | Not working - needs a functional microdrive to debug
Write         | Octadrive      | Not working - under development
Write         | Microdrive     | Not working - under development

## Build
All components are though-hole and standard density.  A schematic can be found [here](https://github.com/ZXQuirkafleeg/ZX-Interface-1-Development-Board/blob/main/PCB/RC2014%20Interface%201%20Dev%20Schematic.pdf).

### PCB 

For the PCB, EasyEDA (V6.5.22) design files can be found [here](https://github.com/ZXQuirkafleeg/ZX-Interface-1-Development-Board/tree/main/PCB) and gerbers [here](https://github.com/ZXQuirkafleeg/ZX-Development-Board/blob/main/PCB/Gerber_PCB%20-%20RC2014-%20Dev%20V1.1%20-%20freeroute.zip).  The PCB is a standard two layer board approx. 100mm by 100mm.  Decoupling capacitors for the CPLD are mounted under the socket.

## PCB ERROR

Due to a netlist error, pin 14 (5V) of HC04 oscillator is unconnected and will need to be linked to a nearby 5V supply.  This will be fixed in V1.1 of the PCB.

### CPLD Programming

Programming the CPLD can be done by the Programmer app in Quartus 13.1.  Connect a USB Blaster dongle (or clone) to J4 and connect the 5V supply to the ZX develoment board.  

### ROM Programming

Programming the ROM can be done by using a TL866II or similar.  There is no provision for programming the ROM in-situ.

## Jumpers and Connectors

* J1 – RC2014 Bus connector
* J2 – ROMCS, NMI and WAIT jumpers – used connect CPLD to RC2014 bus
* J3 – Altera USB Blaster ICSP connector
* J4 - Interface 1 signals (Microdrive side)
* J5 - Jumpers to link Interface 1 to Microdrive
* J6 - Interface 1 signals (Interface 1 side)
* J7 - Configures order of Microdrive and Octadrive in the chain (COMMSDATA routing)
* J8 - Network jumpers (untested)
* J9 - Internal (8MHz) or external clock
* J10 - Polarity of 9V supply via CN3
* J11 - If U5 (5V regulator) is fitted, power board and RC2014 bus CN3 supply

* CN1 - Spectrum Microdrive connector 

## Octodrive

U6 is a standard arduino nano programmed with Oqtadrive [here](https://oqtadrive.org/).

## Connecting to a real Spectrum

The board can be connected to a real spectrum using a simple adapter [here](https://github.com/ZXQuirkafleeg/ZX-RC2014-Adapter).
