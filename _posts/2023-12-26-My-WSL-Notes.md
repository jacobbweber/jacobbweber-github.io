---
layout: post
title: "My WSL Setup Notes"
date: 2023-12-26 21:00:00 -0000
categories:
tags:
---

## WSL-Setup

From an elevated Powershell. Or, use the windows store

```bash
wsl --install
```

To persist DNS resolv.conf after WSL reboot (may only be needed with wsl2 win11)

- Create wsl.conf file:

```bash
sudo vim /etc/wsl.conf
```

```yaml
#config
[network]
generateResolvConf = false
```

Configure resolve.conf for dns lookup

- Edit resolv.conf

```bash
sudo vi /etc/resolv.conf
```

> **note**
> Replace IP Addresses with your preferred DNS provider

```yaml
#config
nameserver 8.8.8.8
nameserver 8.8.4.4
```

If needed, open powershell and restart wsl

```powershell
wsl --shutdown
```

### WSL-Setup-Troubleshooting

> **Warning**
> If resolv.conf settings get overwrittent after wsl restart, run the following to set the file(s) as immutable

```shell
sudo rm /etc/resolv.conf
sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
sudo bash -c 'echo "nameserver 8.8.4.4" >> /etc/resolv.conf'
sudo bash -c 'echo "[network]" > /etc/wsl.conf'
sudo bash -c 'echo "generateResolvConf = false" >> /etc/wsl.conf'
sudo chattr +i /etc/resolv.conf

#Makes file IMMUTABLE, nothing can change this file
#sudo chattr +i /etc/resolv.conf

#Makes file Changabley again, if you need to modify or delete it
#sudo chattr -i /etc/resolv.conf
```

---

## Ansible-Setup

- Update APT

```bash
sudo apt -y update && sudo apt -y upgrade
```

- Add Ansibles official project’s PPA (personal package archive) in your system’s list of sources:

```bash
sudo apt-add-repository ppa:ansible/ansible
```

- Install Ansible

```bash
sudo apt -y install ansible
```

- Add kerberos authentication support

```bash
sudo apt -y install python3-pip
sudo apt-get -y install python3-dev libkrb5-dev krb5-user
pip3 install pywinrm[kerberos]
```

- Configure realms in krb5.conf
```bash
sudo vi /etc/krb5.conf
```

- Be sure to replace contoso.com with your preffered domain name in the examples

```yaml
[logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

[libdefaults]
    dns_lookup_realm = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true
    rdns = false
    pkinit_anchors = /etc/pki/tls/certs/ca-bundle.crt
    spake_preauth_groups = edwards25519
    default_realm = CONTOSO.COM
    default_ccache_name = KEYRING:persistent:%{uid}

[realms]
CONTOSO.COM = {

      kdc = ad01.contoso.com
      kdc = ad02.contoso.com

}

DMZ.CONTOSO.COM = {

      kdc = dmzad01.dmz.contoso.com
      kdc = dmzad02.dmz.contoso.com

}
```

### Ansible-Setup-Troubleshooting

> **Note**
> Remove ansible and re-install - need to investigate more, but
> when I blew my local wsl up this got me back to a working, and correct
> ansible version.
> <https://www.cyberciti.biz/faq/how-to-install-and-configure-latest-version-of-ansible-on-ubuntu-linux/>

```bash
sudo apt -y remove ansible
sudo apt -y --purge autoremove
sudo apt -y update
sudo apt -y upgrade
sudo apt -y install software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt -y install ansible
```

> **Note**
> IF needed, to fix "kerberos: Bad HTTP response returned from server. Code 500"
> <https://access.redhat.com/solutions/3486461>

```bash
pip install --upgrade {pywinrm,pykerberos,requests-kerberos,requests-ntlm}
```

To remove a dir:
```bash
rm -d /etc/krb5.conf.d/
```

---

## Setup-Git-in-WSL

- Install git

```bash
sudo apt-get install git
```

To set up your Git config file, open a command line for the distribution you're working in and set your name with this command (replacing "Your Name" with your preferred username):

- Git config file setup:

```bash
git config --global user.name "Your Name"
```

- Set your email with this command (replacing "youremail@domain.com" with the email you prefer):

```bash
git config --global user.email "youremail@domain.com"
```

- For AzureDevops Repos
  - To set up GCM for use with a WSL distribution, open your distribution and enter this command:

```bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager-core.exe"
```
if that doesnt work, because no -core exists, use this one instead
```bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-wincred.exe"
```

```bash
git config --global credential.https://dev.azure.com.useHttpPath true
#git config --global credential.useHttpPath true
```

---

## Setup-Powershell-For-Ubuntu

- Update the list of packages

```bash
sudo apt-get update
```

- Install pre-requisite packages.

```bash
sudo apt-get install -y wget apt-transport-https software-properties-common
```

- Download the Microsoft repository GPG keys

```bash
wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb"
```

- Register the Microsoft repository GPG keys

```bash
sudo dpkg -i packages-microsoft-prod.deb
```

- Update the list of packages after we added packages.microsoft.com

```bash
sudo apt-get update
```

- Install PowerShell

```bash
sudo apt-get install -y powershell
```

- Start PowerShell

```bash
pwsh
```

---

## Add-Certificate-into-WSL

```bash
sudo cp /mnt/c/tmp/mycert.crt /usr/local/share/ca-certificates
sudo update-ca-certificates
```

---

## Install-Extra-Ansible-Stuff
- Install Ansible-Lint

```bash
sudo apt-get install -y ansible-lint
```

- Install pyvmomi for vmware collections

```
pip3 install PyVmomi
```

---
## Optional-Notes
<https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git>
If you are seeking to access the Windows file directory from your WSL distribution command line, instead of C:\Users\username, the directory would be accessed using /mnt/c/Users/username, because the Linux distribution views your Windows file system as a mounted drive.

I was able to connect to my windows host after following those steps
However, I had to solve two more issues before I was able to run ansible playbooks against both, WSL and windows host:

1. Define connection for WSL
Windows host uses ```yaml ansible_connection=winrm```, but for WSL needs a different connection, I've set ```yaml ansible_connection=local```.

2. Avoid connection var being overriden
The ansible_connection var is overridden. This is because the var name and the host name is the same. This means that you can either run a playbook for WSL or for Windows host but not against both, as they need different connection.

To fix that you can either set hash-behaviour, or set two different host names for localhost under your WSL, /etc/hosts. I've done the second one:

```bash
127.0.0.1   wsl.local
127.0.0.1   windows.local
```

My /etc/ansible/hosts:

```bash
[wsl]
wsl.local 

[wsl:vars]
ansible_connection=local

[windows]
windows.local 
[windows:vars]
ansible_port=5985
ansible_connection=winrm
ansible_winrm_transport=basic
ansible_user=<<ansible_user>>
ansible_password=<<ansible_password>>

```

For lab type environments, you may need to configure winrm for basic authentication.

```powershell
#Powershell
#Show winrm config
winrmwinrm get winrm/config
#Enable basic auth
Set-Item -Path WSMan:\localhost\Service\Auth\Basic -Value $true
```

Now I can run an ansible_playbook with tasks running against both, my windows host and my WSL. Here for more details on configuration.
