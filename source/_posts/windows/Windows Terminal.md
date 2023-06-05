#### Windows PowerShell

Enhance terminal
	https://learn.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup#install-a-nerd-font
	You can follow the  tutorial to enhance the terminal but you probably run into some problems, but it is easy to solve.
	
If you can't open $profile file.Run the following command before opening the profile.
```shell
new-item $profile -ItemType file -Force
notepad $profile
```

If you start the windows terminal and bump into **“cannot be loaded because running scripts is disabled on this system**“ problem you mignt run the following command to 
permit PowerShell script execution.
```shell
Set-ExecutionPolicy RemoteSigned
```

To avoid falut display of your command line , don't forget to change the font that oh-my-posh using.


#### WSL terminal

follow the tutorial

https://calebschoepp.com/blog/2021/how-to-setup-oh-my-posh-on-ubuntu/

write command to ~/.bashrc so every terminal will use oh-my-posh when launched

```shell
eval "$(oh-my-posh --init --shell bash --config ~/.{theme}.omp.json)"
```