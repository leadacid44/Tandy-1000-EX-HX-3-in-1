# Re-Imaging the Compact Flash (CF) Card
## Explanation/Overview
    There is no true "disk image" restore process in the modern sense, like with SD cards or USB drives.  Instead, rebuilding the CF card is effectively the same as installing DOS onto a new hard drive.
    For the purposes of the Tandy 1000 EX/HX, the CF card should be thought of as a solid state hard disk.  Installation uses DOS tools and behaves exactly like a real hard drive install.

## DOS Version
### Legal Notice
I am not a lawyer.  This is not legal advice.  Only use MSDOS if you own a legitimate copy.  Do not distribute copyrighted software.
I include instructions here for MSDOS because it is my personal recommendation.
I also include FreeDOS instructions as it can be freely used without purchase.

### MSDOS
I strongly recommend MS-DOS v5.0.  So much so, that I don't really recommend anything else.  Version 5 is a good blend between modernity and light resources.  Version 3 and version 6 will both work, but with some caveats.
MS-DOS v3 is older than necessary, and has no meaningful advantages over v5.  
MS-DOS v6 is noticibaly slower and consumes more memory, and also has no meaningful advantages over v5.
If you intend to install from physical media, get the correct media for the disk drive in your system, e.g. 360k or 720k.
If you are going to use the 'serdrive' serial floppy drive method, use the 720k images.  (or maybe the 1.44?)
A great thing about the serdrive serial floppy drive is that it supports *any* standard floppy disk size.  So for example, you can use 1.44MB floppy images on a system that only has a 360k drive.
There's no real reason to get branded (e.g. Tandy) versions of the OS.
I won't recommend a place to get install media, but...
If you are searching online for the version 5.00 720k disk images, a known good set is commonly found in a 7zip archive file "Microsoft MS-DOS 5.00 (3.5-720k).7z".
Same, for the 360k disk images, "Microsoft MS-DOS 5.00 (5.25-360k).7z"
Quick tip, you can (generally) convert a 1.44MB floppy to a 720k floppy by putting a piece of opaque tape over the left-hand shutter on the disk.
https://www.instructables.com/Convert-a-144mb-floppy-to-720k/
I've had good luck formatting the new 720k disks on the Tandy itself.  I then write the disks using a Windows XP PC with a 3.5" floppy drive.
Then, if you are using WinImage to write the DOS disk images to the physical disks, I recommend using the 'Write disk' option, not the 'Format and write disk'.  Seems to work better.

### FreeDOS
FreeDOS works great, it just doesn't install nicely on 8086-class machines.  
https://www.youtube.com/watch?v=EOVLlMQs9f8
https://archive.org/details/free-dos-1.3-8086-minimized
You can get a copy of the FreeDOS images from my github page here: <URL>
Creating the FreeDOS 1.3 disks is a little bit more involved than the MS-DOS ones.
Because the FreeDOS disk images are 360k in size but our 3.5" floppy drive can't write a 360k image, we have to convert the image to be 720k.
Open the image in WinImage.  Then go Image --> Change format... --> 720KB --> OK
Disk --> Format and write disk

## Installation Methods
There are two main ways to install DOS onto a CF card; either via physical floppy disks, or via the XTIDE serial floppy (serdrive).  
Both methods work well.  Your choice depends primary on available hardware.

### Physical Media
**Pros**
- Simple and well understood
- No host PC required during install

**Cons**
- Requires a working Tandy floppy drive
- Requires good floppy media
- Writing 360k disks on modern systems can be unreliable
720k disks are generally the most reliable option and work well across both the Tandy and modern PCs.  Working 360k disks are often harder to find, and are subject to drive head alignment issues.

### Serdrive
Great explaination here: https://minuszerodegrees.net/xtide/Serial%20drive/Serial%20drive.htm
Recommend version 'v2.0.0 Beta 3 (Apr 16 2019)' as it fixes a bug with 720k disk images. https://forum.vcfed.org/index.php?threads/xtide-universal-bios.18240/page-22#post-853254
Requires a host PC to run the software.  Windows XP or higher is required.
Requires the host PC have a serial port.  A USB to serial port adapter can work well.
Requires a null-modem, DB9 M-M cable to connect both.
Keystroke timing can be tricky, but once you get the hang of it, is relatively strightforward.
Allows use of any compatable floppy disk image, even if the Tandy didn't originally support it - e.g. 1.44MB floppy disks.
Can be faster than original FDD interface!
If it doesn't work, can be difficult to determine why.

## Tools and Supplies

### CF Card
I recommend CF cards between 32 and 512 megabytes.  
Smaller cards would work, but you would likely run into disk space constraints.
Larger cards would work, but are likely larger than necessary.  The XTIDE interface has no pratical upper limit.  MS-DOS however, limits partitions to 2GB in size.
A great source of smaller, but not worn out, CF cards are ones from Cisco routers.  These can often be found on eBay for very reasonable prices.  Generally these Cisco cards are written to only a handfull of times in their lives.

### Windows PC
Windows XP (x86) works great

### CF Card Reader
Compact Flash to IDE Adapter + IDE to USB Adapter
https://www.amazon.com/Syba-Compact-Adapter-Enclosure-SD-ADA45006/dp/B0036DDXUM
https://www.amazon.com/Adapter-FIDECO-Converter-5-25-Inch-DVD-ROM/dp/B077N2KK27
USB Compact Flash Adapter
https://www.amazon.com/UGREEN-Reader-Adapter-5Gbps-Simultaneously/dp/B01ARAH6O0

### Floppy Disks
720k or 360k as appropriate

### Serial
Null-Modem Serial Cable
https://www.amazon.com/StarTech-com-10-Feet-RS232-Serial-SCNM9FF/dp/B00006B8BJ
USB to Serial Adapter
https://www.amazon.com/Sabrent-Converter-Prolific-Chipset-CB-DB9P/dp/B00IDSM6BW

## Card Prep
The general idea here is that we want to wipe the card of any previous content.  This can be accomplished in many ways.
WARNING!  This process has the potential to destroy the contents of *any* disk on your system.  Be absolutely sure you are working with the CF card before wiping its contents!
WARNING!  This process will destroy all contents of your CF card!  Ensure this is what you want to do!

### Windows Host PC
Note, 'diskpart' is the perferred method, as it performs a much more thourgouh cleaning of the card.  However, 'diskpart' can have trouble identifying cards on some adapters, presumably whether or not the disk is considered removable.  For example, on my Windows XP laptop, my PCMCIA to CF adapter does not work with diskpart, but my USB to CF adapter does.
Note, if you experience a lot of delays or long scan times within either diskpart or disk management, it is possible that the CF card is damaged or corrupted.  If possible, try a different card.
Note, if you are unsure if your card is working correclty, and have access to a Linux system, it may be useful to do a zero wipe of the card.  This will write zeros to all of the sectors of the card, ensuring all can be written to.  
#### Diskpart        
Insert/connect CF card
Start --> Run --> 'diskpart' --> Enter
DISKPART> list disk
Identify the CF card.  Generally the size of the disk is the key identifyer.  E.g. a 32MB card would show a size of 24 MB.  Note the disk number and use in the next step.
DISKPART> select disk 1
DISKPART> clean
DISKPART> exit            
#### Disk Management
Insert/connect CF card
Start --> Run --> 'diskmgmt.msc' --> Enter.
Locate the CF card.
Right-click on the partition on the card and select 'Delete Partition...'
Click 'Yes' to continue
Safely eject the CF card from the system - OR - power off the Windows PC

Your CF card has now been prepared for DOS installation.
Insert the CF card into the Tandy.
Power on the Tandy, the XT-IDE interface should show the card and a name somewhat like the card manufacturer on the 'Master: 300h <BRAND NAME>'
If the card is not detected by XT-IDE here, or the card name is gibberish, it is likely that the card does not / will not work with the XT-IDE.  Try a different card.

## Card Rebuild

### Working FDD Method
Use this method if you have a working internal disk drive in your Tandy, and have a good set of installation media.

#### MS-DOS 5.00
Power on the Tandy
Insert MS-DOS 5.00 Install Disk 1 into the first disk drive.
When the XT-IDE interface displays, press 'A' to boot from the disk.
Note, because the CF card has been wiped and can no longer boot, if allowed to try it will say 'Boot sector not found' and automatically try booting from the next boot device, floppy drive 'A'.
The MS-DOS 5.00 installer starts.
Press Enter to continue.
Note, the Tandy arrow keys do not work correctly in the MS-DOS installer.  Instead, use the numpad keys to move.  E.g. 8=Up, 2=Down, 4=Left, 6=Right
When prompted, adjust the settings as appropriate for your use case.
I recommend setting the date and time correctly at this time.
When complete, highlight 'The settings are correct.' and press Enter.
Adjust the options as appropriate for your use case.
I recommend the default to install to C:\DOS
I recommend NOT running Shell on startup.
When complete, highlight 'The settings are correct.' and press Enter.
Adjust hard disk options as appropriate for your use case.
I recommend 'Allocate all free hard disk space for MS-DOS'.
Highlight the correct choice, and press Enter.
The MS-DOS installer will partitioning the CF card in the background and then reboot.  This allows the MS-DOS installer to be able to use the disk space.
When the XT-IDE interface displays, press 'A' to boot from the floppy disk
Note, because the CF card now has a partition table, but cannot boot.  If allowed to try booting, it will say 'Missing operating system' and halt.  If this happens, do a CTRL-ALT-DEL and boot from the floppy drive.
The MS-DOS installer will automatically start again.
It will automatically format the CF card and copy the contents of the floppy to the card.
When prompted, insert Disk 2.
When prompted, insert Disk 3.
Remove the disk from the floppy drive and press Enter to exit the installer and reboot.
The Tandy will reset and boot from the CF card.

#### FreeDOS 1.3
Note, if FreeDOS appears to start booting (the dots '...' start appearing) but it errors out, try power-cycling the machine and booting again.
Power on the Tandy
Insert FreeDOS 1.3 Install Disk 1 into the first disk drive.
When the XT-IDE interface displays, press 'A' to boot from the disk.
Note, because the CF card has been wiped and can no longer boot, if allowed to try it will say 'Boot sector not found' and automatically try booting from the next boot device, floppy drive 'A'.
FreeDOS starts.
Enter 'fdisk' and press enter.
Fdisk starts.
Do you want to use large disk support? Y/N --> No.
Choose one of the following --> 1. Create DOS partition
Choose one of the following --> 1. Create Primary DOS Partition
Do you wish to use the maximum... --> Yes.
Primary DOS Partiton created.
Press Esc key.
Press Esc key. (Again)
Press Esc key. (Yet again)
Press CTRL-ALT-DEL to reboot
When the XT-IDE interface displays, press 'A' to boot from the floppy disk
Note, because the CF card now has a partition table, but cannot boot, if allowed to try booting, it will say 'partition signature !=550A' and halt.  If this happens, do a CTRL-ALT-DEL and boot from the floppy drive.
Enter 'format c:' and press enter.
Proceed with format? --> Yes. Enter.
Enter volume label --> <blank> Enter.
Note, the format should complete very quickly.  A 32MB CF card took ~3 seconds.
Enter 'sys c:' and press enter.
This will take a few seconds and will give an error about failing to open 'A:COMMAND.COM'.  This is normal.
Enter 'setup.bat' and press enter.
When prompted, insert disk 2 and press enter to continue.
When complete, either press CTRL-ALT-DEL, or power cycle the machine.
The Tandy will boot FreeDOS 1.3 from the CF card.

### SerDrive Method
This method works extremely well, if you have the tools available.

#### Host PC Prep
I used a Windows XP laptop with a USB to Serial adapter. Theoretically a physical serial port would work just as well.
Serdrive supports Windows XP and higher, I've only tested with Windows XP.
Place a copy of the 'serdrive' software onto the PC, for example into a folder called 'C:\Tandy1000'.  Version 'v2.0.0 Beta 3 (Apr 16 2019)' is the recommended version.  This software version seems to work correctly with 720k disks.
https://forum.vcfed.org/index.php?threads/xtide-universal-bios.18240/page-22#post-853254
Place a copy of the desired DOS install disks onto the PC into the same folder.
Connect the PC to the Tandy using a DB9 null-modem cable.
Identify the COM port on the PC that your cable is connected to.  My USB adapter was COM4.
Critical Note --> I've found that, at least on my Windows XP laptop, I have to open the serial port with TeraTerm or HyperTerminal first.  Open eithe program, connect to the COM port with any settings, and then close the program.  This seemingly "sets up" the port?  Any serial port settings seems to work, and the 'setup' that it does lasts until Windows is rebooted.  If you don't do this step, the Tandy will not detect the serdrive presented disk image.
Open Command Prompt (as Administrator, if applicable)
Browse to the folder containing serdrive.exe.
cd c:\Tandy1000
Run the serdrive command:
serdrive.exe -v2 -b 115.2 -c 4 <FILE NAME>
Flags explained:
-v2         = Verbose level 2
-b 115.2    = 115200 baud
-c 4        = COM port 4
<FILE NAME> = DOS installation floppy image, e.g. MS-DOS V5.00 DISK 1 of 3

#### Tandy Prep
Note, this will only work if the Tandy has one physical floppy drive.
Prep the Host PC with serdrive and disk 1 your DOS installation.
Power on the Tandy
Quickly press the F6 button to toggle 'ComDtct' or COM Detect.  The 'ComDtct' option will highlight.
The screen will display 'Master at COM Detect:' below where it typically shows the detected compact flash drives.
Quickly press the 'A' key to select 'FDD[A]'.  'FDD[A]' will highlight and ComDtct will no longer be highlighted.
Quickly press the 'B' key to toggle from booting from floppy disk drive 'A' the internal floppy drive, to floppy disk drive 'B', the serial drive.  'FDD[B]' will be displayed.
The screen will display 'Master at COM Detect: <FILE NAME> (COM1/115.2K)' if it correctly communicated with the Host PC and detected the floppy disk image.
Note, <FILE NAME> will be the litteral file name of the floppy image on the Host PC, for example 'DISK01.IMG'.
The Tandy will begin booting from the virtual serial floppy disk drive.
Note, if the XTIDE interface says 'Master at COM Detect: not found', confirm that 
the serdrive software is running
the serdrive software is configured for the correct serial port
you are using a null modem serial cable
you have opened TeraTerm, conneted to the COM port, and closed the software
Note, if the Tandy fails to boot from the virtual floppy, confirm that you toggled FDD boot and toggled between drives A and B.
Note, if you experience errors with data transfer between the Host PC and the Tandy, try reducing the serial baud rate from 115,200 to 9,600 (e.g 115.2 to 9600).  It will be signifigantly slower, but should work universally.
On the Host PC, you will see messages scrolling in the command window of heads, cylinders, sectors, LBA, etc. as the image is accessed by the Tandy.

#### MS-DOS            
The MS-DOS 5.00 installer starts.
Follow the setup and install instructions the same as for physical disk installation.
When the MS-DOS installer reboots, you will need to again boot from floppy:
Quickly press the F6 button to toggle 'ComDtct'.
Quickly press the 'A' key to select 'FDD[A]'.
Quickly press the 'B' key to toggle between drive 'A' and 'B'.
The Tandy will begin booting from the virtual serial floppy disk drive.
The MS-DOS installer will automatically start again.
When prompted to change disks, on the Host PC, in the 'serdrive' software console window, press CTRL-C to terminate the serdrive program, and then run the program again, changing the command line options to specify the next disk.
When the install is complete, on the Host PC, press CTRL-C again to terminate the serdrive program.  Then on the Tandy, press Enter to exit the installer and reboot.
The Tandy will reset and boot from the CF card.

#### FreeDOS
FreeDOS starts.
Follow the setup and install instructions the same as for physical disk installation.
When you reboot the system with CTRL-ALT-DEL, you will need to again boot from floppy:
Quickly press the F6 button to toggle 'ComDtct'.
Quickly press the 'A' key to select 'FDD[A]'.
Quickly press the 'B' key to toggle between drive 'A' and 'B'.
The Tandy will begin booting from the virtual serial floppy disk drive.
FreeDOS starts (again).
Again, follow the setup and install instructions the same as for physical disk installation.
When prompted to change disks, on the Host PC, in the 'serdrive' software console window, press CTRL-C to terminate the serdrive program, and then run the program again, changing the command line options to specify the next disk.
When the install is complete, on the Host PC, press CTRL-C again to terminate the serdrive program.  Then on the Tandy, either press CTRL-ALT-DEL, or power cycle the machine.
The Tandy will boot FreeDOS 1.3 from the CF card.

### Quality of Life Improvements
I've collected a few quality of life improvements in a zip file located here: <URL to be added later>
Extract the contents of the ZIP file to the root folder of your MS-DOS 5.00 CF card.
Note - in theory these improvements could also work on FreeDOS, but this is currently untested - certainly the autoexec.bat and config.sys files wouldn't work directly.
Contents:
DOSKEY\
Improved command history (F3) and command autocomplete (TAB).
DOSMAX\
Memory manager that lets you take advantage of the EMS memory on the 3-in-1 adapter, leaving more conventional memory available.
SETBP35\
Useful for HX Only - Change default device size of A: from 360k to 720k.
AUTOEXEC.BAT                
CONFIG.SYS
SETUPHX.COM
Useful for HX Only - Setup program for the Tandy 1000 HX.
