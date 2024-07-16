# Tandy 1000 EX/HX 3-in-1 Upgrade
The Tandy 1000 EX/HX 3-in-1 Upgrade expands your 1000 EX or HX with some fantastic features!
![The 3-in-1 Upgrade](Pictures/3-in-1%20Upgrade%20Top.jpg "The Upgrade PCB")

## About
The Tandy 1000 EX and HX systems originally came with just 256Kb of system memory, no serial ports, no hard drive, and a non-standard expansion slot.  These limitations have made the EX and HX somewhat unattractive for the modern vintage computer enthusiast.  While there were contemporary ways to expand the system’s capabilities, such upgrades were somewhat uncommon and are difficult to obtain today.  The Tandy 1000 EX/HX 3-in-1 Upgrade overcomes these limitations by providing the following features:
* Fully expanded system memory - 640Kb conventional + 96Kb UMB 
* Standard DB9 RS232 Serial Port
* XT-IDE ‘CF Lite’ Interface

## Acknowledgements
This project is based on the work of [Rob Krenicki's Tandy-EX-HX-3in1 project](https://github.com/rkrenicki/Tandy-EX-HX-3in1).  It was forked in 2023. The original idea and execution was Rob's, but a few small changes have been made:
* Modification of the mounting plate to accomodate the rivnut style connections, greatly improving board mount stability.
* The User's Guide was added

## Memory
The 3-in-1 Upgrade uses an Alliance AS6C4008 4Mbit static random access memory (SRAM) chip to provide an additional 512Kbytes of system memory.  In combination with the original 256Kb of system memory, your computer will now have 768Kb of memory configured as 640Kb of conventional memory, plus an additional 96Kb of UMB (Upper Memory Block) memory.

## Serial Port
The 3-in-1 Upgrade uses a Texas Instruments TL16C550 UART to provide a standard 16550-based, DE9 serial RS-232 port.  This port is configured as ‘COM1’ and is capable of communications of up to 115kbit/s.  The serial port is perfect for a serial mouse or communications with other systems.

## XT-IDE
The 3-in-1 Upgrade implements a “XT-CF-lite rev.2” style XT-IDE adapter, which provides the standard XT-IDE Universal BIOS and a CompactFlash socket that is accessible from the rear of the computer.

## Compatibility
The 3-in-1 Upgrade is only compatible with the Tandy 1000 EX or Tandy 1000 HX.  The upgrade is not compatible with any other PLUS slot expansion adapters and must be the only adapter installed - all other adapters must be removed.  Physically, the upgrade will take ‘Slot 2’ on the rear of your computer.  Slots 1 and 3 will be unavailable for use.

## Compact Flash Card Support
The upgrade’s CompactFlash interface is generally compatible with all CompactFlash cards, however there are a wide variety of cards available, so not all cards may work the same, or at all.  Generally it is recommended to use a CompactFlash card smaller than 256MB.  It is generally not recommended to use MicroSD-to-CF card adapters, nor MicroDrive style cards.  For more details on compatible cards, consult the XT-IDE project documentation.

## CPU Compatibility
The 3-in-1 Upgrade is compatible with both the Tandy 1000’s original Intel 8088 CPU, as well as the NEC V20 CPU.  An optional enhanced BIOS is available specifically for the NEC V20 CPU, which can improve disk performance.

## Configuration
The 3-in-1 Upgrade board requires no additional configuration for normal operation, and is ‘plug and play’.  There is one jumper, ‘J1’, which controls whether the XT-IDE EEPROM is in ‘Write Enable’ mode.  The default is for the jumper to be open (removed) to disable writes.  Unless you plan to write to the EEPROM, such as for on-system XT-IDE updates, it is strongly recommended that this jumper be left open.

## Operation
Operation of the 3-in-1 Upgrade board in your Tandy 1000 is almost entirely automatic.  No specific configuration of the board is necessary for normal functionality, however a few quality-of-life changes can be made to improve  operation of your computer with the 3-in-1 Upgrade.

### Memory
The 3-in-1 Upgrade will automatically increase the computer's conventional memory to 640Kb.  On power up, the computer will display “Memory Size = 640k” on the screen, indicating that the upgrade is properly connected and functional.  No other action is required to use this additional memory.

Note! If the computer does not display 640k of system memory at system power on, or there appears to be other problems with the upgrade, power off the computer and confirm that the upgrade board is properly seated.

An additional 96Kb of UMB (Upper Memory Block) memory is provided by the 3-in-1 Upgrade, but most versions of DOS are unable to take advantage of this memory directly.  The included disk images have example configurations for using the ‘DOSMAX’ utility to move MS-DOS into this UMB, freeing up additional conventional system memory.  Typical MS-DOS 5 configurations using DOSMAX can yeild 624Kb of conventional memory available for user programs.  Should you wish to use this utility, examine the example configurations and implement as necessary for your situation.

### DMA
Historically, memory upgrades for the Tandy 1000 EX / HX (such as Tandy’s ‘Memory PLUS Expansion Adapter’ P/N 25-1062) provided an additional Direct Memory Access (DMA) controller to handle (among other things) the refresh timing for the adapter’s added DRAM memory.  As the 3-in-1 Upgrade uses SRAM, which does not have such refresh requirements, the DMA functionality is not needed.  The presence or lack of DMA does not impact performance of most aspects of using the system.

### XT-IDE
The 3-in-1 Upgrade provides a “XT-CF-lite rev.2” style XT-IDE adapter, providing the standard XT-IDE Universal BIOS and a CompactFlash socket that is accessible from the rear of your computer.  The XT-IDE ROM is mapped to the 0xC000 address, and the CF socket to the 0x300 address.  Version ‘R602’ of the XT-IDE software is programmed into the EEPROM.  Operation of the XT-IDE software and interface is the same as any standard XT-IDE implementation, so it is recommended to reference the official XT-IDE documentation for specific operational instructions.

When installed in a Tandy 1000 EX, the XT-IDE software will start automatically.  When installed in a Tandy 1000 HX, the XT-IDE software will not necessarily start automatically, but instead follow the existing configured boot order.  By default, the HX will boot the built-in system ROM containing Tandy MS-DOS v2.11, and then either load the command prompt, load a menu, or load Personal DeskMate.  The Tandy ‘SETUPHX.COM’ program can change this behavior, and a copy is included on the provided CompactFlash card for your convenience.  If your system boots to the menu, press the F4 key for ‘Startup from Internal Drive’ and the XT-IDE software will load.  If you want the XT-IDE software to load every time, run the setup program and change the ‘PRIMARY START-UP DEVICE’ setting to ‘DISK’.

The 3-in-1 Upgrade board has a single jumper ‘JP1’ which enables writes to the EEPROM for future XT-IDE software upgrades.  The jumper should be left removed for normal operation.

### Serial Port
The 3-in-1 Upgrade places a serial port on the typical I/O address 0x3F8 and IRQ 4, which the computer will automatically detect.  MS-DOS, in turn, will see this serial port and assign it the label COM1.  System information programs like Norton System Info will indicate if the system has detected the serial port.
The serial port address and IRQ configuration is hard-wired and cannot be changed.  Serial port settings are under software control, and must be initialized for correct baud rate, parity, etc. 

## License
This project is licensed under the Creative Commons - Attribution - ShareAlike 3.0 License

## Attribution
This board was derrived from works by, uses design elements from, or contains sofware writen by the following:
* Rob Krenicki (https://github.com/rkrenicki)
* Sergey Kiselev (http://www.malinov.com/Home/sergeys-projects)
* James Pearce (https://www.lo-tech.co.uk/)
* Adrian Black (https://www.youtube.com/user/craig1black/featured)
* Jacob Dorne of Monotech PCs (https://monotech.fwscart.com/)
* XTIDE Universal BIOS Team (http://www.xtideuniversalbios.org/)

