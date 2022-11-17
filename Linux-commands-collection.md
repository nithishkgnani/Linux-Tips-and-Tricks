


## Terminal commands for general information 

* Check os version in Linux  
`cat /etc/os-release`
* Find Linux kernel version  
`uname -r`


## Terminal commands for simple tasks

* To make files like .bin file into executable.  
`chmod +x filename.extention`  
Then you can run it using ./filename.bin




## Solutions 
#### Ubuntu update error: "waiting for unattended-upgr to exit"
1. Stop the automatic updater  
`sudo dpkg-reconfigure -plow unattended-upgrades`  
At the first prompt, choose not to download and install updates.  
Do a reboot.
2. Make sure any packages in an unclean state are installed correctly.  
  `sudo dpkg --configure -a`
3. Get your system up-top-date.  
  `sudo apt update && sudo apt -f install && sudo apt full-upgrade`
4. Turn the automatic updater back on, now that the blockage is cleared.  
  `sudo dpkg-reconfigure -plow unattended-upgrades`  
    Select the package unattended-upgrades again.  
[Source](https://unix.stackexchange.com/questions/374748/ubuntu-update-error-waiting-for-unattended-upgr-to-exit) 

#### Ubuntu Software: Unable to install "_PACKAGE_": snap "_PACKAGE_" has "install-snap" change in progress
Snap is probably still working on something in the background (or at least it thinks so). 
Open a terminal and run `snap changes` so see a list of ongoing changes.

    $ snap changes
    ID   Status  Spawn               Ready  Summary
    ...
    110  Doing   today at 13:09 IST  -      Install "code" snap from "latest/stable" channel
    ...

You can abort ongoing change(s):

    sudo snap abort 110

Then you should be able to successfully install the package through the software center, or through the command line using `snap install PACKAGE_NAME`.  
[Source](https://askubuntu.com/a/1029123)

## Tips and Tricks

#### Tell GRUB to reboot into Windows only for the next reboot  
In a dual boot system, if you want to reboot to Windows from Ubuntu terminal just once 
instead of permanently altering the boot order, do the following steps:  
1. Edit the /etc/default/grub and replace `GRUB_DEFAULT=0` with `GRUB_DEFAULT=saved`
2. `sudo update-grub`
3. Your command for one time reboot to Windows will be:

      `sudo grub-reboot "$(grep -i windows /boot/grub/grub.cfg|cut -d"'" -f2)" && sudo reboot`
  
To make it a function that can be called to do the same: 
Edit `~/.bashrc` using any editor and add the following lines at the bottom and source it:

    # Reboot directly to Windows
    # Inspired by http://askubuntu.com/questions/18170/how-to-reboot-into-windows-from-ubuntu
    reboot_to_windows ()
    {
        windows_title=$(grep -i windows /boot/grub/grub.cfg | cut -d "'" -f 2)
        sudo grub-reboot "$windows_title" && sudo reboot
    }
    alias reboot-to-windows='reboot_to_windows'

**Now you can reboot to Windows one time by typing `reboot-to-windows`  on a terminal.**

In case, your grub.conf contains multiple lines for Windows, following functions will take care only about lines starting by `menuentry` and picking just the first one, referring to Windows:

    function my_reboot_to_windows {
        WINDOWS_TITLE=`grep -i "^menuentry 'Windows" /boot/grub/grub.cfg|head -n 1|cut -d"'" -f2`
        sudo grub-reboot "$WINDOWS_TITLE"
        sudo reboot
    }

[Source](https://unix.stackexchange.com/questions/43196/how-can-i-tell-grub-i-want-to-reboot-into-windows-before-i-reboot/112284#112284)

