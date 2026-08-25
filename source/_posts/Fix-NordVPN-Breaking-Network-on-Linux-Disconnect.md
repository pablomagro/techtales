---
title: Fix NordVPN Breaking Your Network on Linux After Disconnecting
date: 2026-08-26 00:00:00
tags:
  - Linux
  - NordVPN
  - Networking
  - Debian
categories:
  - Troubleshooting
---

If disconnecting NordVPN on Linux leaves you without internet access - no name resolution, no ping, `apt update` failing - the culprit is often the `nordvpnd` daemon fighting with NetworkManager, not NordVPN itself.

> Solution found and shared on the [Debian Forums](https://forums.debian.net/viewtopic.php?t=157619).

## The Problem

Stopping NordVPN from the console (`nordvpn d`) doesn't fully release control of the network. The `nordvpnd` daemon keeps running in the background even after the VPN connection itself is closed, and it can leave the system unable to resolve names, ping hosts, or reach the internet at all.

## Diagnosing It

First, list running services to confirm the daemon is still active even after stopping NordVPN from the console:

```
systemctl list-units --type=service
```

Look for:

```
nordvpnd.service                loaded active running NordVPN Daemon
```

## The Fix

Stop the daemon directly:

```
sudo systemctl stop nordvpnd
```

Then restart NetworkManager to restore connectivity:

```
sudo systemctl restart NetworkManager
```

After this, internet access, name resolution, and `apt update` should work again.

## What Was Confirmed

Testing the cycle further showed:

- Restarting `nordvpnd` and then connecting via `nordvpn c` worked fine, with the network staying up.
- Disconnecting again via `nordvpn d` reproduced the same network breakage as before.
- Stopping the daemon (`sudo systemctl stop nordvpn`) alone fixed it - no NetworkManager restart needed at that point.

## Takeaway

The workaround is to manually stop the `nordvpnd` daemon after disconnecting NordVPN, and start it again (or just let `nordvpn c` restart it) before reconnecting. It's a bit annoying to do by hand every time, but it reliably avoids the broken-network state. This could be scripted into a small wrapper around `nordvpn c` / `nordvpn d` if you want to automate it.
