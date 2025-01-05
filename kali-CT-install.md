# Kali-Container-Installation 

## Install Base Packages
```bash
apt -y install \
   wget \
   inetutils-tools \
   iputils-ping \
   ssh \
   man \
   nano
```  

## Install ZSH Kali Theme  
```bash
sudo apt -y install \
   kali-defaults \
   zsh \
   zsh-syntax-highlighting \
   zsh-autosuggestions
```  

## Create a Traditional User:Group (kali:kali)  
```bash
adduser kali && usermod -aG sudo kali && id kali
```  

## Enable SSH Server and Login Using "kali" User (via Putty)  
1. Edit the SSH configuration file:  
   ```bash
   nano /etc/ssh/sshd_config
   ```  
   - Set `PermitRootLogin yes` (optional)  

2. Enable and start the SSH service:  
   ```bash
   systemctl enable ssh && systemctl start ssh
   systemctl status ssh
   ```

3. Perform additional updates and installation:  
   ```bash
   sudo apt update && sudo apt -y dist-upgrade
   ```
   ```bash
   sudo reboot now  # optional
   sudo apt-cache search kali-linux #sudo kali-tweaks
   sudo apt -y install kali-linux-default
   ``` 

## Setting up RDP with Kali Base XFCE  
1. Update and upgrade the Kali distro:  
   ```bash
   apt-get update
   apt-get dist-upgrade -y
   apt-get install -y kali-desktop-xfce xorg xrdp firefox-esr
   apt-get purge network-manager
   ```  

2. Perform additional updates and installation:  
   ```bash
   sudo apt-get update && sudo apt-get -y dist-upgrade
   sudo reboot now  # optional
   sudo apt-cache search kali-linux
   sudo apt-get -y install kali-linux-default
   sudo apt-get purge network-manager
   ```  

3. Check and enable RDP:  
   ```bash
   systemctl status xrdp
   systemctl enable xrdp && systemctl start xrdp
   systemctl status xrdp
   ```
   
