# Archived and No longer maintained. 

Due to the constant updates and time it takes to maintain this script I will no longer be updating it. Free free to fork it and take what you want from here. There has been some fantastic contributions over the past year and I learned a lot while making this project. 

Thank you!

# ArchTitus Installer Script
[![GitHub Super-Linter](https://github.com/ChrisTitusTech/ArchTitus/workflows/Lint%20Code%20Base/badge.svg)](https://github.com/marketplace/actions/super-linter)

<img src="https://i.imgur.com/YiNMnan.png" />

This README contains the steps I do to install and configure a fully-functional Arch Linux installation containing a desktop environment, all the support packages (network, bluetooth, audio, printers, etc.), along with all my preferred applications and utilities. The shell scripts in this repo allow the entire process to be automated.)

---
## Create Arch ISO or Use Image

Download ArchISO from <https://archlinux.org/download/> and put on a USB drive with [Etcher](https://www.balena.io/etcher/), [Ventoy](https://www.ventoy.net/en/index.html), or [Rufus](https://rufus.ie/en/)

If you don't want to build using this script I did create an image @ <https://cttstore.com/arch-titus>

## Boot Arch ISO

From initial Prompt type the following commands:

This will set keyboard layout to Italian
```
loadkeys it
```
From the initial prompt, type the following commands after waiting a few seconds (as explained [here](#error-keyring-is-not-writable)):

```bash
pacman -Sy git
git clone https://github.com/Jiozza/ArchJiozza
cd ArchJiozza
./archjiozza.sh
```

### System Description
This is completely automated arch install. It includes prompts to select your desired desktop environment, window manager, AUR helper, and whether to do a full or minimal install. The KDE desktop environment on arch includes all the packages I use on a daily basis, as well as some customizations.

## Troubleshooting

__[Arch Linux RickEllis Installation Guide](https://github.com/rickellis/Arch-Linux-Install-Guide)__

__[Arch Linux Wiki Installation Guide](https://wiki.archlinux.org/title/Installation_guide)__

The main script will generate .log files for every script that is run as part of the installation process. These log files contain the terminal output so you can review any warnings or errors that occurred during installation and aid in troubleshooting. 


### No Wifi

You can check if the WiFi is blocked by running `rfkill list`.
If it says **Soft blocked: yes**, then run `rfkill unblock wifi`

After unblocking the WiFi, you can connect to it. Go through these 5 steps:

#1: Run `iwctl`

#2: Run `device list`, and find your device name.

#3: Run `station [device name] scan`

#4: Run `station [device name] get-networks`

#5: Find your network, and run `station [device name] connect [network name]`, enter your password and run `exit`. You can test if you have internet connection by running `ping google.com`, and then Press Ctrl and C to stop the ping test.

### **error: keyring is not writable**
If you get this error when installing git:
```
downloading required keys...
error: keyring is not writable
error: required key missing from keyring
error: failed to commit transaction (unexpected error)
Errors occurred, no packages were upgraded.
```
Reboot the ISO and wait at least 15 seconds before installing git. \
When starting the Arch ISO, it will update the keyring and trust database in the background. \
You can run `journalctl -f` and wait until it says something like **next trustdb check due at 2022-05-6** and **Finished Initializes Pacman keyring**.


### **Script failing constantly**
If the script fails multiple times, try to remove `install.conf` and run the script again.

### **Timezone won't get detected**
Make sure the domains `ipapi.co` and `ifconfig.co` don't get blocked by your firewall.

---
## Credits
- Forked from ChrisTitusTech
- Original packages script was a post install cleanup script called ArchMatic located here:\
https://github.com/rickellis/ArchMatic \
https://github.com/rickellis/Arch-Linux-Install-Guide
