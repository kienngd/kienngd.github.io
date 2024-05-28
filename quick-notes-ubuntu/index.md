# 🚧 Quick-notes working with Ubuntu


<!--more-->
# Some Quick-notes

<font color="#0000FF">These notes will be moved to another place soon</font>

## Using sshfs to mount remote-folder to local
Test with ubuntu 22.04
```bash
# Install
sudo apt install sshfs

# Show help message
sshfs --help

# Mount from folder /data from remote-server to folder /mnt/data at local-server
sshfs USER@SERVER:/data /mnt/data -o reconnect,ServerAliveInterval=15,ServerAliveCountMax=3 ...

# Unmount
fusermount -u /mnt/data
```

---

## Run Swagger Editor docker
- Document link: https://github.com/swagger-api/swagger-editor
- Command
```bash
docker pull swaggerapi/swagger-editor
docker run -d -p 80:8080 swaggerapi/swagger-editor
```

---

## Install LUbuntu 24.04 notes
### Install
  - Download LUbuntu ISO from offical site.
  - Use tool `Start Disk Creator` to make bootable-usb
  - Start PC from USB, then follow the instructions.
  
### After install
  - **Auto-mount 2nd hdd**
    - Run `sudo blkid` to get `UUID` of partitions
    - Edit `/etc/fstab`\
    Add:
      ```
      UUID=... /mount-point              ext4    discard    0 0    
      ```
    -  Reload: 
        ```
        systemctl daemon-reload
        ```
  - Install net-tools
      `sudo apt install net-tools`
