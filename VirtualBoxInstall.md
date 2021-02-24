Installation
====

```
dnf config-manager --add-repo=https://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo

rpm --import https://www.virtualbox.org/download/oracle_vbox.asc

dnf search virtualbox
```
Latest Version of VirtualBox at the time of installing this on Feb 22 2021 is VirtualBox-6.1

```
dnf install VirtualBox-6.1.18-1.el8.x86_64

```
Installation of VirtualBox Server 
=====
```
dnf install VirtualBox-server-6.1.18-1.el8.x86_64
```
Adding VirtualBox Development and Guest Addition packages 
=====
```
dnf install VirtualBox-devel-6.1.18-1.el8.x86_64
dnf install VirtualBox-guest-additions-6.1.18-1.el8.x86_64

dnf install akmod-VirtualBox kernel-devel-$(uname -r)
akmods; systemctl restart vboxdrv.service

```
Installation of Extension Packs
=====
Extension pack needs to be installed to enable the Remote Server Display

First make sure dependencies are installed
```
dnf install gcc kernel-devel kernel-headers dkms make bzip2 perl
```
Download the Extension pack 
```
wget https://download.virtualbox.org/virtualbox/6.1.18/Oracle_VM_VirtualBox_Extension_Pack-6.1.18.vbox-extpack
```
Install
```
VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.1.18.vbox-extpack 
```


