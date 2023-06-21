---
title: Use GUI in WSL2
categories:
  - windows
---
1.Using XRDP and xfce4

In wsl
```shell
// install xfce4 desktop
sudo apt-get install -y xfce4 xfce4-goodies

// install and start xrdp
sudo apt install xrdp -y
sudo service xrdp start

// verbose operation for port conflict
// change default port 3389 to other e.g. 3390
vim /etc/xrdp/xrdp.ini

// or
sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak  
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini  
sudo sed -i 's/max_bpp=32/#max_bpp=32\nmax_bpp=128/g' /etc/xrdp/xrdp.ini  
sudo sed -i 's/xserverbpp=24/#xserverbpp=24\nxserverbpp=128/g' /etc/xrdp/xrdp.ini

// manual restart xrdp
sudo /etc/init.d/xrdp start
```


Then lanch rdp client in windows and the target ip will be the eth0 address in wsl

Note that if you don't setup any user in the begining the org(from rdp) authentication will fail,
switch to windows terminal and  `wsl adduser <username>`  to set one and login again.


2.Microsoft recommended solution:

Follow the instruction:
https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps

you may get  “Failed to connect to the bus:"  Error, set the environment variable and it should work.

```bash
export LIBGL_ALWAYS_INDIRECT=1
export DISPLAY=:0
```

Another common error you might get is "# Error: Can't open display: :0" , this is how you can solve it.

```shell
// Solution 
ls /tmp/.X11-unix ls -la /tmp/.X11-unix 
sudo rm -r /tmp/.X11-unix 
ln -s /mnt/wslg/.X11-unix /tmp/.X11-unix

// restart wsl
wsl --shutdown
wsl
```