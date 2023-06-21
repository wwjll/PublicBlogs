---
categories:
  - windows
---
#### Global proxy setting

System running on wslw like Ubuntu is connected to Windows virtually , Window is netting its IP address.Other computer won't know the actual ip of the wsl2.
System running on wslw like Ubuntu is connected to Windows virtually , Window is netting its IP address.Other computer won't know the actual ip of the wsl2.


1.Set windows firewall

You must turn on your wsl for vEthernet(WSL) to be detected so you can allow the inbound action. Use "ipconfig /all" to find the vEthernet.
```powershell
New-NetFirewallRule -DisplayName "WSL" -Direction Inbound  -InterfaceAlias "vEthernet (WSL)"  -Action Allow
```


2.Set Linux proxy in ~/.bashrc
```shell
	export windows_host=`cat /etc/resolv.conf|grep nameserver|awk '{print $2}'`
	export ALL_PROXY=socks5://$windows_host:10810
	export HTTP_PROXY=$ALL_PROXY
	export http_proxy=$ALL_PROXY
	export HTTPS_PROXY=$ALL_PROXY
	export https_proxy=$ALL_PROXY

if [ "`git config --global --get proxy.https`" != "socks5://$windows_host:10810" ]; then
            git config --global proxy.https socks5://$windows_host:10810
fi
```


3.Try 

```shell
curl google.com
curl --location google.com
```


#### Chrome individual setup

1.Use command in Chrome Launcher (this acquires gui setup)

```
// xrdp + xfce4  setting chrome start command
/usr/bin/google-chrome-stable %U --proxy-server="socks5://182.168.1.100:10802"
// wslg chrome using host proxy

google-chrome-stable --no-sandbox --proxy-server="socks5://182.168.1.100:10810"
```

2. I don't know why it will fails each time wsl2 restart , so you might need SwitchOmega plugin for fast proxy setup.Use ipconfig /all to get vEhternet(WSL) and use in proxy setting.

#### Visual Adapter to link both

1.Make sure system is win11 professional or even more advanced and Hyper-v features is turned on.

2.Setup a virtual switch to connect wsl ethernet and the host windows system adapter.

```powershell
// Get adapter
get-netadapter

// Setup a virtual switch
Set-VMSwitch WSL -NetAdapterName <Adapter you are using>

```


```powershell
rename-vmswitch
```

#!/bin/bash

```bash

sudo ip addr del $(ip addr show eth0 | grep 'inet\b' | awk '{print $2}' | head -n 1) dev eth0
sudo ip addr add 192.168.1.150/24 broadcast 192.168.1.132 dev eth0
sudo ip route add 0.0.0.0/0 via 192.168.1.1 dev eth0

```


google-chrome --no-sandbox --proxy-server="socks5://192.168.1.132:10802"



Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
Connect-VMNetworkAdapter -VMNetworkAdapterName "vEthernet(WSL)" -SwitchName "WSLSwitch"
