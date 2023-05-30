# How to Connect to a Server via SSH Without Password Authentication


<!--more-->
**SSH key authentication** is a convenient and secure way to connect to remote servers without having to enter a password every time. In this tutorial, I will show you how to set up SSH key authentication on your server.

**Step 1**: Generate an SSH key pair
The first step is to generate an SSH key pair on your local computer. Open the terminal and run the following command:
```
ssh-keygen
```
By default, the key pair will be saved in the `~/.ssh` directory with the names `id_rsa` (private key) and `id_rsa.pub` (public key).

**Step 2**: Copy the public key to the server
Next, you need to copy the contents of the public key to the server's authorized_keys file. To do this, run the following command:
```bash
cat ~/.ssh/id_rsa.pub | ssh user@server 'cat >> ~/.ssh/authorized_keys'
```
Replace `user` with your username on the server, and `server` with the IP address or hostname of the server.

If you saved your key pair with a different name, use the `-i` option to specify the path to your private key:
```bash
cat ~/.ssh/my_key.pub | ssh user@server -i ~/.ssh/my_key 'cat >> ~/.ssh/authorized_keys'
```
**Step 3**: Test the SSH connection
Now that the public key is installed on the server, you should be able to connect without entering a password. To test this, run the following command:
```bash
ssh user@server
```
If you saved your key pair with a different name, use the `-i` option to specify the path to your private key:
```bash
ssh -i path/to/my_key user@server
```
If everything is set up correctly, you should now be logged in to the server without being prompted for a password.

In conclusion, using SSH key authentication can help improve security and save time by eliminating the need to enter passwords each time you log in to your server.
