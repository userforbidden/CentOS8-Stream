# CentOS8-Stream
 
![centos](FlowImages/CentOS-Stream.drawio.svg)


Description  
========  
I am wrting this repository to keep track of how I downloaded and installed the CentOS 8 Stream and What configuration I made to work on my Laptop Leonovo Ideapad Y510P.

Installation of Wine
=========

Step 1 - Prerequisite
------

Become a root user 
```
$ sudo -i
```
Install the development packaages needeed
```
# dnf clean all 
# dnf update
```
Install required pacjkage for Wine using any package manager commands
```
# dnf groupinstall 'Development Tools'
# dnf install libX11-devel zlib-devel libxcb-devel libxslt-devel libgcrypt-devel libxml2-devel gnutls-devel libpng-devel libjpeg-turbo-devel libtiff-devel dbus-devel fontconfig-devel freetype-devel 
```

Step 2 - Install Wine on CentOS 8
-------
Download the source code for WIne. RPm packages are not available

```
# cd /opt
# wget https://dl.winehq.org/wine/source/5.x/wine-5.1.tar.xz
# tar -Jxf wine-5.1.tar.xz
# cd wine-5.1
# history
```
Configure wine using following command based on system architecture since mine is 64bit architecture I used 
```
# ./configure  --enable-win64
```
Finally, run make and make install command to compile the wine source and install it in your system
```
# make
# make install 
``` 
Step 3 - Check Wine Version
-----
Using the following command I checked the version of the wine installed in my system

```
wine64 --version
```

