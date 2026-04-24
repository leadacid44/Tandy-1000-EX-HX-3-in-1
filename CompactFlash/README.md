# Re-Imaging the Compact Flash (CF) Card

## Table of Contents

- [Explanation / Overview](#explanation--overview)
- [Choosing a DOS Version](#dos-version)
  - [Legal Notice](#legal-notice)
  - [MS-DOS](#ms-dos)
  - [FreeDOS](#freedos)
- [Installation Methods](#installation-methods)
  - [Physical Media](#physical-media)
  - [SerDrive](#serdrive)
- [Tools and Supplies](#tools-and-supplies)
  - [CF Card](#cf-card)
  - [Windows PC](#windows-pc)
  - [CF Card Reader](#cf-card-reader)
  - [Floppy Disks](#floppy-disks)
  - [Serial](#serial)
- [Card Prep](#card-prep)
  - [DiskPart Method (Windows)](#diskpart-method-windows)
  - [Disk Management Method](#disk-management-method)
- [Quality of Life Improvements](#quality-of-life-improvements)

---

## Explanation / Overview

There is no true “disk image” restore process in the modern sense (as with SD cards or USB drives). Instead, rebuilding the CF card is effectively the same as installing DOS onto a new hard drive.

For the purposes of the Tandy 1000 EX/HX, the CF card should be thought of as a solid-state hard disk. Installation uses DOS tools and behaves exactly like a real hard drive install.

---

## Choosing a DOS Version

### Legal Notice

I am not a lawyer. This is not legal advice. Only use MS-DOS if you own a legitimate copy. Do not distribute copyrighted software.  I include instructions here for MS-DOS because it is my personal recommendation.  I also include FreeDOS instructions as it can be freely used without purchase.

### MS-DOS

I strongly recommend **MS-DOS v5.0**. Its a good blend between modernity and light resource usage.

- **MS-DOS v3** – Older than necessary, no meaningful advantages
- **MS-DOS v6** – Slower, higher memory usage, no advantages on 8086

**Media Notes**

- Physical installs: Use 360k or 720k media
- SerDrive installs: 720k or 1.44MB images

SerDrive supports all standard floppy sizes.

I won't tell you where to get copies of DOS online, but known-good image names could be:

- `Microsoft MS-DOS 5.00 (3.5-720k).7z`
- `Microsoft MS-DOS 5.00 (5.25-360k).7z`

720k disks can usually be created by taping the write-detect hole on a 1.44MB floppy:
https://www.instructables.com/Convert-a-144mb-floppy-to-720k/

When using WinImage to write the disk images to physical disks, I sometimes had better luck by formatting the disk on the Tandy itself, and then choosing **Write disk** over **Format and write disk** on the modern PC.

### FreeDOS

FreeDOS works well but requires extra steps on 8086-class systems.

- Video walkthrough: https://www.youtube.com/watch?v=EOVLlMQs9f8
- Minimal image set: https://archive.org/details/free-dos-1.3-8086-minimized

A copy of the FreeDOS disk images is also available here:
https://github.com/leadacid44/Tandy-1000-EX-HX-3-in-1/blob/main/CompactFlash/FreeDOS%201.3%208086%20Minimized.zip

Since the FreeDOS images are 360k, they must be converted to 720k before writing with WinImage:

1. Open image in WinImage
2. Image → Change format → 720KB
3. Disk → Format and write disk

---

## Installation Methods

Two supported installation paths exist:

- Physical floppy disks
- XT-IDE serial floppy (SerDrive)

Both work reliably depending on available hardware.

### Physical Media

**Pros**
- Simple and proven
- No host PC required

**Cons**
- Requires working floppy drive
- Requires good media
- 360k disks are unreliable on modern PCs

720k disks are the most reliable choice.

### SerDrive

Documentation:
https://minuszerodegrees.net/xtide/Serial%20drive/Serial%20drive.htm

Recommended version: **v2.0.0 Beta 3 (Apr 16 2019)**

Requirements:
- Windows XP or newer
- Serial port (USB adapters supported)
- DB9 null-modem cable

Supports all common floppy sizes and may outperform original floppy hardware.

---

## Tools and Supplies

### CF Card

Recommended size: **32–512 MB**

Cisco router CF cards are an excellent low-wear option.

### Windows PC

- Windows XP (x86) recommended

### CF Card Reader

- CF → IDE + IDE → USB adapter
- USB CF reader

### Floppy Disks

- 720k or 360k as appropriate

### Serial

- DB9 null-modem cable
- USB → serial adapter

---

## Card Prep

> **WARNING**
> This process permanently erases all data on the CF card.

### DiskPart Method (Windows)

```
DISKPART> list disk
DISKPART> select disk <N>
DISKPART> clean
DISKPART> exit
```

### Disk Management Method

1. Run `diskmgmt.msc`
2. Delete all partitions on the CF card
3. Safely eject the card

Insert the CF card into the Tandy and confirm detection in the XT-IDE BIOS.

---

## Quality of Life Improvements

Optional utilities and configuration files are available here:
<URL to be added>

Extract contents to the CF card root after DOS installation.

Includes:
- DOSKEY
- DOSMAX
- SETBP35 (HX only)
- AUTOEXEC.BAT
- CONFIG.SYS
