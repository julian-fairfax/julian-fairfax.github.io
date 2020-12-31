---
title: Blog
---


## Fixing proprietary graphics drivers on Linux with systemd-boot
### 20.12.20

If you use Linux on a computer with a certain company's graphics card, you may notice that the open source graphics drivers don't work properly and might try installing the proprietary graphics drivers. Unfortunately, you're likely to run into problems if you don't do some steps before installation. 

Some Linux distributions use systemd-boot which requires following different steps.

I've had this problem when running Linux on my MacBook7,1 (this is most likely not going to be a problem for you if you have a newer computer) and I've [created a script](https://gist.github.com/julian-fairfax/752f6f5fc9786b7c41ea08920800f788) to fix the proprietary drivers. It's important to run the script before you install the drivers, as not doing so could result in your computer not booting.

This script is based on [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1910114#p1910114) for fixing the computer not booting:
```
sudo wget -O /boot/efi/shellx64.efi https://github.com/tianocore/edk2/blob/UDK2018/EdkShellBinPkg/FullShell/X64/Shell_Full.efi
echo "mm 02000004 1 ;PCI :7
mm 0017003E 1 ;PCI :8

for %i run (0 9)
  if exist fs%i:\EFI\<UUID_ROOT>\vmlinuz.efi then
    fs%i:\EFI\<UUID_ROOT>\vmlinuz.efi root=<INDENTIFER_ROOT> rw initrd=\EFI\<UUID_ROOT>\initrd.img
  endif
endfor" | sudo tee /boot/efi/startup.nsh

sudo efibootmgr --create --disk <INDENTIFER_DISK> --loader shellx64.efi --label "EFI Shell"
sudo efibootmgr -o $(efibootmgr | grep "EFI Shell" | sed 's/Boot//'| sed 's/\*.*//')
```

Make sure to replace these values before running the script:  
```
<UUID_ROOT> should be replaced with the UUID of your root parition which can be found by running blkid
<INDENTIFER_ROOT> should be replaced with the indentifier of your root partition which be found by running lsblk
<INDENTIFER_DISK> should be replaced with the indentifier of your disk which can be found by running lsblk
```

Written by Julian Fairfax