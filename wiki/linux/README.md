# Linux

Linux is an `Open Source Operating System Kernel`. 

> [!IMPORTANT]
> Linux is just the kernel - the layer that lets hardware and software communicate

It manages things like:
- Process management (which program gets CPU time and when)
- Memory management
- Device drivers (access to hard drive, network, graphics card, etc.)
- File system access

But the kernel has no graphical interface, no programs and no package manager.
It can be looked at like a motor but not the whole car.

## Why people use Linux?

Why do people even use Linux when the competitors like Microsoft or Apple are that big?
Some reasons can be:

- Free & Open Source - source code is publicly viewable and changeable  
- Control & Customizability - almost every part of the system can be modified
- Stability & Performance - especially for servers
- Security - strict permissions, less of a target for malware than Windows
- Learning - understanding how an operating system works

## Where does it run?

Linux powers more devices than you might think.

Things like:
- Servers - majority of the internet runs on Linux
- IoT Devices - routers, smart tv's
- Android Smartphones - Android kernel is based on Linux
- Desktop - smaller community, but growing

## Distributions

Distributions. or short distros, are complete OS packages which combine the Linux kernel with other programs, drivers, and a desktop. 
User friendly distros are `Ubuntu` or `Linux Mint`
They can be an alternative to other operating system like Windows or MacOS.

Distros can be divided in these broad categories:

| *Type* | *Examples* | *Specialty* |
|-------|-----------|------------|
|Beginner Friendly | Ubuntu, Linux Mint | Pre configured, stable |
|Minimal, DIY | Arch Linux | Building your own System |
|Enterprise | RHEL | Focus on Server |
|Security | Kali | For special use cases (Pen testing) |

Most distros are based upon large `families`: 
- `Debian` -> (Ubuntu, Mint)
- `Red Hat` -> (Fedora)
- `Arch` -> (Endeavour OS)

## File system

Different than Windows (`C:` , `D:`), Linux only has one directory tree.
The tree starts with `/` (root) and everything is beneath this, even USB-Drives which get `mounted` into it.


| *Path* | *Purpose* |
|------|---------|
| `/bin`, `/usr/bin` | Executable programs (binaries). |
| `/boot` | Bootloader and kernel images. |
| `/dev` | Device files (e.g., hard drives, USB devices) represented as files. |
| `/etc` | System-wide configuration files. |
| `/home` | Users' personal home directories (e.g., `/home/max`). |
| `/lib`, `/usr/lib` | Shared libraries required by programs. |
| `/media`, `/mnt` | Mount points for removable and external storage devices. |
| `/opt` | Optional or third-party software packages. |
| `/proc` | Virtual filesystem containing information about running processes and the kernel. |
| `/root` | Home directory of the **root** user (not to be confused with `/`, the filesystem root). |
| `/sys` | Virtual filesystem providing information about hardware and kernel settings. |
| `/tmp` | Temporary files, often cleared automatically on reboot. |
| `/usr` | User applications, libraries, and documentation (contains the majority of the system's software). |
| `/var` | Variable data such as logs, caches, and databases. |

### Important concepts

> Everything is a file

In Linux is nearly everything a file. Even things like devices (`/dev/sda` for hard drives)
This makes the system uniform to use

Also files are `case sensitive` which means that `file.txt` and `File.txt` are not the same but two independent files. 

If a file can be executed is not defined by the ending (Like `.exe` for Windows) but by the `permissions` 

Every role has different permissions to: 

- Read
- Write
- Execute

Seeing what role has what permissions on a file us can use `ls -l`

The output might be something like this: 

`-rwxr-xr-- 1 max users 4096 Jul 13 10:00 script.sh`

| *Field* | *Example* | *Description* |  
|-------|---------|-------------|  
| **File Type & Permissions** | `-rwxr-xr--` | The first character indicates the file type, followed by the permission bits. |  
| **Hard Links** | `1` | Number of hard links pointing to this file. |  
| **Owner** | `max` | The user who owns the file. |  
| **Group** | `users` | The group that owns the file. |  
| **Size** | `4096` | File size in bytes. |  
| **Last Modified** | `Jul 13 10:00` | Date and time of the last modification. |  
| **Filename** | `script.sh` | The name of the file. |  
  
#### File Type  
  
The first character indicates the type of the file:  
  
| *Symbol* | *Meaning* |  
|--------|---------|  
| `-` | Regular file |  
| `d` | Directory |  
| `l` | Symbolic link |  
| `c` | Character device |  
| `b` | Block device |  
| `p` | Named pipe (FIFO) |  
| `s` | Socket |  
  
#### File Permissions  
  
The remaining nine characters are divided into three groups:  
  
```text  
-rwxr-xr--  
^^^ ^^^ ^^^  
Owner Group Others  
```  
  
Each group contains three permission bits:  
  
| *Symbol* | *Meaning* |  
|--------|---------|  
| `r` | Read permission |  
| `w` | Write permission |  
| `x` | Execute permission |  
| `-` | Permission not granted |  
  
### Example Breakdown  
  
```text  
-rwxr-xr--  
```  
  
- **Owner (`rwx`)** → Read, write, and execute.  
- **Group (`r-x`)** → Read and execute, but no write.  
- **Others (`r--`)** → Read only.