## SSH

#### WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
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
