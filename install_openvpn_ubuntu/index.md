# OpenVPN magic on Ubuntu 22.04: A beginner's guide


**Do you want to protect your data online?** OpenVPN is the solution for you! Today, we will install OpenVPN on your Ubuntu 22.04 server and set up a secure VPN connection.
<!--more-->

## Install OpenVPN-Server
- First things first, we need to download script from: https://github.com/kienngd/openvpn-install \
 This script is actually a fork of another awesome script by **Nyr** (https://github.com/Nyr/openvpn-install). Big thanks to them for making our lives easier!
- Run script `openvpn-install.sh` under `root` user and follow the descriptions.\
This will be done in minutes.
- This script will:
    - Check and install requiremented-libs
    - Install on Ubuntu, Debian, AlmaLinux, Rocky Linux, CentOS and Fedora
    - Download and install `easy-rsa`
    - In case you want to use the newer version of easy-rsa, find and edit `easy_rsa_url=...` inside file `openvpn-install.sh`
    - Install OpenVPN-Server
    - Create some **firewall rules** (Create service **openvpn-iptables**)
    - Create the **first client**
    - Create a service: **openvpn-server@server**

## Using command
- **Uninstall**: Run script `openvpn-install.sh` under `root` user again and choose `3` remove openvpn.
- **Create a new client**: Run script then choose `1` or `5` then sent the **.ovpn** file to user.
- **Revoke an exsisting client**: Run script then choose `2` 

## Modify iptables rules to allow client access server's LAN network
- Maybe your server has a **LAN network** you **want to share** with devices connected to the VPN. To do this, you'll need to tweak some firewall rules. Don't worry, it's not that scary! Just follow these steps:
    - Open file `/etc/systemd/system/openvpn-iptables.service`
    - Imagine your VPN has a special IP address, like: `10.10.10.0`, and your LAN network has another, like `192.168.120.0`, There's also your server's public IP, like `123.123.123.123` (don't share this with anyone!).
    - Find the line that says something like `ExecStart=/usr/sbin/iptables -t nat -A POSTROUTING -s 10.10.10.0/24 ! -d 10.10.10.0/24 -j SNAT --to 123.123.123.123` and remove it (carefully, though!)
    - Add these lines:
        ```bash
            ExecStart=/usr/sbin/iptables -t nat -N OPENVPN_LAN_RULE
            ExecStart=/usr/sbin/iptables -t nat -A OPENVPN_LAN_RULE -d 10.10.10.0/24 -j RETURN
            ExecStart=/usr/sbin/iptables -t nat -A OPENVPN_LAN_RULE -d 192.168.120.0/24 -j SNAT --to-source 192.168.120.104
            ExecStart=/usr/sbin/iptables -t nat -A OPENVPN_LAN_RULE -d 192.168.120.0/24 -j RETURN
            ExecStart=/usr/sbin/iptables -t nat -A OPENVPN_LAN_RULE -j SNAT --to-source 123.123.123.123
            ExecStart=/usr/sbin/iptables -t nat -A POSTROUTING -s 10.10.10.0/24 -j OPENVPN_LAN_RULE
        ```
    - Find the line that says something like `ExecStop=/usr/sbin/iptables -t nat -D POSTROUTING -s 10.10.10.0/24 ! -d 10.10.10.0/24 -j SNAT --to 123.123.123.123` and remove it (carefully, though!)
    - Add this line: `ExecStop=/usr/sbin/iptables -t nat -D POSTROUTING -s 10.10.10.0/24 -j OPENVPN_LAN_RULE`
    - Update systemd: `sudo systemctl daemon-reload`
    - Restart service: `sudo systemctl restart openvpn-iptables`
