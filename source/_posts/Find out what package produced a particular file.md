---
title: Find out what package produced a particular file
date: 2020-04-13T11:46:03+12:00
tags:
  - Packages
categories:
  - GNU/Linux
  - Debian
---

To identify the package that produced the file named foo execute either:

* dpkg --search foo

      This searches for foo in installed packages. (This is (currently) equivalent to searching all of the files having the file extension of .list in the directory /var/lib/dpkg/info/, and adjusting the output to print the names of all the packages containing it, and diversions.).

      A faster alternative to this is the dlocate tool.

          dlocate -S foo

* zgrep foo Contents-ARCH.gz

      This searches for files which contain the substring foo in their full path names. The files Contents-ARCH.gz (where ARCH represents the wanted architecture) reside in the major package directories (main, non-free, contrib) at a Debian FTP site (i.e. under/debian/dists/jessie). A Contents file refers only to the packages in the subdirectory tree where it resides. Therefore, a user might have to search more than one Contents files to find the package containing the file foo.

      This method has the advantage over dpkg --search in that it will find files in packages that are not currently installed on your system.

* apt-file search foo

      If you install the apt-file package, similar to the above, it searches files which contain the substring or regular expression foo in their full path names. The advantage over the example above is that there is no need to retrieve the Contents-ARCH.gz files as it will do this automatically for all the sources defined in /etc/apt/sources.list when you run (as root) apt-file update.