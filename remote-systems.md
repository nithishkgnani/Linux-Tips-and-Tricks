[Back to Readme](README.md)

* [SSH](#ssh)
* [SCP](#scp)
* [VNC](#vnc)


## SSH

#### 1. Run multiple commands in one ssh command
- For running commands sequentially,
`ssh user@RemoteSystemIP "Command1 && Command2"`
- For running commands simultaneously,
`ssh user@RemoteSystemIP "Command1 & Command2"`

#### 2. Passwordless SSH
To prevent ssh from asking for password everytime you ssh to the remote terminal, use:
1. `ssh-keygen -t rsa -P ""` - This has to be done once in your local system
2. `sudo ssh-copy-id -i /root/.ssh/id_rsa.pub user@RemoteSystemIP` - Do this in your local system once each for every remote system you want to SSH into.

#### 3. WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
_Note: If you think your systems are under attack, this solution is not for you !_  
If you changed or reinstalled the OS on your remote system, it can still retain its IP address.
If you try to connect to it using SSH or try a file transfer using SCP, 
you will get an error as mentioned below:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:BBBBaaaacccccddddd12134jkfjgoetj888899jrmgg.
Please contact your system administrator.
Add correct host key in /home/usernam/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /home/username/.ssh/known_hosts:17
  remove with:
  ssh-keygen -f "/home/username/.ssh/known_hosts" -R "xx.xx.xx.xx"
ECDSA host key for xx.xx.xx.xx has changed and you have requested strict checking.
Host key verification failed.
```
To fix this issue, type in the terminal: 
`ssh-keygen -R <IP_ADDRESS>`  
replace <IP_ADDRESS> with the remote host's IP address.  
`-R hostname` Removes all keys belonging to hostname from a known_hosts file. This option is useful to delete hashed hosts.


## SCP

The Secure Copy Protocol, or SCP, is a file transfer network protocol used to move files between servers and hosts.  

* The basic command to move a file named _filename.txt_ is: `scp file_source_location file_destination_location`. Example:  
`scp Remote_Host_Username@<IP_ADDRESS>:/home/Remote_Host_Username/Desktop/filename.txt /home/My_Username/Documents/`  
 

* If the remote host's username is HOST1 and IP address is 192.168.1.123 and the file is in Desktop. 
My username is MY_NAME and I want to transfer the file into Documents, the command will be:  
`scp HOST1@192.168.1.123:/home/HOST1/Desktop/filename.txt /home/MY_NAME/Documents/`
* The same file transferred from my system to remote system:  
`scp /home/MY_NAME/Documents/filename.txt HOST1@192.168.1.123:/home/HOST1/Desktop/`


* To transfer all files of the same file extension, use asterisk followed by extension. 
Example to tranfer all python files in remote's Desktop to my Documents:  
`scp HOST1@192.168.1.123:/home/HOST1/Desktop/*.py /home/MY_NAME/Documents/`


* To transfer and entire directory, use the extension `-r` to indicate recursive copy.   
Say you want to copy the directory named _Folder_A_ in remote's Desktop to my Documents:  
`scp -r HOST1@192.168.1.123:/home/HOST1/Desktop/Folder_A /home/MY_NAME/Documents/`
'
* To transfer files at a much higher speed, use `scp -C` to enable compression


## VNC

> Details on how to access a Remote Desktop Server (via VNC) using the Remmina Desktop Client

Assume the two Ubuntu 18.04 systems - **sys1** (Desktop Server) and **sys2** (Desktop Client).

#### How to set up the Desktop Server (sys1)?

* Go to Settings > Sharing.
* Turn on the 'Sharing' toggle on top-right (switched off by default)
* Toggle on Screen Sharing (switched off by default) > enable 'Allow connections to control the screen'.
* Set the access options as per your use-case.

#### How to set up the Desktop Client (sys2)?

* After you have completed configuring the Desktop server follwing the above steps, open Remmina on your Desktop Client system (sys2).
* On the top-left, click on the 'plus' icon to create a new connection profile
* The mandatory fields that need to be filled.
  * Name - Give your desktop server a name
  * Protocol - Choose VNC (Virtual Network Computing)
  * Server - sys1's IP Address
  * Username - sys1's username
  * Password - sys1's password set while configuring sys1.
* Choose 'Color Depth' and 'Quality' as per your use-case.
* Click on 'Save and Connect'.

This should allow you to control sys1 using sys2 (via VNC) using Remmina Desktop Client Software.

[Back to Readme](README.md)
