---
title: How to provide non-free firmware files to the Debian Stretch Installer
tags:
  - Debian
categories:
  - GNU/Linux
  - Installer
date: 2018-01-03 20:09:55
---

When I attempted to install Debian (9.3) on my laptop / pc, I could not get a network connection, because the installer told me that it was missing the required firmware files for my network interfaces:

```txt
Some of your hardware needs non-free firmware files to operate.  The firmware can be loaded from
removable media, such as a USB stick or floppy.

The missing firmware files are: iwlwifi-6000g2b-6.ucode iwlwifi-6000g2b-5.ucode

If you have such media available now, insert it, and continue.
Load missing firmware from removable media?
```

As I have been in this situation several times when I do not have a easy access to internet using a wired connection and I have a wireless card where the driver is not recognized by debian, and I have decided to write these lines to remind me how to fix it.

## Faster solution

Use the unofficial ISO images with the non-free firmware already included (My normal option):
[http://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/](http://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/)

## Longer solution

Download the non-free firmware, store it within an usb drive and mount it during the installation; you can check [this post](https://www.linuxquestions.org/questions/debian-26/how-to-provide-non-free-firmware-files-to-the-debian-jessie-installer-4175542680/) out, it is very well explained. Below is a summary from above post:

* First, of course, I had to actually find the required firmware files. To that end:
* I went to the Debian site.
* I clicked the Debian Packages link, to continue to the Debian Packages page.
* Under the Packages header, I selected the Search the contents of packages link.
* In the Keyword: field, I entered: iwlwifi.
* Under Display:, I selected the option labelled packages that contain files whose names contain the keyword.
* I left the Distribution: value unchanged at stable.
* I changed the Architecture: value to 64-bit PC (amd64).
* I clicked the Search button.
* In the list of search results that appeared next, I looked for the two files that I needed: iwlwifi-6000g2b-5.ucode and iwlwifi-6000g2b-6.ucode. Both files were present in the firmware-iwlwifi package.
* I clicked one of the firmware-iwlwifi links, to move on to the Binary firmware for Intel Wireless cards page.
* Under the Download firmware-iwlwifi header, I clicked the all architecture link to continue.
* On the next page, I clicked the link to the site from which I wanted to download the file.

The Debian package firmware-iwlwifi_20161130-3_all.deb got downloaded for me.

Next, it was time to extract the contents of the downloaded packages:

I opened a command-line terminal window, and went to the directory where the packages were downloaded―which, in my case, was my personal download directory:
Code:

```bash
cd ~/Downloads
```

* I extracted the contents of both packages into the current directory:

```bash
dpkg-deb --extract firmware-iwlwifi_20161130-3_all.deb .
```

* I copied the entire contents of the firmware subdirectory to a USB stick that was formatted with a FAT filesystem.

Note, in particular, that the USB stick included the contents of the firmware directory, not the directory itself!

Finally, the time had come to retry the Debian installation. I simply booted the computer off the Debian 8.0.0 medium, and when it complained again about the missing firmware files, I took the following steps:

* Inserted the USB stick.
* pressed the `<CTRL>+<Alt>+<F2>` key combination, to switch to the second virtual terminal.
* ran either the blkid or the fdisk -l command, to find out under which device name the USB stick was known: /dev/sdc. Its FAT filesystem, which contained the firmware files, then, was /dev/sdc1.
* mounted the FAT filesystem under the /lib/firmware mountpoint―which, however, I had to create first:

```bash
mkdir /lib/firmware
mount /dev/sdc1 /lib/firmware
```

* I pressed `<Ctrl>+<Alt>+<F5>` to continue the installation process.

The firmware files were successfully loaded, and I got prompted for my wireless networking parameters.
