### tp-link USB500 Bluetooth dongle not working in Ubuntu 20.04
I followed the following answer: https://askubuntu.com/a/1435285. It is reproduced below in case that answer is deleted.

---
I was able to connect my UB500 on Ubuntu 20.04.
After running `sudo dmesg | grep -i bluetooth` I noticed the following firmware file was missing:
```
Bluetooth RTL: firmware file rtl_bt/rtl8761bu_fw.bin not found 
```
**My solution:**
Copy the rtl8761b_fw firmware:
```
cp /usr/lib/firmware/rtl_bt/rtl8761b_fw.bin /usr/lib/firmware/rtl_bt/rtl8761bu_fw.bin
cp /usr/lib/firmware/rtl_bt/rtl8761b_config.bin /usr/lib/firmware/rtl_bt/rtl8761bu_config.bin
```
Run modprobe:
```
sudo modprobe btusb
```
Restart the bluetooth service:
```
sudo systemctl restart bluetooth.service
```
Then re-plug the bluetooth dongle.

---
