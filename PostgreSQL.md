I have used this tutorial in this Link https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-centos-8 to install PostgreSQL in my CentOS. 
I have noted down the steps which worked on my machine

Step-1 Installing PostgreSQL
=====
List out the available streams available for the *postgresql* module using the *dnf* command:
```
[root@saranyan ~]# dnf module list postgresql
Last metadata expiration check: 3:53:31 ago on Thu 11 Feb 2021 06:56:33 PM CST.
CentOS Stream 8 - AppStream
Name                        Stream                  Profiles                Summary                                             
postgresql                  9.6                     client, server [d]      PostgreSQL server and client module                 
postgresql                  10 [d]                  client, server [d]      PostgreSQL server and client module                 
postgresql                  12                      client, server [d]      PostgreSQL server and client module                 
postgresql                  13                      client, server [d]      PostgreSQL server and client module 
```
I have installed the default version 10
marked by [d] in the stream column 

```
$ dnf install postgresql-server
[root@saranyan ~]# dnf install postgresql-server
Last metadata expiration check: 4:00:16 ago on Thu 11 Feb 2021 06:56:33 PM CST.
Dependencies resolved.
============================================================================================================================================
 Package                          Architecture          Version                                              Repository                Size
============================================================================================================================================
Installing:
 postgresql-server                x86_64                10.15-1.module_el8.4.0+579+22c56897                  appstream                5.0 M
Installing dependencies:
 libpq                            x86_64                13.1-1.el8                                           appstream                197 k
 postgresql                       x86_64                10.15-1.module_el8.4.0+579+22c56897                  appstream                1.5 M
Enabling module streams:
 postgresql                                             10                                                                                 

Transaction Summary
============================================================================================================================================
Install  3 Packages

Total download size: 6.7 M
Installed size: 26 M
Is this ok [y/N]: y
Downloading Packages:
(1/3): libpq-13.1-1.el8.x86_64.rpm                                                                          521 kB/s | 197 kB     00:00    
(2/3): postgresql-10.15-1.module_el8.4.0+579+22c56897.x86_64.rpm                                            2.9 MB/s | 1.5 MB     00:00    
(3/3): postgresql-server-10.15-1.module_el8.4.0+579+22c56897.x86_64.rpm                                     7.6 MB/s | 5.0 MB     00:00    
--------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                       5.9 MB/s | 6.7 MB     00:01     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                    1/1 
  Installing       : libpq-13.1-1.el8.x86_64                                                                                            1/3 
  Installing       : postgresql-10.15-1.module_el8.4.0+579+22c56897.x86_64                                                              2/3 
  Running scriptlet: postgresql-server-10.15-1.module_el8.4.0+579+22c56897.x86_64                                                       3/3 
  Installing       : postgresql-server-10.15-1.module_el8.4.0+579+22c56897.x86_64                                                       3/3 
  Running scriptlet: postgresql-server-10.15-1.module_el8.4.0+579+22c56897.x86_64                                                       3/3 
[/usr/lib/tmpfiles.d/pesign.conf:1] Line references path below legacy directory /var/run/, updating /var/run/pesign → /run/pesign; please update the tmpfiles.d/ drop-in file accordingly.
[/usr/lib/tmpfiles.d/postgresql.conf:1] Line references path below legacy directory /var/run/, updating /var/run/postgresql → /run/postgresql; please update the tmpfiles.d/ drop-in file accordingly.

  Verifying        : libpq-13.1-1.el8.x86_64                                                                                            1/3 
  Verifying        : postgresql-10.15-1.module_el8.4.0+579+22c56897.x86_64                                                              2/3 
  Verifying        : postgresql-server-10.15-1.module_el8.4.0+579+22c56897.x86_64                                                       3/3 
Installed products updated.

Installed:
  libpq-13.1-1.el8.x86_64                                                  postgresql-10.15-1.module_el8.4.0+579+22c56897.x86_64            
  postgresql-server-10.15-1.module_el8.4.0+579+22c56897.x86_64            

Complete!
```

Step 2 - Creating a New PostgreSQL Database Cluster 
====
```
[root@saranyan ~]# postgresql-setup --initdb
 * Initializing database in '/var/lib/pgsql/data'
 * Initialized, logs are in /var/lib/pgsql/initdb_postgresql.log
[root@saranyan ~]# systemctl start postgresql
[root@saranyan ~]# systemctl enable postgresql
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /usr/lib/systemd/system/postgresql.service.
[root@saranyan ~]# 
```
Step 3 - Using PostgreSQL Roles and Database
====
```
[saranyans@saranyan ~]$ sudo -i -u postgres
[sudo] password for saranyans: 
[postgres@saranyan ~]$ psql
psql (10.15)
Type "help" for help.

postgres=# \q
[postgres@saranyan ~]$ exit
logout
[saranyans@saranyan ~]$ sudo -u postgres psql 
could not change directory to "/home/saranyans": Permission denied
psql (10.15)
Type "help" for help.

postgres=# \q
[saranyans@saranyan ~]$ 
```


