# Code-Server code in your browser

Hello, it is me again. Today, we will talk about **Code-Server** an "in browser vs code IDE". I use Ubuntu 20.04 to test. Have fun!

1. Download **Code-Server** from github page: https://github.com/coder/code-server/releases ~~https://github.com/cdr/code-server/releases/~~
    - You can download **rpm** or **deb** file or **tar.gz** file :).
2. If you download rpm or deb, use PMS of your OS to install it. I download file **tar.gz** so I just **untar** it to an folder.
<!--more-->
3. Run server

    Go to **code-server folder** and run command to show all options
    ```bash
        ./code-server --help
    ```

    Run command and show output in console

    ```bash
        ./code-server --auth=password
    ```
    Default config file is: **~/.config/code-server/config.yaml**
    
    Open your browser, try access: http://localhost:2704 (please change to your port) and enjoy.

4. You can create service to manage: [how to create linux service](/howto/how_to_create_linux_service/)

Happy Coding.

