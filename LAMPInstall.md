Linux,Apache,MongoDB,Php(LAMP) Installation
====
Introduction
----
Usually LAMP stack means Linux, Apache, MySQL & Php. In my case I have installed NoSQL database instead of MySQL relational database. Lets see how I installed the lamp stack on my Centos Linux machine

Check Installation of Apache
----
Centos by default has Apache installed. You just need to verify if it is enabled or not 
```
rpm -q httpd
```
To check run staus 
```
/sbin/service httpd status
```
or 
```
systemctl status httpd
```
![Run Status](FlowImages/LAMPInstall/Runstatus.drawio.svg)

Installation of PHP
----

