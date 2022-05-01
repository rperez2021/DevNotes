---
id: lejkqveywayfggf8ln0tt34
title: File Structure
desc: 'General Notes on Standard Unix File Structure'
updated: 1651382447687
created: 1651380958660
---
## /bin (Binary) and /sbin (System Binary)

Binary folders stuff like `ls` `cat`

`/sbin` is for system binaries

## /boot (Boot Folder)

Boot files go here (ex Grub)

## /cdrom (CDROM Folder)

A legacy mounting folder for cdrom not used very often.

## /dev (Devices Folder)

Remember that in Unix everything is a file. This includes stuff like your hard drives (and their partitions), mouse, keyboard, etc.

## /etc (Etcetera Folder)

Some people call it the edit to configure folder.

This is where all the configs are stored for system wide applications (like `apt`)

## /lib /lib32 /lib64 (Library Folders)

Files that give added functionality and can be shared by programs.

## /mnt (Mount Folder) /media (External Media)

This is where you would find other mounted drives, external drives, usb sticks, sdcards.

Most external store will be automatically installed to media.

If you need to install something manually mount it in the `/mnt` folder

## /opt (Optional Folder)

User installed software. A good place to also place user developed software.

## /proc (Process Folder)

Folder containing all the processes that the system is running and is sorted by their `pid`

## /root (Root User Folder)

Pretty self explanatory

## /run

Newer folder not in all distros, files here are generally stored in ram and gets wiped on reboot.

## /snap (Snap Package Folder)

Snaps are self-contained packages that work across a range of Linux distributions. This is unlike traditional Linux package management approaches, which require specifically adapted packages for each Linux distribution.

## /srv (Service Folder)

If you run a webserver, accessed files will be found here.

## /sys (System Folder)

A way to interact with the kernel, this directory is similar to the run directory and is created every time if boots up.

## /tmp (Temporary Folder)

Temporary files, usually emptied during reboot

## /usr

User Application Space, stuff that is installed that is only used by users.

Also known as Unix System Resource which means non essential applications

Also has child `/bin /sbin /etc /src /lib` subfolders

## /var

Variable directory, contains files and directories that are expected to grow in size.

## /home

Personal files and documents sorted by users. Also contained theme config files.
