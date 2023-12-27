These scripts are used to build the ISO of my custom version of Arch Linux using the optimized CachyOS repo and settings.\
For more detailed info look at the [Arch Wiki archiso page](https://wiki.archlinux.org/title/archiso) 

Be aware that this will work only on CPUs that support the x86_64_v3 set of instructions.\
(The first CPUs that support it were built in 2014/2015 (Intel Haswell 4th generation))

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

If the set of instruction is supported you will see (supported, searched) next to it.

If your CPU doesn't support it or if you want to use the v4 version, you have to change the repos in the pacman.conf. (See the CachyOS wiki https://wiki.cachyos.org/ )

---

## Package list

Add the packages to install in the txt files in the /archiso/Packages folder or create a new txt file inside the folder.

You can also add  AUR packages, add them to the /archiso/Packages/AUR/aur.txt file 

#### AUR local repo

First, run the script in ./archiso/Packages/AUR/aur_download.sh. It will build a local repo containing all the AUR packages.

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
`git clone https://github.com/pviscone/ViscOS_x86_64_v3.git`

`cd ViscOS_x86_64_v3`

## Build

`sudo ./buildiso.sh -v`

## The iso appears in the out folder

---

**Boot and install by selecting the option "offline installer"**
