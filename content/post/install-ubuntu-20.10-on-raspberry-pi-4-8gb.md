---
title: "Install Ubuntu 20.10 on Raspberry Pi 4 8GB"
date: 2020-10-25T13:02:16Z
draft: false
authors: [Vojtech Vitek]
hero: "/images/rpi4.jpg"
featured: true
---

I decided to install Ubuntu 20.10 on my Raspberry Pi 4 (8GB RAM) booting from an USB SSD disk, so I could leverage a better I/O performance over an SD card and also to improve the lifespan of the device (SD cards tend to get corrupted over time by too many writes). Here's what I did:

# Prerequisities

- Raspberry Pi 4 with 8GB RAM
- SD card (I bought cheap SanDisk 32G card, nothing fancy since we're using it only for bootstrapping)
- SSD disk (I bought ADATA ASD600Q, a 500G SSD USB3.1 disk with 440Mb/s read & write speed, so we I could get a nice I/O performance boost)
- Micro-HDMI to HDMI converter
- HDMI cabel + monitor
- USB-C power adaptor

![image alt text](/images/rpi4.jpg)

# Install Raspberry OS on the SD card

The RPi can't boot from USB device by default. We need to use SD card first to update the RPi firmware, so the RPi can boot from an external USB disk with no card in the SD slot.

1. Plug-in the SD card into your computer (I used my older MacBook Pro's SD card reader slot)
2. Install [Raspberry Pi Imager](https://www.raspberrypi.org/blog/raspberry-pi-imager-imaging-utility/) for your OS
3. Open the program and install Raspberry Pi OS onto the SD card

# Install Ubuntu 20.10 (server) on SSD disk

Now, since we have Raspberry Pi Imager program open, let's prepare our SSD disk too.

1. Insert the SSD disk into your computer
2. Open the Raspberry Pi Imager program and install Ubuntu 20.10 server onto it.
3. Now, we need to overwrite firmware file on the SSD disk with the latest files from [Raspberry's firmware](https://github.com/raspberrypi/firmware) repo. Go to your SSD disk directory in your terminal and run the below command to download the latest .elf and .dat firmware files:
```bash
$ wget $( wget -qO - https://github.com/raspberrypi/firmware/tree/master/boot | perl -nE 'chomp; next unless /[.](elf|dat)/; s/.*href="([^"]+)".*/$1/; s/blob/raw/; say qq{https://github.com$_}' )
```
*(this command was taken from [atomicstack's gist](https://gist.github.com/atomicstack/9c43e452c4b7cefb37c1e78f65b0b1fa))*

# Boot Raspberry Pi from SD card & update the firwmare

Insert the SD card into the Raspberry Pi (it's on the back of the board) and connect your USB keyboard, mouse, ethernet, 

# Boot Raspberry Pi from SSD disk

