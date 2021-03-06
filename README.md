# Setup of my linux boxes

## Check SATA ports
Your should attach your disk at the fastest sata links

    dmesg | grep SATA | grep up
    dmesg | grep ata?

## Install Vim
    sudo apt-get install vim

## Install Google Chrome

    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
    sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
    sudo apt-get update
    sudo apt-get install google-chrome-stable
      
## Look & Feel

    rm -rf ~/Templates ~/Public ~/examples.desktop
    sudo apt install gnome-tweak-tool

## Dropbox
Download Dropbox from official website.

    sudo dpkg -i dropbox_2020.03.04_amd64.deb

## Setup enctypted filesystems

    vim ~/.encfs
    # enter password
    chmod 600 ~/encfs

    sudo apt-get install encfs
    mkdir ~/env; cat ~/.encfs
    encfs ~/Dropbox/.env/ ~/env/
    ~/env/conf/install

## Improve memory and disable Wayland
    sudo vim  /etc/gdm3/custom.conf
    WaylandEnable=false
    
## Install SSH keys
    tar xvzf ~/.private/ssh.tar.gz -C $HOME

## Sudo

    sudo visudo

    %simon ALL=NOPASSWD: /sbin/reboot
    %simon ALL=NOPASSWD: /sbin/halt
    %simon ALL=NOPASSWD: /usr/sbin/pm-suspend
    %simon ALL=NOPASSWD: /usr/sbin/vpnc-connect
    %simon ALL=NOPASSWD: /usr/sbin/vpnc-disconnect
    %simon ALL=NOPASSWD: /usr/bin/unattended-upgrade
    %simon ALL=NOPASSWD: /usr/bin/apt-get
    %simon ALL=NOPASSWD: /bin/mount
    %simon ALL=NOPASSWD: /bin/umount

## Packages

### Basic packages

    sudo apt-get install scribus gimp unrar filezilla hplip nmap imagemagick smbclient cifs-utils vpnc screenruler pwgen glmark2 flip colordiff hardinfo

### Skype
Download Skype from official website.

    sudo dpkg -i ~/Downloads/skypeforlinux-64.deb

### Git
    sudo apt-get install git
    git config --global user.email "schw4b@gmail.com"
    git config --global user.name "Simon Schwab"
    
### MRI/neuroscience:

    sudo apt-get install mricron dcm2niix
    
### Multimedia

    sudo apt-get install ubuntu-restricted-extras
    
### R and Rstudio
    sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    sudo apt-get install r-base
    
Get RStudio deb package from website and install it.
    
    sudo apt-get install libjpeg62 
    sudo dpkg -i studio-1.3.959-amd64.deb
    
Fix for rstudio blank screen after window resizing on ultia-wide monitors

    sudo apt-get install libqt5webenginecore5
    
Install libraries that are required by some of the R packages I'm using
    
    sudo apt-get install libcurl4-openssl-dev # httr and rvest

### Latex

    sudo apt-get install texlive-latex-extra

### Games

    get freeciv-client-gtk micropolis
    
    Flightgear:
    
    sudo add-apt-repository ppa:saiarcot895/flightgear
    sudo apt-get update
    get flightgear
    
## VirtualBox

    sudo apt-get libqt5x11extras5
    dpkg -i virtualbox-5.1_5.1.26-117224-Ubuntu-xenial_amd64.deb
    
## NVIDIA
Search nvidia website for suitable driver version for card

    sudo add-apt-repository ppa:graphics-drivers
    sudo apt-get update
    search ^nvidia-xxx | grep binary
    get nvidia-xxx

Fix splash after nvidia driver was installed

    sudo apt-get install v86d
    sudo vim /etc/default/grub
    GRUB_GFXMODE=1280x1024x24
    GRUB_GFXPAYLOAD_LINUX=keep
    echo FRAMEBUFFER=y | sudo tee /etc/initramfs-tools/conf.d/splash
    sudo update-initramfs -u
    sudo update-grub2

## Speed up GRUB Menu

    sudo vim /etc/default/grub
    set timeout to 2 sec
    comment hidden timeout
    sudo update-grub2

## Change kernel boot options
For echobase:

    sudo vim /etc/default/grub
    GRUB_CMDLINE_LINUX_DEFAULT="nomodeset"
    sudo update-grub

## Printers
HP Officejet Pro 6830 e-All-in-One

    sudo apt-add-repository ppa:otto-kesselgulasch/misc
    sudo apt-get update
    get hplip
    hp-doctor # for HP-1020
    
This may be required with office printers
    
    sudo vim /etc/samba/smb.conf
    
    [global]
    client min protocol = SMB2
    client max protocol = SMB3
    
Check access to a windows domain printer

    smbclient -L host -U DOMAIN/simons%password

