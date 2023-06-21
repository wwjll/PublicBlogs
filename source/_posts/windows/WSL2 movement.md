---
title: Move wsl to desired position
categories:
  - windows
---


Using https://github.com/pxlrbt/move-wsl.git

after moving you may need to setup for normal usage

```powershell
wsl -l -v(get distro and version)
wsl --set-version <Distro> <Version> 
```

and fix  \\wsl$ can't access if there's

```powershell
wsl reset
```

change distribution name in
```
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Lxss
```
