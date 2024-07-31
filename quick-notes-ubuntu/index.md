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

## Supervisor commands
```bash
  # After change your config file, run these commands
  supervisorctl reread
  supervisorctl update

  # Restart some process
  supervisorctl restart SUPERVISOR-PROGRAM-NAME
```

## Change route metric
- Problem: ???
- Edit file `vi /etc/netplan/50-cloud-init.yaml`
- Find your interface. Example `ens3`. Add these lines
  ```yml
    dhcp4-overrides:
      route-metric: 150 # This will change metric to 150.
  ```
- Apply change: `sudo netplan apply`

---

## Change network metric of docker network and disable log
- Problem: ???
- Edit file: `/etc/docker/daemon.json`
- Add these lines:
  ```json
    "mtu":1450,
    "log-driver": "none"
  ```

---

<!-- ## Run Swagger Editor docker
- Document link: https://github.com/swagger-api/swagger-editor
- Command
```bash
docker pull swaggerapi/swagger-editor
docker run -d -p 80:8080 swaggerapi/swagger-editor
```

--- -->

<!-- ## Install LUbuntu 24.04 notes
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

--- -->

## Install Ubuntu 24.04 notes
### Install
  - Download Ubuntu ISO from offical site.
  - Use tool `Start Disk Creator` to make bootable-usb
  - Start PC from USB, then follow the instructions.

### After Install

- Install keepass2 mate-terminal net-tools ibus-unikey gimp ttf-mscorefonts-installer ubuntu-restricted-extras imagemagick
  ```bash
    sudo apt install keepass2 mate-terminal net-tools ibus-unikey gimp ttf-mscorefonts-installer ubuntu-restricted-extras imagemagick
  ```

- Install driver for usbwifi
  ```bash
    cd /hdd/data/softs/rtl8812au/
    git pull origin v5.6.4.2
    sudo apt install build-essential dkms
    sudo make dkms_install
  ```

- Install VPN
  - Get file ovpn from vpn server.
  - Import ovpn file.
  - Connect.


- Change geany default font

- Set Shortcut key for main menu is: Meta (super, window, Microsoft)

- Vietnamese keyboard: `gnome-control-center --> keyboard --> input sources --> add input sources`

- Install docker
  ```bash
    ## Add Docker's official GPG key:
    sudo apt update
    sudo apt install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    ## Add the repository to Apt sources:
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    sudo apt-get update
    sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    sudo usermod -aG docker kiennd ## Change kiennd to your real username
  ```

- Install vscode
  - Download file .deb from microsoft site
  - sudo dpkg -i ....

- Set git parrams
  ```bash
    git config --global user.email "kienngd@gmail.com"
    git config --global user.name "Kien Nguyen"
  ```

- Install drawio
	- wget https://github.com/jgraph/drawio-desktop/releases/download/v24.2.5/drawio-amd64-24.2.5.deb
	- sudo dpkg -i drawio-amd64-24.2.5.deb

- Install Github-Desktop
  ```bash
    wget https://github.com/shiftkey/desktop/releases/download/release-3.3.12-linux2/GitHubDesktop-linux-amd64-3.3.12-linux2.deb  ## Remember to check the newest version
    sudo dpkg -i GitHubDesktop-linux-amd64-3.3.12-linux2.deb
  ```

- Install Google chrome
	- Download file deb from google
	- `sudo dpkg -i google-chrome-stable_current_amd64.deb`

- Set alias: `~/.bash_aliases`

- Config ssl: 


- Auto-mount 2nd ddd
	- Edit file `/etc/fstab`

	  `UUID=... /mount-point              ext4    discard    0 0`

	- `systemctl daemon-reload`

---

