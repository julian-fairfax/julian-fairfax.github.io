---
title: Blog
---


## Fixing proprietary graphics drivers on Linux
### 20.12.20

If you use Linux on a computer with a certain company's graphics card, you may notice that the open source graphics drivers don't work properly and might try installing the proprietary graphics drivers. Unfortunately, you're likely to run into problems if you don't do some steps before installation.

I've had this problem when running Linux on my MacBook7,1 (this is most likely not going to be a problem for you if you have a newer computer) and I've [created a script](https://gist.github.com/julian-fairfax/f6867255fa695231c34c7da40614ac83) to fix the proprietary drivers. It's important to run the script before you install the drivers, as not doing so could result in your computer not booting.

This script is based on [this thread](https://askubuntu.com/questions/264247/proprietary-nvidia-drivers-with-efi-on-mac-to-prevent-overheating) for fixing the computer not booting:
```
echo "cat << EOF
setpci -s "00:17.0" 3e.b=8
setpci -s "02:00.0" 04.b=7
EOF" | sudo tee /etc/grub.d/01_enable_vga.conf

sudo chmod 755 /etc/grub.d/01_enable_vga.conf
sudo update-grub
```

And [this thread](https://askubuntu.com/questions/76081/brightness-not-working-after-installing-nvidia-driver) for fixing the brightness not working:
```
echo 'Section "Device"
    Identifier     "Device0"
    Option         "RegistryDwords" "EnableBrightnessControl=1"
EndSection' | sudo tee /usr/share/X11/xorg.conf.d/10-brightness.conf
```


I also added this code to not show the certain company's logo on boot:
```
echo 'Section "Screen"
    Identifier     "Screen0"
    Option         "NoLogo" "True"
EndSection' | sudo tee /usr/share/X11/xorg.conf.d/10-nologo.conf
```

Written by Julian Fairfax