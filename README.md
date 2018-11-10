# rpi-backup

A small script to make compressed SD card images under macOS. Basic compression
(`bz2`, `zip` and `gzip`) uses the built-in macOS binaries. The only required
non-system dependency is `pv`.  That and better compression packages such as
XZ (`xz-utils`) and 7-Zip (`p7zip`) can easily be installed with Homebrew (`brew`).

## Installation
1) Install Brew: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2) Install PV, XZ-Utils and 7-Zip: `brew install pv xz-utils p7zip`
3) Download rpi-backup: `git clone https://github.com/timothybrown/rpi-backup.git`
4) Install:
  - `sudo mv rpi-backup/rpi-backup.sh /usr/local/bin/`
  - `sudo chmod +x /usr/local/bin/rpi-backup.sh`

## Usage
```
┌──────────────────────────────────────────────────────────────────────────────┐
│ rpi-backup v077 by Timothy Brown                                             │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│ Syntax: sudo rpi-backup /dev/disk# /path/to/backup.img [compression method]  │
│                                                                              │
│                              Compression Method                              │
├──────────┬──────────┬───────────┬────────────────────┬───────────┬───────────┤
│ Argument │   Tool   │ Algorithm │     Available      │ - Speed + │ - Ratio + │
├──────────┼──────────┼───────────┼────────────────────┼───────────┼───────────┤
│  xz      │ XZ Utils │ LZMA2     │ /usr/local/bin/xz  │ ╍╍◆╍╍╍╍╍╍ │ ╍╍╍╍╍╍◆╍╍ │
│  7z      │ 7-Zip    │ LZMA2     │ /usr/local/bin/7za │ ╍◆╍╍╍╍╍╍╍ │ ╍╍╍╍╍╍╍◆╍ │
│  gz      │ GNU Zip  │ DEFLATE   │ /usr/bin/gzip      │ ╍╍╍╍◆╍╍╍╍ │ ╍╍╍╍◆╍╍╍╍ │
│  zip     │ Info-ZIP │ DEFLATE   │ /usr/bin/zip       │ ╍╍╍╍◆╍╍╍╍ │ ╍╍╍╍◆╍╍╍╍ │
│  bz2     │ bzip2    │ BWT       │ /usr/bin/bzip2     │ ╍╍╍◆╍╍╍╍╍ │ ╍╍╍╍╍◆╍╍╍ │
│  z       │ compress │ LZW       │ /usr/bin/compress  │ ╍╍╍╍╍◆╍╍╍ │ ╍╍◆╍╍╍╍╍╍ │
│  raw     │ dd       │ None      │ /bin/dd            │ ╍╍╍╍╍╍╍╍◆ │ ◆╍╍╍╍╍╍╍╍ │
└──────────┴──────────┴───────────┴────────────────────┴───────────┴───────────┘
```
Example: `sudo rpi-backup /dev/disk4 ~/Desktop/raspbian.img zip`
Will result in a zip compressed file named `raspbian.img.zip` on your Desktop.
