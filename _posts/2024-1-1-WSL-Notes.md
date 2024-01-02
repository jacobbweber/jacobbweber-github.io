---
layout: post
title: "WSL Setup Notes"
date: 2024-1-1 1:00:00 -0000
categories:
tags:
---

I wanted to start this new year off being productive by doing a little prep work for upcoming hobby projects. I cleaned up old workloads running on my Hyper-V host and reinstalled the Operating System on my PC. Fresh year, fresh installs. I went through the process of reinstalling all my stuff having the typical thoughts "Why don't I automate all this". I decided not having everything automated was fine. But setting up a quick WSL2 environment was a little tedious. I usually just go over to my GitHub repo [my-wsl-setup](https://github.com/jacobbweber/my-wsl-setup) and just copy line by line the commands I need. For my needs this has worked fine, I don’t have the most robust or sophisticated WSL setup. But I do typically install Ansible, git, PowerShell, and dependencies.

I went the route of creating a simple shell script, nothing fancy, but just wanted to start somewhere. After I got the script created I tested in out on a Win11 VM running in Hyper-V

The workflow went something like this:

- Create a Windows 11 VM
- Enable nested virtualization on the VM

```powershell
$VMName = 'win11'
Stop-VM -VMName $VMName
Set-VMProcessor -VMName win11 -ExposeVirtualizationExtensions $true
Checkpoint-VM -VMName $VMName -SnapShotName 'Pre-WSL Setup'
Start-VM -VMName $VMName
```

- Log into the VM
- Install Chocolatey
- Install Git
- Clone the repo
- Run prep-windows.ps1 from an elevated PowerShell window, script asks to reboot.
- After logging back in, run the prep-windows.ps1 script again to finish installing WSL.

> I was hung up on the last two steps. It felt weird running the script twice vs having two separate scripts, but the thought of having more files for something so simple seemed worse. So with some conditional logic it just checks if the first steps are done and proceeds.
 {: .prompt-info }

- After wsl Ubuntu is setup, open Ubuntu from the start menu and setup the first local user.
- Once logged in, I executed the wsl-config.sh script from its cloned location on windows.

```bash
bash sudo /mnt/c/Users/lab/my-wsl-setup/wsl-config.sh
```

> Because of the way I wrote this shell script on a DOS based machine then doing a binary transfer to the Linux system I was getting error "\r': Command not Found errors. To get around this I just ran
>
> ```bash
> sed -i 's/\r$//' /mnt/c/Users/lab/my-wsl-setup/wsl-config.sh
> ```
 {: .prompt-info }

- Manually updated my git config with my default username and email
- Manually updated my krb5.conf file to add the default realms for my lab in place of the contoso.com place holders.

That's where I decided to leave off for my WSL setup for now.

I did a little browsing to see what others are doing for this and found some great example projects. I saw a few where people were utilizing the method of invoking shell scripts via PowerShell on the windows side

```powershell
wsl bash -e ./wsl-config.sh
```

Wouldn’t that be slick to get that working and put it at the end of the first script. Some other projects I see examples of PowerShell choice driven scripts that let you pick what flavor of Linux you want installed with WSL as a wrapper. Seemed great if you have the need to install multiple instances.

Happy New Year!