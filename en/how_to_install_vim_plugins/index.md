# How to install VIM plugins


Hello, today we will to learn 2 of many ways to install and use VIM plugins. I use Ubuntu 20.04 to test. Have fun!

If you want to install plugin named **nerdtree**, 

1st way: Copy plugin files to: **~/.vim/pack/vendor/start** and they will be load when you launch VIM

Example:
```bash
cp -r nerdtree ~/.vim/pack/vendor/start/
```
Then inside VIM, you can use command: **:NERDTree**
<!--more-->
2nd way: Copy plugin files to: **~/.vim/pack/vendor/opt** and they will be not load until you use command **packadd** to load it.

Example:
```bash
cp -r nerdtree ~/.vim/pack/vendor/opt/
```
Then inside VIM, you can use command: **packadd nerdtree** to load the plugin. Then you can use command **:NERDTree**

