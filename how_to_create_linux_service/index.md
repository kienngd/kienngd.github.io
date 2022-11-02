# How to create a linux service


Hi, today we will learn how to create a linux service. I use Ubuntu 20.04 to test. Have fun!

##### Step 1: Create new service file
```
/etc/systemd/system/test_service.service
```
Example file content:
```ini
[Unit]
Description=Demo test service
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1
User=**root**
ExecStart=**COMMAND TO EXECUTE**

[Install]
WantedBy=multi-user.target
```
You can see the full service defination here: [Will be update](#)
<!--more-->
##### Step 2: Start service
```bash
sudo systemctl daemon-reload
sudo systemctl start test_service.service
```

##### Step 3: Enable service (so service will start with OS)
```bash
sudo systemctl enable test_service.service
```

##### Check service status
```bash
sudo systemctl status test_service.service
```

##### Stop service
```bash
sudo systemctl stop test_service.service
```
