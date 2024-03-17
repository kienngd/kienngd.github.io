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
