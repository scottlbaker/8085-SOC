
## Summary

This project is an SOC (System on a Chip) coded in VHDL and implemented for the Lattice iCE40-hx8k dev board. The SOC contains the following components: 8085 CPU + UART + Timer + I/O Ports

## Required Hardware

* Lattice iCE40-hx8k dev board (can be ordered online at www.latticesemi.com)
* USB-to-Serial 3.3V adapter (can be ordered from eBay)
* misc USB cables and wires for connecting the USB-to-Serial adapter

NOTE: Make sure the USB-to-serial adapter is a 3.3V version. Some adapters have 5V interface signals which could damage your iCE40-hx8k dev board.

## Tools

* IceCube2 (from Lattice Semiconductor) was used for synthesis and FPGA Routing.
* Icestorm (https:/github.com/cliffordwolf/icestorm) was used for programming.


## Build Flow

I used the Lattice IceCube2 software to generate the SOC_bitmap.bin programming file and then I used this command line "iceprog SOC_bitmap.bin" the program the iCE40-hx8k dev board over the USB cable (iceprog is part of the icestorm tool suite).

## Console Interface

I used the minicom program (on Ubuntu Linux) as a console to communicate with the 8085 SOC over the USB-to-Serial connection. Configure minicom using the command line "minicom -s" to configure the serial port for ttyUSB0 and turn of the hardware handshaking. There are probably other alternatives to minicom. Any ANSI terminal-emulator program should work for this application.

## Pinout

The iCE40 pins are defined as follows:
```
UART_RXD   G1 -pullup yes
UART_TXD   G2
PORTA[0]   B5
PORTA[1]   B4
PORTA[2]   A2
PORTA[3]   A1
PORTA[4]   C5
PORTA[5]   C4
PORTA[6]   B3
PORTA[7]   C3
RESET      N3 -pullup yes
CLK        J3 -pullup yes
```

## Memory Map

The memory map of this SOC is as follows:
```
0 -> 0fff  4k bytes of RAM
```

## I/O Map

The I/O map of this SOC is as follows:
```
00 -> 07   UART  registers
08 -> 0b   Timer registers
0c         Output register
0d         Interrupt mask register
0e -> 0f   Random number generator
10         Interrupt source register
```

## 8085 CPU Background Info

The 8085 was introduced in 1976 as the successor to the popular 8080 microprocessor. The 8085 added two instructions to enable/disable three added interrupt pins (and the serial I/O pins). It also simplified hardware by only using +5V power, and adding clock generator and bus controller circuits on-chip.

Like the 8080, the 8085 had a 16-bit address bus and an 8 bit data bus. Internally it had seven 8-bit registers (A, B, C, D, E, H, and L). The register pairs BC, DE and HL could be used as 16 bit registers. It  had a 16 bit stack pointer to memory and a 16 bit program counter. It also had 256 I/O ports, so that I/O devices could be hooked up without using any memory address space.

## Contributors

* Scott L Baker - SOC design

## License

See the **LICENSE** file in this repository
