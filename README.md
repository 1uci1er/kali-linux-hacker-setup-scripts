# kali-linux-hacker-setup-scripts
A comprehensive guide to setting up and optimizing Kali Linux for hacking, CTFs, and cybersecurity. Includes essential scripts, tools, and configurations for a seamless hacking experience.
---
![my_kali_linux_setup](https://github.com/user-attachments/assets/a64bcd44-2c84-4044-8dad-43ea24e3fd6a)

# Kali Linux Setup and Optimization Guide

<div align="center" style="border: 2px solid #ccc; padding: 10px; margin: 10px 0; background-color: #f9f9f9;">
  <strong>Time Spent:</strong> 2 hours 12 minutes
</div>

Welcome to my **Kali Linux Setup and Optimization Guide**! This repository contains essential tips, tricks, and scripts to help you set up and optimize your Kali Linux environment for hacking, CTFs, and general productivity. Whether you're a beginner or an experienced user, these steps will streamline your workflow and enhance your experience.

---

## Table of Contents

1. [Update and Upgrade](#1-update-and-upgrade)
2. [Change Hostname](#2-change-hostname)
3. [Change Default Repository](#3-change-default-repository)
4. [Essential Tweaks for Hackers](#4-essential-tweaks-for-hackers)
   - [Remove Boilerplates](#41-remove-boilerplates-that-kali-defaults-home-directories)
   - [CTF Setup](#42-ctf-setup-️)
   - [Disable Lock Screen](#43-disable-your-lock-screen)
   - [Change SSH Keys & Default Password](#44-change-your-ssh-keys--default-password)
   - [Configure DNS Servers](#45-configure-google-dns--opendns-servers)
   - [Enable Autologin](#46-enable-autologin-for-a-seamless-login-experience)
5. [Essential Packages to Install](#5-essential-packages-to-install)
   - [Python3-pip Installation](#52-python3-pip-installation)
   - [Archive Managers](#54-install-archive-managers)
   - [Guest Additions](#55-install-guest-additions)
   - [OBS Studio](#56-install-obs-studio-for-screen-recording)
   - [Wine for Windows Applications](#57-setup-wine-to-use-windows-applications-in-linux)
   - [Terminal Multiplexer](#58-install-multiplexer-terminal)
6. [Setup Your Own Aliases](#6-setup-your-own-aliases)
   - [Get Local and VPN IPs](#get-local-and-vpn-ips)
   - [Common Tasks](#common-tasks)
   - [CTF Directory Shortcut](#ctf-directory-shortcut)
   - [System Updater](#system-updater)
   - [HTB & THM VPN Shortcuts](#htb--thm-vpn-shortcuts)
7. [Conclusion](#conclusion)

---

## 1. Update and Upgrade

Before making any changes, ensure your system is up-to-date.

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

**Note:** Regularly updating your system ensures you have the latest security patches and software updates.

---

## 2. Change Hostname

Customize your hostname to easily identify your machine in a network.

```bash
sudo hostnamectl set-hostname "1uci1er"
```

**Tip:** Choose a hostname that reflects your personality or the purpose of the machine.

---

## 3. Change Default Repository

Kali Linux uses rolling releases, so it's important to ensure your repository is correctly configured.

```bash
echo "deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware" | sudo tee /etc/apt/sources.list
```

**Additional Tip:** Enable the `deb-src` mirror for access to source packages.

```bash
echo "deb-src http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware" | sudo tee -a /etc/apt/sources.list
```

---

## 4. Essential Tweaks for Hackers

### 4.1 Remove Boilerplates That Kali Defaults, Home Directories

Kali Linux comes with default directories that you might not need. Here's how to clean them up:

```bash
#!/usr/bin/bash
echo "Removing Kali Boiler Home Directories!!.."
mv $HOME/Downloads/* $HOME
# Wait Wait Brother, If You Have any File or Folder Plz Move to Another Location..
sudo rm -rf $HOME/{.vim,Downloads,Pictures,Documents,Music,Videos}
```

**Note:** Be cautious when running this script, as it will permanently delete the specified directories.

---

### 4.2 CTF Setup ✌️

Organize your CTF (Capture The Flag) challenges with dedicated directories.

```bash
mkdir -p $HOME/CTF
touch $HOME/CTF/Target

mkdir -p $HOME/CTF/{htb,thm}
```

**Tip:** Use subdirectories for different platforms like Hack The Box (HTB) and TryHackMe (THM) to keep things organized.

---

### 4.3 Disable Your Lock Screen

To disable the lock screen:

- Go to **Settings** > **Power Manager** > **Display Tab** and disable screen lockout.

**Security Note:** Disabling the lock screen can be convenient but may pose a security risk. Use this option wisely.

---

### 4.4 Change Your SSH Keys & Default Password

Changing default SSH keys and passwords is a critical security measure.

```bash
cd /etc/ssh
sudo mkdir original_ssh_keys
sudo mv ssh_host_* original_ssh_keys/
sudo dpkg-reconfigure openssh-server
```

**Security Tip:** Always use strong, unique passwords and consider using SSH key-based authentication for added security.

---

### 4.5 Configure Google DNS / OpenDNS Servers

Using reliable DNS servers can improve your internet experience.

```bash
echo "nameserver 1.1.1.1" | sudo tee /etc/resolv.conf
```

**Alternative DNS Servers:**
- Google DNS: `8.8.8.8` and `8.8.4.4`
- OpenDNS: `208.67.222.222` and `208.67.220.220`

---

### 4.6 Enable Autologin for a Seamless Login Experience

Autologin can save time, but it’s not recommended for secure environments.

```bash
# For Gnome Desktops
sudo nano /etc/gdm3/daemon.conf

# For Xfce (default Kali desktop)
sudo nano /etc/lightdm/lightdm.conf
```

Add or modify the following lines:

```bash
autologin-user=<your-username>
autologin-user-timeout=0
```

**Security Note:** Autologin should be avoided on systems that handle sensitive data.

---

## 5. Essential Packages to Install

Here’s a list of essential packages that every hacker should have:

```bash
sudo apt install -y software-properties-common kali-archive-keyring git stow curl zsh neofetch tmux textlive-latex-recommended textlive-fonts-extra pandoc evince seclists gobuster rlwrap dirsearch html2text gedit python3 python-is-python3 pipx golang crackmapexec netexec
```

---

### 5.2 Python3-pip Installation

Ensure you have the latest version of `pip` installed:

```bash
python3 -m pip install --upgrade pip
```

---

### 5.4 Install Archive Managers

Handling various archive formats is essential:

```bash
sudo apt-get install unrar unace p7zip zip unzip p7zip-full p7zip-rar file-roller -y
```

---

### 5.5 Install Guest Additions

For VMware or VirtualBox users, installing guest additions enables features like fullscreen mode and clipboard sharing.

```bash
sudo apt install -y open-vm-tools
```

---

### 5.6 Install OBS Studio For Screen Recording

OBS Studio is a powerful tool for recording your screen:

```bash
sudo apt-get install obs-studio

# If not available, use the PPA:
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt install obs-studio
```

---

### 5.7 Setup Wine to Use Windows Applications in Linux

Wine allows you to run Windows applications on Linux:

```bash
sudo dpkg --add-architecture i386
sudo apt-get update 
sudo apt-get install wine32
```

**Note:** Wine is useful for running Windows-specific tools, but dual-booting is often a better solution for heavy Windows usage.

---

### 5.8 Install Multiplexer Terminal

Terminal multiplexers like `tmux` or `terminator` can enhance your workflow:

```bash
sudo apt install tmux
```

**Tip:** Learn the basics of `tmux` to manage multiple terminal sessions efficiently.

---

## 6. Setup Your Own Aliases

Aliases are shortcuts for frequently used commands. Here are some useful ones:

### Get Local and VPN IPs

```bash
# Get local WiFi or LAN IP
alias myip="ip -o -4 addr show eth0 | awk '{print \$4}' | cut -d'/' -f1"

# Get VPN IP (e.g., HTB or THM)
alias tunip="ip -o -4 addr show tun0 | awk '{print \$4}' | cut -d'/' -f1"
```

---

### Common Tasks

```bash
alias ins="sudo apt install -y"
alias rem="sudo apt purge -y"
alias ls="ls --color=always"
alias ll="clear && ls --color=always -rthla"
alias grep="grep --color=auto"
```

---

### CTF Directory Shortcut

If you’ve set up a CTF directory, use this alias to navigate quickly:

```bash
alias ctf="cd $HOME/CTF && ll"
```

---

### System Updater

Simplify system updates with a single command:

```bash
updater() {
    sudo apt update -y 2> /dev/null;
    sudo apt --fix-broken install -y 2> /dev/null;
    sudo apt upgrade -y 2> /dev/null;
    sudo apt dist-upgrade -y 2> /dev/null;
    sudo apt autoremove -y 2> /dev/null;
    sudo apt autoclean -y 2> /dev/null;
    sudo apt clean -y 2> /dev/null;
}
```

**Usage:** Just type `updater` in the terminal to run all update commands.

---

### HTB & THM VPN Shortcuts

Connect to Hack The Box or TryHackMe VPNs with ease:

```bash
# Hack The Box
htb(){
  pid=$(pgrep openvpn | sed -ne 's/\([0-9]*\)/\1/p'); sudo kill $pid
  cd $HOME/ctf/htb/
  sudo openvpn *.ovpn </dev/null &>/dev/null &
  clear
}

# TryHackMe
thm(){
  pid=$(pgrep openvpn | sed -ne 's/\([0-9]*\)/\1/p'); sudo kill $pid
  cd $HOME/ctf/thm/
  sudo openvpn *.ovpn </dev/null &>/dev/null &
  clear
}
```

---

## Conclusion

These tips and tricks should help you set up a more efficient and personalized Kali Linux environment. Feel free to customize these steps according to your needs and preferences. Happy hacking!

---
