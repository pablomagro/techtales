---
title: Reducing PDF file-size in GNU/Linux
date: 2018-09-13 22:12:24
tags:
  - PDF
  - Ghostscript
categories:
  - GNU/Linux
---

I have tried several apps to compress PDF files and the best one in my opinion in terms of useability and compression is [ghostscript](https://www.ghostscript.com/index.html).

# Install

Run from a terminal below command if you are based on Debian and children.

```bash
# ghostscript - interpreter for the PostScript language and for PDF
apt install ghostscript
```

# Use

Run the following command to reduce the file-size of your PDF:

```bash
ghostscript -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/print -sOutputFile=new_file.pdf original_file.pdf
```

**Note**: You can use gs if you wish. For me it is an alias for `git status`.

```bash
type ghostscript
ghostscript is /usr/bin/ghostscript

ll /usr/bin/ghostscript
lrwxrwxrwx 1 root root 2 Sep  6 10:02 /usr/bin/ghostscript -> gs (/usr/bin/gs)
```

Now you have a few options here under -dPDFSettings:

* **/screen** Selects low-resolution output (72 dpi), and the lowest file-size.
* **/ebook** Selects medium-resolution output (150 dpi), with a medium file-size.
* **/printer** and **/prepress** are both the high-resolution options (300 dpi), which is mainly used for printing PDFs. As you might have guessed, this option gives you the biggest file-size (yes, even bigger than your mother).

# References

* How to Use Ghostscript: https://www.ghostscript.com/doc/9.20/Use.htm
