---
title: Bootable CD from ISO
tags:
  - Bootable
  - ISO
categories:
  - GNU/Linux
  - CLI
date: 2016-09-15 11:39:55
---

Execute below command to create a bootable CD/USB from the ISO `/path/to.iso` to the device `/dev/sdb`.

``` bash
$ sudo dd if=/path/to.iso of=/dev/sdb bs=16M
```
Some documetation in regards the **dd** command.

### Name
**dd** - convert and copy a file

### Description
The **dd** utility copies the standard input to the standard output. Input
data is read and written in 512-byte blocks. If input reads are short, input from multiple reads are aggregated to form the output block. When
finished, **dd** displays the number of complete and partial input and output blocks and truncated input records to the standard error output.

##### The following operands have been used for this example.
```
bs=n                    Set both input and output block size to n bytes,
                        superseding the ibs and obs operands.  If no
                        conversion values other than noerror, notrunc or
                        sync are specified, then each input block is
                        copied to the output as a single block without
                        any aggregation of short blocks.

if=file                 Read input from file instead of the standard input.

of=file                 Write output to file instead of the standard
                        output.  Any regular output file is truncated
                        unless the notrunc conversion value is specified.
                        If an initial portion of the output file is
                        seeked past (see the oseek operand), the output
                        file is truncated at that point.
```

You can check more documetation on below links.
- https://www.gnu.org/s/coreutils/manual/html_node/dd-invocation.html
- http://ibgwww.colorado.edu/~lessem/psyc5112/usail/man/solaris/dd.1.html
- http://www.linuxguide.it/command_line/linux-manpage/do.php?file=dd
