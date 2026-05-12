# Setup of my Linux boxes

## Checks

### SATA ports
You should attach your disk to the fastest SATA link.

    sudo dmesg | grep SATA | grep up
    sudo dmesg | grep ata?

### Secure boot

    mokutil --sb-state

## GNOME settings

### Enable paste with the middle mouse button
    
    gsettings set org.gnome.desktop.interface gtk-enable-primary-paste true

## Install vim

    sudo apt-get install vim

## Install Google Chrome
Download from Google website, then run:

    sudo dpkg -i google-chrome-stable_current_amd64.deb
      
## Dropbox
Download Dropbox from the official website.

    sudo dpkg -i dropbox_2026.01.15_amd64.deb

## Setup encrypted filesystems

    vim ~/.encfs
    # enter password
    chmod 600 ~/.encfs

    sudo apt-get install encfs
    mkdir ~/env; cat ~/.encfs
    encfs ~/Dropbox/.env/ ~/env/
    ~/env/conf/install
   
## Install SSH keys

    tar xvzf ~/.private/ssh.tar.gz -C $HOME

## Packages

### Basic tiny tools

    sudo apt-get install unrar pwgen flip hplip

### Image processing

    sudo apt-get install imagemagick gimp

### Git

    sudo apt-get install git
    git config --global user.email "schw4b@gmail.com"
    git config --global user.name "Simon Schwab"

Resolve the issue under Windows that Linux changed files appear changed due to different line breaks.

    git config --global core.autocrlf true

### Zoom

    sudo dpkg -i zoom_amd64.deb
    sudo apt --fix-broken install # install dependencies
    sudo apt-get install libopengl0
    
### R, RStudio, and Quarto
The best way to install R (package r-base) is to follow the most recent instructions for Ubuntu Linux at <https://cran.r-project.org/>.

    sudo apt-get --no-install-recommends install r-base
    sudo apt-get install r-base-dev
    
Get the RStudio deb package from the website and install it.

    sudo apt-get install libssl-dev libclang-dev
    sudo dpkg -i rstudio-2026.04.0-526-amd64.deb
    
Use Chaos theme and font size 12 for editor and help.

    sudo dpkg -i quarto-1.9.37-linux-amd64.deb
    
Install libraries that are required by some of the R packages I'm using
    
    sudo apt-get install libcurl4-openssl-dev # httr and rvest

### Latex

    sudo apt-get install texlive-latex-extra

### LibreOffice

    sudo apt-get libreoffice hyphen-en-us libreoffice-l10n-de
    
