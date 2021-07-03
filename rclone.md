` rclone --vfs-cache-mode writes mount onedrive: <path> --allow-non-empty `   to mount ondedrive with 

`rclone --vfs-cache-mode writes mount onedrive: ~/onedrive` 

to mount

start up `sh /home/$(USER)/.onedive.sh`


```
#!/bin/sh
sleep 3
rclone --vfs-cache-mode writes mount onedrive: ~/onedrive
```
