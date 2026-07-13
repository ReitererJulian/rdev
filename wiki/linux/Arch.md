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