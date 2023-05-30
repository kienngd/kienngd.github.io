# How To Use Screen Command In Linux: A Beginner’s Guide


<!--more-->
**How To Use Screen Command In Linux: A Beginner’s Guide**

Have you ever been frustrated when your **SSH connection drops** and your **command gets terminated**? If so, you need to learn about screen. 

Screen is a tool that lets you create multiple sessions on a single terminal. You can detach from a screen session and re-attach to it later, even from a different computer. This way, you can keep your commands running in the background without interruption. 

To use `screen`, you need to install it first. On Ubuntu, you can do this by typing `sudo apt install screen` in the terminal. Then, you can use screen with these basic operations and more:

- To create a new screen session, type `screen` in the terminal.
- To create a new screen session with a name, type `screen -S name` where name is the name you want to give to the session.
- To detach from the current screen session, press **Ctrl-A followed by D**, or type `screen -d`.
- To detach other users from a screen session, type `screen -D`.
- To exit and terminate the current screen session, press **Ctrl-A followed by K**, or type `exit`.
- To re-attach to a running screen session, type `screen -r` if there is only one session, or `screen -r name` if there are multiple sessions with names.
- To list all the screen sessions, type `screen -ls`.
- To switch between different screen sessions, press **Ctrl-A followed by N** for next **or P** for previous.
- To rename the current screen session, press **Ctrl-A followed by A**.
- To create a new window within the current screen session, press **Ctrl-A followed by C**.
- To switch between different windows within the current screen session, press **Ctrl-A followed by the window number** or **"** to see a list of windows.
- To see all options of this command, type `screen --help`

Screen is a powerful tool that can help you manage multiple processes and sessions on a single terminal. Explore its features and options and have fun!

**Tips**
- By default, the shortcut key to detach from a **screen session**  is **CTRL + A followed by D**. However, if you want to customize this shortcut key, you can create a file called **./.screenrc** with the contents `escape ^Bb`. Then you run command: `screen -S My-Screen -c .screenrc`. With this setup, you can now detach from a **screen session** by pressing **CTRL + B followed by D**.
