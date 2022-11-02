# How to connect to a service on the remote server via SSH tunnel

Hello, today we will talk about connecting to a remote service via SSH tunnel. I use Ubuntu 20.04 to test. Have fun!

Imagine that you have a MySQL server listen on port 3306. For security reasons, your firewall denies port 3306 from the internet. And you have a SSH account to connect to your server. Normally you can SSH to the server then use mysql client console to interact with the database.

But sometimes you want to connect to a database using a third party application (Example navicat or DBeaver...). In these cases you can create a SSH tunnel then connect via tunnel.


**<u>Option 1</u>**: Command line
Create tunnel
```bash
ssh -p[SERVER_SSH_PORT] -L [LOCAL_PORT_TO_LISTEN]:[LOCAL_ADDRESS_TO_LISTEN]:[SERVER_PORT_TO_FORWARD] [SERVER_USER_NAME]@[SERVER_IP]
```
**Example**:
```bash
ssh -p22 -L 3307:127.0.0.1:3306 test@192.168.11.204
```
<!--more-->
Then you can connect to database
```bash
mysql -P3307 -uroot -p -h127.0.0.1
```

**<u>Option 2</u>**: Use DBeaver

When you create or edit a connection, you can create a tunnel

**Create tunnel**

![ssh_tunnel_01](/images/ssh_tunnel_01.png)

**Create connection**

![ssh_tunnel_02](/images/ssh_tunnel_02.png)

Thank you for reading. Further information from ssh manual:
```bash
man ssh
```
![ssh_tunnel_03](/images/ssh_tunnel_03.png)
