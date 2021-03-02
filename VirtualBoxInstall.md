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

Running the Virtual Machine Headless
====
List Available VM's
```
[saranyans@saranyan ~]$ VBoxManage list vms
"Kali_Linux_2020" {11xxxx69-c859-493b-bxx5-a1ebxxxxx4df}
"Windows10_Education_64" {51cxxx47-28xxf-4xx1-9xxc-148xxxxx6f1}
```
Start the VM using the below command 
```
[saranyans@saranyan ~]$ VBoxManage startvm "Kali_Linux_2020" --type headless
Waiting for VM "Kali_Linux_2020" to power on...
VM "Kali_Linux_2020" has been successfully started.
```
Enabling Remote Display
=======
You can enable Remote display of your VM by going to the Display tab in the settings page 

![Display Server](FlowImages/VirtualBox/DisplayServer.drawio.svg)

If you have the settings for Server Port, Authentication Method: External and Authentication Timeout: 5000 you can connect to the VM remotely by using user account of the host where you deployed this VM. 
If you want to use a different user account other than the host's user credential, follow the below instruction to add a separate user for RDP connection 

Adding a separate User to authenticate the RDP connection 
===
An additional library called VBoxAuthSimple performs authentication against credentials configured in the extradata section of a virtual machine's XML settings file. This is probably the simplest way to get authentication that does not depend on a running and supported guest. The following steps are required 

Check if your VM's are running 
```
$ VBoxManage list runningvms
"Kali_Linux_2020" {111bc269-c859-493b-b635-a1eb55df04df}
"Windows10_Education_64" {51c75547-283f-40d1-928c-1485db02d6f1}
```
If you have running VM's Shut them down before adding the external authentication method for Virtual Box 
 
```
$ VBoxManage controlvm "VM_Name" poweroff
```
Enable VBoxAuthSimple with the following command 
```
$ VBoxManage setproperty vrdeauthlibrary "VBoxAuthSimple"
```
 To enable the library for a particular VM, you must switch authentication to external, as follows
```
$ VBoxManage modifyvm VM-name --vrdeauthtype external
```

Replace VM-name with the VM name or UUID.
 
You then need to configure users and passwords by writing items into the machine's extradata. Since the XML machine settings file, into whose extradata section the password needs to be written, is a plain text file, Oracle VM VirtualBox uses hashes to encrypt passwords. The following command must be used

```
$ VBoxManage setextradata VM-name "VBoxAuthSimple/users/user" hash
```
Replace VM-name with the VM name or UUID, user with the user name who should be allowed to log in and hash with the encrypted password. The following command example obtains the hash value for the password secret
```
$ VBoxManage internalcommands passwordhash "secret"
2bb80d537b1da3e38bd30361aa855686bde0eacd7162fef6a25fe97bf527a25b
```
You then use VBoxManage setextradata to store this value in the machine's extradata section.

As a combined example, to set the password for the user john and the machine My VM to secret, use this command:
```
$ VBoxManage setextradata "My VM" "VBoxAuthSimple/users/john"
    2bb80d537b1da3e38bd30361aa855686bde0eacd7162fef6a25fe97bf527a25b
```

For more information view the section [7.1.5 RDP Authentication](https://www.virtualbox.org/manual/ch07.html) in this page 
