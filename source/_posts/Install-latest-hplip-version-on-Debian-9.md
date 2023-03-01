---
layout: latest
title: Install latest hplip version on Debian 9
date: 2017-12-29 11:35:26
tags:
  - Install
  - hplip
categories:
  - GNU/Linux
  - Debian
---

I bought a new HP Deskjet 2621 and I tried to install it using the hp-setup which didn't recognize it.

The problem is the hplip version (generaly 3.16.11+repack0-3 in jessie and 3.16.11+repack0-1~bpo8+1 in jessie-backports), if you have a too recent printer (like me), ppd files are not available in version 3.16.11+repack0-3.

I tried to install latest one [binary](https://sourceforge.net/projects/hplip/files/hplip/3.17.11/) (at that moment).

```bash
sh hplip-3.17.11.run
```

After the whole process a had a dependencies problems because packages:

* __pyqt4__
* __pyqt4-dbus__

had different names in 9.3:

* __python-qt4__
* __python-qt4-dbus__

So to fix it you have two options once downloaded the source code from above link.

1. Following the instructions from the following [link](https://answers.launchpad.net/hplip/+question/452076) (#3 message).
2. Compile and install it your self.

I chose the 2nd option:

```bash
~/src/hplip-3.17.11 $ ./configure
```

Here I found another dependencies issue:
```
"configure: error: cannot find net-snmp support (or --disable-network-build)"
```

Disabling the networking build is bad idea if you have a wireless printer, it won't work. Then your have to install the __net-snmp__ packages and the development packages for __openssl__.

Once installed above dependencies, I just executed bellow commands to install the hp-setup binary with my printer drivers.

```bash
~/src/hplip-3.17.11 $ make clean
~/src/hplip-3.17.11 $ ./configure
~/src/hplip-3.17.11 $ make
~/src/hplip-3.17.11 $ su -c "make install"
```

And then execute hp-setup ans install your printer:

<img src="https://i.imgur.com/A9DIJ2v.png" width="" height="" alt="Hp-setup example" />