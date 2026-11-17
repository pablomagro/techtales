---
title: Fix "Desktop effects were restarted due to a graphics reset" on Debian 13 with NVIDIA
date: 2026-11-18 21:00:00
tags:
  - Linux
  - Debian
  - NVIDIA
  - KDE
categories:
  - Linux
---

After upgrading Debian 12 (bookworm) to 13 (trixie) on a KDE Plasma 6 machine with an NVIDIA GTX 1650 SUPER, KDE kept showing **"Desktop effects were restarted due to a graphics reset"** and Plasma Wayland would not start. Two separate causes, two small fixes.

<!-- more -->

## Summary

| # | Symptom | Cause | Fix |
|---|---|---|---|
| 1 | Wayland session fails (`No suitable DRM devices have been found`) | Still running the old bookworm kernel (6.1), NVIDIA `modeset` off | Install the trixie kernel and headers, enable `nvidia-drm modeset=1` |
| 2 | Message appears after hibernate or suspend | NVIDIA driver does not save GPU memory across sleep, KWin loses its GL context | Set `NVreg_PreserveVideoMemoryAllocations=1` |

## Problem 1: Old kernel and Wayland not starting

### Diagnose

```bash
uname -r
sudo dkms status
sudo cat /sys/module/nvidia_drm/parameters/modeset
```

| Output | Meaning |
|---|---|
| `uname -r` shows `6.1.x` | Still on the bookworm kernel under trixie userland |
| `modeset` prints `N` | Wayland cannot use the NVIDIA GPU |

The upgrade never installed the `linux-image-amd64` metapackage, so no trixie kernel was pulled in.

### Fix

Install the kernel and headers. The headers trigger the DKMS build of the NVIDIA module.

```bash
sudo apt install linux-image-amd64 linux-headers-amd64
sudo dkms status
```

Wait for a `6.12.x` entry marked `installed`, then reboot. Enable modesetting:

```bash
echo 'options nvidia-drm modeset=1' | sudo tee /etc/modprobe.d/nvidia-drm.conf
sudo update-initramfs -u
sudo reboot
```

### Verify

```bash
uname -r
sudo cat /sys/module/nvidia_drm/parameters/modeset
echo $XDG_SESSION_TYPE
```

Expected: a `6.12.x` kernel, `Y`, and `wayland` (after choosing "Plasma (Wayland)" at the login screen).

## Problem 2: Graphics reset after hibernate or suspend

### Diagnose

```bash
sudo grep -i Preserve /proc/driver/nvidia/params
systemctl list-unit-files 'nvidia-*'
```

| Output | Meaning |
|---|---|
| `PreserveVideoMemoryAllocations: 0` | GPU memory is lost on sleep, this is the problem |
| `nvidia-suspend`, `nvidia-hibernate`, `nvidia-resume` enabled | Services are fine, only the module option is missing |

If the services are missing, install them first with `sudo apt install nvidia-suspend-common` and enable them with `sudo systemctl enable nvidia-suspend nvidia-hibernate nvidia-resume`.

### Fix

```bash
echo 'options nvidia NVreg_PreserveVideoMemoryAllocations=1 NVreg_TemporaryFilePath=/var/tmp' | sudo tee /etc/modprobe.d/nvidia-power.conf
sudo update-initramfs -u
sudo reboot
```

`/var/tmp` is used because `/tmp` is RAM-backed and the saved GPU memory can be large.

### Verify

```bash
sudo grep -i Preserve /proc/driver/nvidia/params
```

Expected: `PreserveVideoMemoryAllocations: 1`. Then hibernate or suspend and resume. The message should be gone.

## Hibernate prerequisites

| Check | Command | Needed |
|---|---|---|
| Swap size | `free -h` | At least as large as the RAM in use |
| Swap type | `sudo swapon --show` | A partition resumes automatically |
| Resume device | `cat /sys/power/resume` | Not `0:0` |

## Tips

- `dkms` and `swapon` live in `/usr/sbin`, which is not in a normal user's PATH on Debian. Use `sudo`.
- If the new kernel fails to boot, pick the old kernel under "Advanced options" in GRUB.
- Keep the old 6.1 kernel until the new one is stable, then run `sudo apt autoremove --purge`.
- Keep X11 as a fallback: choose "Plasma (X11)" from the session menu at the login screen.

## Environment

| Item | Value |
|---|---|
| OS | Debian 13 (trixie), upgraded from 12 |
| Desktop | KDE Plasma 6, Wayland |
| Kernel | 6.12.117+deb13-amd64 |
| GPU | NVIDIA GeForce GTX 1650 SUPER |
| Driver | `nvidia-driver` 550.163.01 |
