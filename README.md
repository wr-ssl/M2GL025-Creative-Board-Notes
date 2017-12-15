# M2GL025-Creative-Board-Notes

![yellow board](/images/RISC-V_yellow_board.png)

<img src="https://github.com/rossberger/M2GL025-Creative-Board-Notes/blob/master/images/RISC-V_yellow_board.png" width="50">

This page has my notes from tinkering with the Microsemi M2GL025 creative board.

## About the board

It's a USD$99 evaluation board from Microsemi that implements a RISC-V CPU system in a 25kLE IGLOO2 FPGA.

 * IGLOO2 M2GL025-VF256 flash-based FPGA
 * 64MB DDR2 SDRAM (Alliance AS4C32M16D2A-25BCN)
 * 8MB SPI flash (Microchip 26F064B)
 * Integrated FT4232-based FlashPro5 USB JTAG adapter
 * Pin headers compatible with various popular hobbyist boards:
   * Arduino
   * mikroBUS (MikroElektronika)
   * PMod (digilent)

The board comes pre-flashed with a minimal RISC-V system and firmware.

## What tools do I need in order to program the board?

It depends what you mean by "program".  You can either program the FPGA or the CPU (if your FPGA design includes a soft CPU such as the RISC-V).

In order to program the FPGA, you need to use Microsemi's Libero tool to synthesize a design and generate the programming files needed to program the FPGA.  Once you've generated the programming files in Libero, you use the FlashPro application to flash the programming bitfile into the target FPGA.

## Do I need to purchase a separate USB FlashPro programmer to use with the creative board?

No.  The board has an integrated FT4232-based USB FlashPro5 interface that works with the FlashPro application.

## Where can I get board schematics?

## What example projects are available as a starting point?
