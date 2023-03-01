---
title: Disable baloo file extractor
date: 2017-11-16 08:33:44
tags:
  - File
categories:
  - GNU/Linux
  - KDE
---

## Disable baloo-file-extractor (KDE 5)  ##

Run below command from the console:

``` bash
$ balooctl status
$ balooctl disable
```

Remove the local content:

``` bash
$ rm -rfv ~/.local/share/baloo
```
