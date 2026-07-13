# Arch Linux

Arch Linux is different than distros like `Ubuntu` because it is so minimal and DIY focused. 
You do not get a pre configurated system - you build it yourself from the ground up.
You choose, kernel, bootloader, desktop, drivers and so on.

## Why use Arch?

- Full control – nothing is pre-installed that you don't want
- Learning – you understand your system much better because you built it yourself
- Up-to-date – rolling releases always mean the latest software (see below)
- Simple – no bloatware, no unnecessary pre-installed stuff
- Arch Wiki – considered one of the best Linux documentation resources available

## Rolling Release

Most distros (Ubuntu) use `hard versions` (Ubuntu 24.04).
These versions get newly released every few years.
Arch is different because it uses so called `rolling releases`

- No version like `Version 10.2.12`
- Updates come ongoing, when software packages are updated
- Always up-to-date
- More bugs in new software

## Package manager: Pacman

Arch uses its own package manager called `Pacman`

Important commands are: 

| *Command* | *Meaning* | 
|-------------|------------|
|`pacman -S package|Install package|
|`pacman -R package|Remove package|
|`pacman -Syu|Update system|
|`pacman -Ss <package>`| Search Package|
|`pacman -Q|List installed packages| 

## AUR (Arch User Repository)

Besides the official repositories exists the `AUR` - a community maintained collection of things like software, that are not officially in arch integrated. 
Pacman cant use the `AUR`. This is why you need helpers like `yay` which automate the building and installing.

## Installation 

This is where Arch is very different from other distros. Arch has traditionally no graphical installer. Everything is done using the command line. 
It is installed step, by step by hand (Partitions, Filesystem, Bootloader, Network)
This is why the installation is considered as an entry hurdle.

>[!NOTE]
> By now you can use the official `archinstall`-Script to simplify the process


### Classic Install

Setup documentation for a arch install without a desktop on a virtual machine without UEFI with ethernet:

To install arch without the `archinstall`-Script you can select a keyboard layout to make your life a little easier:

To see all available keyboard layouts:

`localectl list-keymaps`

To select a layout (For example German):

`loadkeys de`

---

#### Partitioning

Identify your hard drive:

`fdisk -l`

- `dev/loop*` -> Arch ISO, ignored
- `dev/sda` -> actual disk

Partitioning using `fdisk /dev/sda`

| Partition | Typ | Size |
|---|---|---|
| `/dev/sda1` | Linux swap (Hex `82`) | 4 GiB |
| `/dev/sda2` | Linux (Standard `83`) | Rest of disk |

Orders in fdisk:

```
n → p → 1 → Enter → +4G      (Swap-Partition)
n → p → 2 → Enter → Enter    (Root-Partition, Rest of disk)
t → 1 → 82                   (Set Swap-Typ)
p                             (Control)
w                             (write & exit)
```

---

#### Formatting & Mounting

```bash
mkswap /dev/sda1
swapon /dev/sda1
mkfs.ext4 /dev/sda2
mount /dev/sda2 /mnt
```

---

#### Installing bases system

To install the base system use pacstrap:

```bash
pacstrap -K /mnt base linux linux-firmware
```

If you need other things like `nano`, `vim` or other things you can install them nearly the same:

```bash
pacstrap -K /mnt nano vim networkmanager
```

> [!NOTE]
> `nano` and `vim` are not included in the new version. `networkmanager` is needed to connect to the internet after the first reboot

---

#### Generate fstab

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

Check:

```bash
cat /mnt/etc/fstab
```

---

#### Change to new system

```bash
arch-chroot /mnt
```

From that point on, all commands change things in the system not the ISO.

---

#### Time Zone

Setting time zone for `Europe/Vienna`

```bash
ln -sf /usr/share/zoneinfo/Europe/Vienna /etc/localtime
hwclock --systohc
```

---

#### Locale

`/etc/locale.gen` 

- If you want an English terminal remove the `#` for `en_US.UTF-8 UTF-8`
- If you want an German terminal remove the `#` for `de_DE.UTF-8 UTF-8`

After:

```bash
locale-gen
echo "LANG=de_DE.UTF-8" > /etc/locale.conf
```

---

#### Hostname

```bash
echo "archvm" > /etc/hostname
```
Add to `/etc/hosts`:
```
127.0.0.1   localhost
::1         localhost
127.0.1.1   archvm
```

---

#### Root-Password

```bash
passwd
```

---

#### Bootloader

```bash
pacman -S grub
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

---

#### Enable services

```bash
systemctl enable NetworkManager
```

---

#### Cleanup and reboot

```bash
exit                # exit chroot
umount -R /mnt      
swapoff /dev/sda1
reboot
```

> [!IMPORTANT]
> Remove the Arch-ISO from the virtual disk drive while the VM is rebooting. (Devices -> Optical Drives -> Remove Disk) So it boots from the disk, not the ISO

If everything was setup correctly you should see a login prompt `archvm login:` , log in with `root` + set password