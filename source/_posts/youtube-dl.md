---
title: youtube-dl
tags:
  - youtube-dl
categories:
  - CLI
  - youtube-dl
date: 2016-09-13 16:13:19
---

**[youtube-dl][1]** is a command-line program to download videos from YouTube.com and a few more sites. It requires the Python interpreter, version 2.6, 2.7, or 3.2+, and it is not platform specific. It should work on your Unix box, on Windows or on Mac OS X. It is released to the public domain, which means you can modify it, redistribute it or use it however you like.

    youtube-dl [OPTIONS] URL [URL...]

## My common options

OPTIONS

    -i, --ignore-errors              Continue on download errors, for example to
                                     skip unavailable videos in a playlist

    -w, --no-overwrites              Do not overwrite files

    -c, --continue                   Force resume of partially downloaded files.
                                     By default, youtube-dl will resume

    -F, --list-formats               List all available formats of requested
                                     videos

    -f, --format FORMAT              Video format code, see the "FORMAT
                                     SELECTION" for all the info

Subtitle Options:

    --all-subs                       Download all the available subtitles of the
                                     video
Authentication Options:

    -u, --username USERNAME          Login with this account ID
    -p, --password PASSWORD          Account password. If this option is left

## Examples
  ```
  $ youtube-dl --all-subs -f '(mp4)[height=720]' -iwc --username yourusername --password yourpassword "https://www.anyresource.com/content"
  ```
  ```
  $ youtube-dl --all-subs -f '(mp4)[height=720]' -iwc --username yourusername --password yourpassword -o '%(playlist)s/%(chapter_number)s - %(chapter)s/%(playlist_index)s. %(title)s.%(ext)s' https://www.anyresource.com/content --playlist-start 14
  ```

## How to download your Udemy course videos using youtube-dl
> $ youtube-dl --list-extractors | grep udemy

## Steps
1.  Get link to the course to download. e.g. https://www.udemy.com/course-name/
2. Login into udemy website, save the cookie from chrome using Chrome [Cookie.txt][2] export extension. Save it to file udemy-cookies.txt
3. Get the link of the video that you want to download. usually in format. Use the command provided below where you have to replace the {course_link} and {path_to_cookies_file} with respective paths.

```
$ youtube-dl {course_link} --cookies {path_to_cookies_file}
```

```
$ youtube-dl --cookies ./udemy-cookies.txt https://www.udemy.com/course-name/
```

**Notes**
- If you have previously installed `youtube-dl`, you should update it before attempting to download your Udemy courses
  ```
  $ youtube-dl -U
  ```
- If you want your videos to be organized by chapter and the indices included, you can specify the output flag `-o`
  ```
  $ youtube-dl --cookies ./udemy-cookies.txt -o '%(playlist)s/%(chapter_number)s - %(chapter)s/%(playlist_index)s. %(title)s.%(ext)s' https://www.udemy.com/course-name/
  ```

**My preference**
  ```
  $ youtube-dl --cookies cookies.txt -o %(playlist)s\%(chapter_number)s.%(chapter)s\%(playlist_index)s.%(title)s.%(ext)s https://www.udemy.com/course-name
  ```

**Source**
- [How to download your Udemy course videos using youtube-dl](https://gist.github.com/barbietunnie/8531d9c26cd1c0668e7278c7c4ba5853#how-to-download-your-udemy-course-videos-using-youtube-dl)

[1]:https://github.com/rg3/youtube-dl
[2]:https://chrome.google.com/webstore/detail/cookiestxt/njabckikapfpffapmjgojcnbfjonfjfg
