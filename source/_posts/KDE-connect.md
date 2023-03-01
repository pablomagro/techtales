---
title: KDE connect
date: 2018-08-23 06:21:23
tags:
  - Applications
categories:
  - GNU/Linux
  - KDE
---

KDE Connect is a project to communicate across all your devices. For example, with KDE Connect you can receive your phone notifications on your desktop computer, control music playing on your desktop from your phone, or use your phone as a remote control for your desktop. To achieve this, KDE Connect:

implements a secure communication protocol over the network, and allows any developer to create plugins on top of it.
Has a component that you install on your desktop.
Has a KDE Connect client app you run on your phone.
This video from 2013 demonstrates some other cool features: https://www.youtube.com/watch?v=KkCFngNmsh0

## Installation

You will most likely find the KDE Connect desktop component as a package in your distribution's repos. If you use a desktop environment other than KDE's Plasma, you might also want to install indicator-kdeconnect, that provides a system tray as a GUI for other desktops.

The app for Android can be found in both the Google Play Store and the free and open store F-Droid. There was some development of a KDE Connect client app for iOS in 2014 (see source code) and supposedly a client app for Blackberry (where?).

## Browser Integration

KDE Connect can integrate into your browser's right-click menu easily.

if you use plasma, the browser Integration tool will handle this. see more on its page, Here

If you don't use plasma, but you use Firefox or [Chrome/Chromium](https://chrome.google.com/webstore/detail/kde-connect/ofmplbbfigookafjahpeepbggpofdhbo), see the following block for details on extensions for those.

An alternative native extension for Chrome/Chromium (or compatible) and [Firefox](https://addons.mozilla.org/en-US/firefox/addon/kde_connect/) users, lets you "send pages and content from your browser to connected KDE Connect devices, via browser action or context menu." See its [Github](https://github.com/pdf/kdeconnect-chrome-extension) page for installation instructions.

## Some util scripts

- **Shutdown:** ``systemctl poweroff``
- **Suspend:** ``systemctl suspend``
- **Hibernate:** ``systemctl hibernate``
- **Maximum Brightness**: ``qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.brightnessMax``
- **Lock Screen**: ``loginctl lock-session``
- **Unlock Screen**: ``loginctl unlock-session``
- **Close All Vaults**: ``qdbus org.kde.kded5 /modules/plasmavault closeAllVaults``
- **Forcefully Close All Vaults**: ``qdbus org.kde.kded5 /modules/plasmavault forceCloseAllVaults``
- **Custom Script**: ``konsole -e sudo /home/user/scripts/start-plex-kde-connect.sh``
    Note provide right sudo permissions for sh file to execute:

  ```bash
  sudo visudo
  ...
  %sudo   ALL=(ALL) NOPASSWD: /home/pablo/MEGAsync/Documents/scripts/stop-plex-kde-connect.sh
  ...
  ```

## Reference(s)

- KDEConnect reference [wiki](https://community.kde.org/KDEConnect).
- [KDE Connect/Tutorials/Useful commands](https://userbase.kde.org/KDE_Connect/Tutorials/Useful_commands).
