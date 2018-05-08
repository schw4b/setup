# Setup of my linux boxes

## Check SATA ports
Your should attach your disk at the fastest sata links

    dmesg | grep SATA | grep up
    dmesg | grep ata?
    
## Automatic Security Updates
    sudo apt-get install unattended-upgrades
    sudo dpkg-reconfigure unattended-upgrades
    
## Update system
    sudo apt-get update
    rmdir ~/Documents/ ~/Music/ ~/Pictures/ ~/Templates/ ~/Videos/ ~/Public/
    rm ~/examples.desktop

## Dropbox
Download Dropbox package from official website.

    sudo apt-get update
    sudo dpkg -i dropbox_2015.10.28_amd64.deb
    dropbox start -i

Install dropbox from repository and subscribe to folder '.env'

## Fluxbox window manager
    sudo apt-get install encfs git
    mkdir ~/env
    vi .encfs # enter pw
    chmod 600 .encfs
    cat .encfs
    encfs ~/Dropbox/.env ~/env
    ~/env/conf/install
    sudo apt-get install vim fluxbox lxterminal pcmanfm

Reboot into Fluxbox now.

## Look and Feel
    sudo apt-get install moka-icon-theme
    
## Install SSH keys
    tar xvf ~/env/private/ssh.tar.gz -C $HOME

## Install Google Chrome

    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
    sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
    sudo apt-get update
    sudo apt-get install google-chrome-stable

## SMB Credentials

    cp ~/env/private/.smbcredentials.* ~/
    chmod 600 ~/.smbcredentials.*

## Sudoer

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
Basic packages:

    sudo apt-get install xterm cmus sox scribus gimp unrar lame libsox-fmt-mp3 filezilla hplip nmap imagemagick smbclient vpnc screenruler pwgen mesa-utils aspell-de a2ps easytag cifs-utils abcde id3v2 gnome-screenshot screen iotop flip geany geany-plugin-spellcheck xfce4-power-manager lxrandr colordiff pm-utils
    
### MRI/neuroscience:

    sudo apt-get install mricron dcm2niix
    
### Multimedia
    sudo apt-get install ubuntu-restricted-extras
    
### R and Rstudio
    sudo apt-get install r-base   
    
Get RStudio deb package from website and install it.
    sudo apt-get install libjpeg62 
    sudo dpkg -i rstudio-xenial-1.0.153-amd64.deb

Install prerequisite packages for `devtools`
    
    sudo apt-get install libcurl3 libssl-dev

### Libre Office

    get myspell-en-us myspell-de-ch hyphen-en-us hyphen-de

### Latex

    get texlive-latex-base texlive-latex-extra texlive-bibtex-extra texlive-publishers texlive-fonts-extra texlive-math-extra texlive-humanities texlive-lang-german texinfo

### Games

    get freeciv-client-gtk micropolis
    
    Flightgear:
    
    sudo add-apt-repository ppa:saiarcot895/flightgear
    sudo apt-get update
    get flightgear

### Skype
Download Skype from official website.

    get gconf-service libgconf-2-4
    sudo dpkg -i ~/Downloads/skypeforlinux-64.deb
    
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
    
Check access to a bloody windows domain printer

    smbclient -L host -U DOMAIN/simons%password
    


