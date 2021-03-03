---
title: Blog
---


## Pi Capsule Project
### 3rd of March 2021 / 03.02.21

On the 20th of February I released the first version of Pi Capsule Project, which is a Linux command line tool to configure a Pi Capsule: an AFP server, SMB server, and Wi-Fi network designed to replicate the functionality of an Apple Time Capsule using a Raspberry Pi with free and open-source software.

Up until that point I used a first generation Apple Time Capsule for those features which was working fine, but had issues mounting on Linux and more importantly, the power supply would stop working after a few months and I'd had to repair or replace it. Apple also stopped making the Time Capsule a few years ago, so even if I wanted to get a new version that might not have those issues, I couldn't.

This led me to look into setting up an alternative to the Time Capsule and I stumbled upon a few articles suggesting the use of a Raspberry Pi. I had one laying around that I wasn't using (in this case a Raspberry Pi 3b) so I thought I'd give it a try, and once I got everything setup (which takes some time since it's a low powered device), it actually worked pretty well!

I did however have one issue: the method I used for creating a Wi-Fi network (a bridged one, as I did with my Time Capsule) didn't seem to connect to Android devices properly. But I later found a solution for that, which is to use systemd for networking. This requires some additional setup but is now included in the latest version of Pi Capsule Project.

Since I'm happy with my Pi Capsule, this being my first project entirely for Linux, and my Time Capsule not being reliable anymore, I decided to put it up for sale and switch to using my Pi Capsule only. 

If you still have a Time Capsule though, and you want to mount it on Linux, you can use [this script](https://gist.github.com/julian-fairfax/e9d95a76e3b94e8db492262332d567eb)

Make sure to replace these values before running the script:
```
time-capsule.local should be replaced with the IP address of your Time Capsule which you can find in AirPort Utility
/Time Capsule should be replaced with the name of your volume (following the /) which you can find in AirPort Utility
timecapsule should be replaced with the password of your Time Capsule's disk which you can set in AirPort Utlity
```