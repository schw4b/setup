# Setup of my linux boxes

##Check SATA ports
Your should attach your disk at the fastest sata links

    dmesg | grep -i ahci # is ahci enabled in BIOS? See also hardinfo
    dmesg | grep SATA | grep up
    sudo smartctl -a /dev/sda | grep "^SATA"

##Dropbox

    sudo apt-key adv --keyserver pgp.mit.edu --recv-keys 5044912E
    sudo add-apt-repository "deb http://linux.dropbox.com/ubuntu $(lsb_release -sc) main"
    sudo apt-get update
    sudo apt-get install dropbox
    dropbox start -i

Install dropbox from repository and subscribe to folder '.env'

##Fluxbox window manager

    sudo apt-get install encfs git
    mkdir ~/env
    vi .pw # enter pw
    chmod 600 .pw
    encfs ~/Dropbox/.env ~/env
    ~/env/conf/install
    sudo apt-get install vim fluxbox lxterminal pcmanfm

##Install Google Chrome

    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
    sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
    sudo apt-get update
    sudo apt-get install google-chrome-stable
    
## Look and Feel

    gsettings set com.canonical.desktop.interface scrollbar-mode normal # disable overlay scroll
    gsettings reset com.canonical.desktop.interface scrollbar-mode # enable again
    get lxappearance gnome-themes-standard
    
    sudo add-apt-repository ppa:moka/daily
    sudo apt-get update
    sudo apt-get install moka-icon-theme

## SSD Tuning

    sudo hdparm -I /dev/sdb | grep TRIM
    sudo vi /etc/cron.weekly/fstrim # for non-samsung drives
    exec fstrim-all --no-model-check
    cat /proc/mounts | grep noatime
    sudo vi /etc/fstab # add noatime

## SMB Credentials

    cp ~/env/private/.smbcredentials.* ~/
    chmod 600 ~/.smbcredentials.*

## Sudoer

    sudo visudo

    %simon ALL=NOPASSWD: /sbin/reboot
    %simon ALL=NOPASSWD: /sbin/shutdown
    %simon ALL=NOPASSWD: /usr/sbin/pm-suspend
    %simon ALL=NOPASSWD: /usr/sbin/vpnc-connect
    %simon ALL=NOPASSWD: /usr/sbin/vpnc-disconnect
    %simon ALL=NOPASSWD: /usr/bin/unattended-upgrade
    %simon ALL=NOPASSWD: /usr/bin/apt-get
    %simon ALL=NOPASSWD: /bin/mount
    %simon ALL=NOPASSWD: /bin/umount

## Packages
Basic packages:

    get sylpheed xterm r-base-core cmus sox scribus gimp unrar lame libsox-fmt-mp3 filezilla hplip nmap imagemagick smbclient vpnc screenruler pwgen mesa-utils aspell-de a2ps easytag gnome-specimen cifs-utils abcde id3v2 gnome-screenshot screen iotop flip geany geany-plugin-spellcheck chromium-codecs-ffmpeg-extra gksu mricron mriconvert xfce4-power-manager lxrandr
    
## Rstudio

    get libgstreamer0.10-0 libgstreamer-plugins-base0.10-0 libjpeg62
    sudo dpkg -i rstudio-0.99.903-amd64.deb

## Libre Office

    get myspell-en-us myspell-de-ch hyphen-en-us hyphen-de

## Latex

    get texlive-latex-base texlive-latex-extra texlive-bibtex-extra texlive-publishers texlive-fonts-extra texlive-math-extra texlive-humanities texlive-lang-german texinfo

## Games

    get freeciv-client-gtk micropolis
    
    Flightgear:
    
    sudo add-apt-repository ppa:saiarcot895/flightgear
    sudo apt-get update
    get flightgear
    
## NVIDIA
Search nvidia website for newest driver for card
    
    lspci | grep VGA
    
    search nvidia-36
    get nvidia-361

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

## Enable encrypted swap

    sudo cryptsetup status cryptswap1
    sudo vim /etc/crypttab
    sudo vim /etc/fstab # uncomment cryptswap1

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
