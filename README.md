# Linux-Tips-and-Tricks
A collection of tips, tricks, solutions, hacks that may or may not be found online. 

Raspberry Pi
===
Connecting to Enterprise Wi-Fi in Raspberry Pi
---
In Raspberry Pi, the WiFi options are grayed out for University/company networks unlike home networks. This is due to the enterprise WPA protection. There are many solutions in the internet that require modifying the wpa_supplicant configuration manually and similar, but this is pretty complex, hard to get right and inflexible when the configuration changes. The "greyed out" issue is because the PIXEL desktop in Raspbian comes with its own simple network managing service that does not support more complex WiFi setups used in enterprise and university networks (especially eduroam).

There is a simple way to fix this though: Instead of the Raspbian integrated one you use NetworkManager, which is what's used in most Desktop Linux environments.
* `sudo apt install network-manager network-manager-gnome`
* `sudo systemctl disable --now dhcpcd`
* `sudo systemctl enable --now network-manager`

* `nm-apple` # to show the tray icon without reboot

Now check the network options in system tray.
<br />[Source](https://raspberrypi.stackexchange.com/a/119653)
