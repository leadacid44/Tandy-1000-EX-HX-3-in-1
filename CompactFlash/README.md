# Re‑Imaging the Compact Flash (CF) Card

## Explanation / Overview

There is no true “disk image” restore process in the modern sense (as with SD cards or USB drives). Instead, rebuilding the CF card is effectively the same as installing DOS onto a new hard drive.

For the purposes of the Tandy 1000 EX/HX, the CF card should be thought of as a solid‑state hard disk. Installation uses DOS tools and behaves exactly like a real hard drive install.

---

## DOS Version

### Legal Notice

I am not a lawyer. This is not legal advice. Only use MS‑DOS if you own a legitimate copy. Do not distribute copyrighted software.

I include instructions here for MS‑DOS because it is my personal recommendation.  
I also include FreeDOS instructions as it can be freely used without purchase.

### MS‑DOS

I strongly recommend **MS‑DOS v5.0**. Version 5 is a good blend between modernity and light resource usage. Versions 3 and 6 will both work, but with caveats:

- **MS‑DOS v3**  
  Older than necessary and has no meaningful advantages over v5.

- **MS‑DOS v6**  
  Noticeably slower, consumes more memory, and offers no meaningful advantages over v5.

**Media notes:**

- Use 360k or 720k disks for physical installs, as appropriate.
- For the `serdrive` method, 720k or 1.44MB images work well.

Serdrive supports *any* standard floppy size, allowing use of 1.44MB images even on systems originally limited to 360k.

There is no real benefit to branded (e.g. Tandy) DOS versions.

Known‑good MS‑DOS 5.00 image sets commonly appear as:

- `Microsoft MS‑DOS 5.00 (3.5‑720k).7z`
- `Microsoft MS‑DOS 5.00 (5.25‑360k).7z`

**Quick tip:** A 1.44MB floppy can usually be converted to 720k by covering the write‑detect hole:
https://www.instructables.com/Convert-a-144mb-floppy-to-720k/

Formatting 720k disks on the Tandy itself and writing images using Windows XP has proven reliable. When using WinImage, prefer **Write disk** over **Format and write disk**.

### FreeDOS

FreeDOS works well but does not install cleanly on 8086‑class systems without additional steps.

- Video: https://www.youtube.com/watch?v=EOVLlMQs9f8
- Minimal build: https://archive.org/details/free-dos-1.3-8086-minimized

FreeDOS images are available here:
<URL>

The 360k images must be converted to 720k before writing:

1. Open image in WinImage
2. Image → Change format → 720KB
3. Disk → Format and write disk

---

## Installation Methods

Two supported methods exist:

- Physical floppy disks
- XT‑IDE serial floppy (`serdrive`)

Both work well; choice depends on hardware availability.

### Physical Media

**Pros**
- Simple and well understood
- No host PC required during install

**Cons**
- Requires a working floppy drive
- Requires good media
- 360k disks are unreliable on modern hardware

720k disks are generally the most reliable option.

### SerDrive

Documentation:
https://minuszerodegrees.net/xtide/Serial%20drive/Serial%20drive.htm

Recommended version: **v2.0.0 Beta 3 (Apr 16 2019)**

- Supports Windows XP or newer
- Requires serial port (USB adapters work)
- Requires DB9 null‑modem cable

Supports all common floppy image sizes and can outperform original FDD hardware.

---

## Tools and Supplies

### CF Card

Recommended size: **32–512 MB**

Cisco router CF cards are an excellent low‑wear source.

### Windows PC

- Windows XP (x86) recommended

### CF Card Reader

- CF → IDE + IDE → USB
- USB CF reader

### Floppy Disks

- 720k or 360k as appropriate

### Serial

- DB9 null‑modem cable
- USB → serial adapter

---

## Card Prep

> **WARNING**  
> This process will permanently erase all data on the CF card. Double‑check disk selection.

### DiskPart Method (Windows)

```
DISKPART> list disk
DISKPART> select disk <N>
DISKPART> clean
DISKPART> exit
```

### Disk Management Method

1. Run `diskmgmt.msc`
2. Delete existing partition
3. Safely eject card

Insert the card into the Tandy and confirm detection in XT‑IDE BIOS.

---

## Quality of Life Improvements

Optional utilities are available here:
<URL to be added>

Extract to the CF card root after installation.

Contents include DOSKEY, DOSMAX, SETBP35 (HX only), and updated AUTOEXEC.BAT / CONFIG.SYS.
