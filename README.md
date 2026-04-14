# lxipmadi DKMS — Digigram LX-IP / LX-MADI driver

Patched version of the Digigram lxipmadi 3.1.2 driver for modern kernels (5.12+).

## Patches applied

- Replaced removed `snd_printdd()` with `pr_debug()` in `lx_core.h`
- Removed `MODULE_SUPPORTED_DEVICE()` from `lxmadi.c` and `lxip.c` (macro removed in kernel 5.12)

## Prerequisites

```sh
sudo apt install dkms linux-headers-$(uname -r)
```

## Install via DKMS

```sh
sudo cp -r . /usr/src/lxipmadi-3.1.2
sudo dkms add lxipmadi/3.1.2
sudo dkms install lxipmadi/3.1.2
```

## Load the modules

```sh
sudo modprobe snd-lxip
sudo modprobe snd-lxmadi
```

## Verify

```sh
aplay -l
cat /proc/asound/cards
```

> **Note:** Your user must be in the `audio` group to access ALSA devices:
> ```sh
> sudo usermod -aG audio $USER
> ```
> Log out and back in for the change to take effect.

## Uninstall

```sh
sudo dkms remove lxipmadi/3.1.2 --all
sudo rm -rf /usr/src/lxipmadi-3.1.2
```
