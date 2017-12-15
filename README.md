# M2GL025-Creative-Board-Notes

My notes from tinkering with the Microsemi M2GL025 creative board.

[![Blue Board](/images/Microsemi_Board_IMG_9611_tn.jpg)](/images/Microsemi_Board_IMG_9611.jpg)
[![Yellow Board](/images/RISC-V_yellow_board_tn.png)](/images/RISC-V_yellow_board.png)

(Looks like it was originally done up in blue and got a new silkscreen job in 2017.  I don't see any changes to PCB routing or parts placement between the two).

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

Boards are available for purchase [here](http://www.futureelectronics.com/en/Technologies/Product.aspx?ProductID=FUTUREM2GLEVBFUTUREELECTRONICSDEVTOOLS7091559&IM=0)

## What tools do I need in order to program the board?

It depends what you mean by "program".  You can either program the FPGA or the CPU (assuming your FPGA design includes a soft CPU such as the RISC-V).

### FPGA

In order to program the FPGA, you need to use Microsemi's Libero tool to synthesize a design and generate the programming files needed to program the FPGA.  Once you've generated the programming files in Libero, you use the FlashPro application to flash the bitfile into the target FPGA.

### RISC-V CPU

In order to program the CPU you need a compiler/linker/assembler toolchain.  For RISC-V that toolchain is [GCC](https://github.com/riscv/riscv-gcc) (though folks are working on [LLVM](https://github.com/riscv/riscv-llvm)).

You can either use the tools directly or use a vendor-branded Eclipse-based IDE.

 * [RISC-V GCC](https://github.com/riscv/riscv-gcc) is the primary compiler/linker/assembler/debugger toolchain.
 * [RISC-V OpenOCD](https://github.com/riscv/riscv-openocd) is an OpenOCD fork that supports RISC-V JTAG debug interface.
 * [GNU MCU Eclipse](https://gnu-mcu-eclipse.github.io/) is a family of Eclipse extensions for ARM and RISC-V development

Other tools simply combine the above into an easy to deploy product:
 * [Microsemi SoftConsole](https://www.microsemi.com/products/fpga-soc/design-resources/design-software/softconsole#overview) Bundles Eclipse + GNU MCU extensions (OpenOCD and GCC) + some Microsemi-related examples.
 * [SiFive Freedom Fries Studio](https://www.sifive.com/products/tools/) is like SoftConsole but geared towards SiFive's product line.

## What's the licensing deal?

 * **RISC-V core**: Freely available.  Note that there appear to be two Microsemi DirectCore RISC-V cores (CoreRISCV_AXI4 and MiV_RV32) -- see below.  The license verbiage for the MiV_RV32 core sounds more permissive (["This core is being released under a modified Apache 2.0 license and is freely available through Libero"](http://www.actel.com/ipdocs/MiV_RV32IMA_L1_AHB_HB.pdf)).
 * **Libero**: The [Silver/Free license level](https://www.microsemi.com/products/fpga-soc/design-resources/licensing) can program devices up to 25k LEs, which matches the capacity of the M2GL025 IGLOO2 part.  So if you don't need a bigger FPGA you're all set with the free Silver license.
 * **SoftConsole**: Free.  It's just Eclipse + MCU Eclipse extensions + GCC + OpenOCD in a bundle with some Microsemi-related examples.

However, IANAL and I'm not sure about the specifics of licensing for commercial works.

## What's the difference between CoreRISCV_AXI4 and MiV_RV32 cores?

No idea.  Looks like MiV is the most recent version (does that mean CoreRISCV_AXI4 is depricated?) and comes in two flavors (with and without floating point).  If you have more information please let me know!

## Do I need to purchase a separate USB FlashPro programmer to use with the creative board?

No.  The board has an integrated FT4232-based USB FlashPro5 JTAG interface that works with the FlashPro application.

If you use the creative board design as a basis for your own design, you could leave off the FT4232 parts and just bring out the normal JTAG signals on a header for use with a [regular FlashPro4/5](https://www.microsemi.com/products/fpga-soc/design-resources/programming/flashpro#ordering).

## Where can I get board schematics?

 * [Future Electronics](http://www.futureelectronics.com/en/campaign/microsemi/Pages/CreativeDevelopmentBoard.aspx)
Fill out the "Request Demo Projects" link, submit your information, and you'll get an email with links to the board schematics and BOM in pdf format.

## What example projects are available as a starting point?

