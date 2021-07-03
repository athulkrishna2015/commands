# onedrive

` rclone --vfs-cache-mode writes mount onedrive: <path> --allow-non-empty `   to mount ondedrive with 

`rclone --vfs-cache-mode writes mount onedrive: ~/onedrive` 

to mount at startup

create  `/home/$(USER)/.onedive.sh` give excute permission 
```
#!/bin/sh
sleep 3
rclone --vfs-cache-mode writes mount onedrive: ~/onedrive
```
add `sh /home/$(USER)/.onedive.sh` to start up application  
