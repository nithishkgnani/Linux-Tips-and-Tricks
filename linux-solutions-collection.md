[Back to Readme](README.md)

* [Terminal commands for general information](#terminal-commands-for-general-information)
* [Terminal commands for simple tasks](#terminal-commands-for-simple-tasks)
* [Solutions](#solutions)
* [Tips and Tricks](#tips-and-tricks)
* [Useful Links](#useful-links)

## Terminal commands for general information 

* Check os version in Linux  
`cat /etc/os-release`
* Find Linux kernel version  
`uname -r`


## Terminal commands for doing various tasks

* To make files like .bin file into executable.  
`chmod +x filename.extention`  
Then you can run it using ./filename.bin

* To find a particular word or string inside the files of a directory
```bash
grep -rni "example string" /path/directory_name/
```

### Finding and stopping processes
* Finding process id of a running software.  
`pidof <software-name>`  
Example command for finding process id of VS-Code software: `pidof code`  
_Note:_ One software can return multiple process ids
* To kill a process or multiple processes using their process ids:  
`sudo kill -9 process-id-1 process-id-2 process-id-3 process-id-n`
* To kill all processes of a software:  
`sudo kill -9 'pidof <software-name>'`  
or  
`killall software-name`

### Search tips
* To find the locations of any file    
`locate <filename>`
* To find all the instances of a given string/keyword in all the directories  
`grep -Hrni <string/keyword>`
* To find all the instances of a given string/keyword in the current directory  
`grep -Hrni <string/keyword> . `

* Options explained: -Hrni
  * -H: print the filename for each match
  * -r: recursively search subdirectories listed
  * -n: print the line number for each match
  * -i: ignore case
* For more info on grep, type `man grep` in the terminal.


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

#### Linux Mint - terminal shows asterisks while typing password
Can be solved by disabling password feedback. Enter the above line in the terminal to stop showing asterisks while typing passwords in Linux Mint.   
` echo 'Defaults !pwfeedback'|sudo tee /etc/sudoers.d/9_no_pwfeedback `  

#### Error: Failed to take /etc/passwd lock: Invalid argument
I faced this error while trying to install a package using apt-get in Windows Subsystem for Linux (WSL).
```bash
Failed to take /etc/passwd lock: Invalid argument
dpkg: error processing package systemd (--configure):
 installed systemd package post-installation script subprocess returned error exit status 1
Errors were encountered while processing:
 systemd
E: Sub-process /usr/bin/dpkg returned an error code (1)
```
Solution:
```bash
sudo mv /var/lib/dpkg/info /var/lib/dpkg/info_silent
sudo mkdir /var/lib/dpkg/info
sudo apt-get update
sudo apt-get -f install
sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info_silent
sudo rm -rf /var/lib/dpkg/info
sudo mv /var/lib/dpkg/info_silent /var/lib/dpkg/info
sudo apt-get update
sudo apt-get upgrade
```
[Source](https://superuser.com/a/1804301)


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

[Back to Readme](README.md)

## Useful links
* [Linux Mint - 45 Tips and Tweaks](https://easylinuxtipsproject.blogspot.com/p/tips-1.html#ID15)
