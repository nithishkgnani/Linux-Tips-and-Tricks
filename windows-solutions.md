### The device is currently in use 

While trying to safely remove external HDD, if you get "the device is currently in use" prompt even though you have closed all files and programs, fix it using diskpart:
1. Open command prompt in admin mode and enter the following commands
2. `diskpart`
3. `list disk`
4. select the external hdd using select  
   `select disk 2`  
    change 2 to the disk number of the external HDD
5. `offline disk`
6. This makes the **disk go offline**. Now you should be able to click on safely remove and it will work.

When you re-connect the same disk, it needs to be **made online again**. Use Disk Management for that.
1. Open Disk-Management by typing diskmgmt.msc in Run or by right clicking on the start button and selecting it.
2. Right click on the external HDD at the bottom of the window and slect online.

### Cloning HDD to SSD
To clone disks so that you can move the OS and all files to a new disk, and use it as a new cloned system:  
Use the free software called `DiskGenius`. It can also handle cloning from a larger disk to a smaller disk (Do not have data more than the smaller disk size though).  
1. Go to Tools > Clone Disk. Select the source disk.  
2. `Yes` to Migrate System
3. Select the target (destination) disk.
4. Click on Start. It will take a while to complete.
Done

### Deleting an OEM partition
The Windows Disk Management tool does not let one delete the OEM partition. So, you can use the command line tool called "Diskpart".  
Warning - Proceed at your own risk:
* Open the Run prompt, type `diskpart`, and hit Enter.
* Type, and enter `list disk` to list the disks.
* Select the disk you want to manage – say it is Disk Z, where 'Z' is the disk number.
* Then type `select disk z` and hit Enter.
* Enter `list partition` and hit Enter to display all the volumes.
* Type `select partition x` and hit Enter. Here 'x' stands for the partition you want to delete.
* Finally, type `delete partition override` and hit Enter to delete it.