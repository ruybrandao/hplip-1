![HPLIP Graphic](https://repository-images.githubusercontent.com/223663034/807cb980-0e33-11ea-9d3e-2ec5bcf80451)  
# HPLIP 3.19.11  
![Travis Build Status](https://img.shields.io/travis/ll-todd-family/hplip?style=for-the-badge)  ![GitHub last commit](https://img.shields.io/github/last-commit/ll-todd-family/hplip?style=for-the-badge)  ![GitHub repo size](https://img.shields.io/github/repo-size/ll-todd-family/hplip?style=for-the-badge)  

[HPLIP Documentation](https://github.com/ll-todd-family/hplip/doc/index.html)  

## HP Linux Imaging and Printing
HP's [original sources](https://sourceforge.net/projects/hplip/files/hplip/3.19.11/hplip-3.19.11.tar.gz/download).  
HP's [HPLIP website](https://developers.hp.com/hp-linux-imaging-and-printing).

*"Chances are, your Linux system already has the HPLIP software installed. That's because all major Linux distributions regularly pick up the HPLIP software and include it with their distribution installation. However, if it is not installed or you need to upgrade to a newer HPLIP version to support your printer, you've come to the right place."*

***HPLIP is free, open source software, distributed under the following open source licenses:***
* GNU General Public License (GPL) v2
* MIT license
* BSD license
* GNU General Public License (GPL) v3

For more information, please read [COPYING](COPYING).

# About This Repo

The version of HPLIP that is in the Debian 10.1 repository will not work on our Linux systems (for the most part), requiring us to download and compile the suite manually.  After some trial and error, the suite built on our Debian 10.1 systems.

**Install Dependency Packages**
1. Open terminal shell
2. Update your apt repos
   - sudo apt update -y
3. Install the required dependency packages
   - sudo apt install --force-yes -y build-essential libcups2 libcups2-dev cups-bsd cups-client libcupsimage2 libcupsimage2-dev libdbus-1-dev gs-esp libssl-dev libjpeg62-dev libsnmp-dev libc6 libtool libusb-1.0.0-dev make wget python-imaging policykit-1 policykit-1-gnome python-qt4 python-qt4-dbus python-dbus python-gobject python-dev python-notify python python-reportlab sane libsane-dev sane-utils xsane
   
**Get the Source Code**
1. Clone this repo somewhere convenient
   -  git clone https://github.com/ll-todd-family/hplip.git
2. Change into the directory you cloned from the git repo

**Configure HPLIP for Installation**
The following configuration options are what worked for us.  Your milage may vary.
   - (As normal user): ./configure --enable-static --enable-dependency-tracking --enable-apparmor_build --with-gnu-ld
   - You may or may not see configuration warnings.  Don't sweat it; as long as there are no error messages, it's fine.
   - (As normal user): make
   - **sudo** make dist
     - This will leave you with a file named hplip-3.19.11.tar.gz
     - If you want to try to install with this file, move it to / and then run **sudo** tar -zxf hplip-3.19.11.tar.gz
     - You also have the option of using "**sudo** make install"
       - The downside to either of these options is trying to remove them once they're installed.

***BUT WAIT!  THERE'S A BETTER INSTALL OPTION!***
   - The Makefile has an option to build a deb package!  If you want to use this option, **be sure to install the epm package**
     - **sudo** apt install epm -y
   - Now make the deb: **sudo** make deb
     - For the deb to work properly, you **must either build it as root or use sudo**!
     - Trying to install the deb built as a regular user failed for us; installing after building with sudo worked fine
     - Install the deb: **sudo** dpkg --install hplipfull*.deb
     
# Finishing After Install
* Run hp-setup to configure the suite
* Access the suite by using hp-toolbox

