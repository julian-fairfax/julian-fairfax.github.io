---
title: Blog
---


## Uniform look for Qt applications in GTK
### 10th of March 2021 / 10.02.21

Applications that use the Qt toolkit use different themes than applications that use the GTK toolkit and than a GTK desktop environment. This post will help you get a uniform look for your Qt applications in a GTK desktop environment. You can run [this script](https://gist.github.com/julian-fairfax/3703b14ea8f819852f55ac4988848c39) or follow the instructions below.

First you need to install QGtkStyle which can be done by running the following command:
```
sudo apt install qt5-style-plugins
```

Next you'll need to configure QGtkStyle to use your GTK theme in Qt applications by running the following commands:
```
if [[ ! -d ~/.config/environment.d ]]; then
    mkdir -p ~/.config/environment.d
fi

echo "[Qt]
style=GTK+" | tee -a ~/.config/Trolltech.conf

echo "QT_QPA_PLATFORMTHEME=gtk2
QT_STYLE_OVERRIDE=gtk2" | tee -a ~/.config/environment.d/envvars.conf
```