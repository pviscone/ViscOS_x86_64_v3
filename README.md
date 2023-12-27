This scripts are used to build the ISO of my custom version of Arch linux using the optimized CachyOS repo and settings.

Be aware that this will work only on CPU that support the x86_64_v3 set of instructions.

To check if your CPU supports it run the following

```bash
/lib/ld-linux-x86-64.so.2 --help
```

```bash
#Output


Subdirectories of glibc-hwcaps directories, in priority order:
  x86-64-v4
  x86-64-v3 (supported, searched)
  x86-64-v2 (supported, searched)


```

If the set of instruction is supported you will see (supported, seached) next to it.

If your CPU doesn't support it of if you want to use the v4 version you have to change the repos in the pacman.conf. (See the CachyOS wiki https://wiki.cachyos.org/ )

---

## Package list

Add the packages to install in the txt files in the /archiso/Packages folder or create a new txt files inside the folder.

You can add also  AUR packages, add them to the /archiso/Packages/AUR/aur.txt file 

#### Arch local repo

First run the script in ./archiso/Packages/AUR/aur_download.sh . It will build a local repo containing all the AUR packages.

Insert the absolute path of the local repo in ./archiso/pacman.conf

```
[AUR]
SigLevel = Optional TrustAll
Server = file:///path/to/repo
```

#### Services

TBD

# buildiso

buildiso is used to build CachyOS ISO.

#### Arguments

```
$ ./buildiso.sh -h
Usage: buildiso [options]
    -c                 Disable clean work dir
    -h                 This help
    -p <profile>       Buildset or profile [default: kde]
    -v                 Verbose output to log file, show profile detail (-q)
```

* Uses the same signature that normal repo and has no mirrors package to install.

`sudo pacman -Syy`

## Install necessary packages

`sudo pacman -S archiso mkinitcpio-archiso git squashfs-tools --needed`

Clone:\
`git clone https://github.com/cachyos/cachyos-live-iso.git cachyos-archiso`

`cd cachyos-archiso`

## Build

`sudo ./buildiso.sh -p kde -v`

## The iso appears at out folder

---

**Install selecting the option "offline installer"**
