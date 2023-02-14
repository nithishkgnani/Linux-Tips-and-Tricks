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
