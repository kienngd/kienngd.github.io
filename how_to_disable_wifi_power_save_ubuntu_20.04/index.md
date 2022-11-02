# How to disable wifi power save Ubuntu 20.04

Hello, today I've installed new Ubuntu 20.04. Then I get the wifi problem. When system start, the wifi works fine. But a few moment later, it was dropped so I cannot connect to the internet. I disable wifi, then enable wifi, it works fine for some minutes and fall into problem again.

I see [this link](https://unix.stackexchange.com/questions/269661/how-to-turn-off-wireless-power-management-permanently) and try to edit file */etc/NetworkManager/conf.d/default-wifi-powersave-on.conf* change **wifi.powersave** from 3 (enable power save) to 2 (disable power save). And reboot. Now the wifi works fine.
<!--more-->
