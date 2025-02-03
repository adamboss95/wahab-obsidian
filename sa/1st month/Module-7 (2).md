# SCP (Secure Copy Protocol ):  
its more secure & authenticated method than FTP  
Transfer file from local to remote host

> [!NOTE]  
> scp    -r    file-name    remote-user-name@if of remote:path of remote user where file is going to send

```  
scp -r sania ummehabiba@10.10.10.66:/home/ummehabiba  
```

# rsync – Remote Synchronization:
- rysync is mostly used to transfer files efficiently and synchronizing files within same computer or to remote computer by comparing modification times and size of files  
- It is alot faster than ftp and is used to create backup for files and directories.  
- Default rsync port=22(same as SSH)  
**Commands:**  
1. First create a backup.tar file using the following command:  
```  
tar cvf backups.tar .  
```  
2. After creating a directory in `/tmp/backups` we will transfer backup file in it using the following command:  
```  
sudo rsync -zvh backups.tar /tmp/backups  
```  
3. Now if you want to create backup on a remote server you will use the following command:  
```  
sudo rsync -avz backups.tar habiba@10.10.10.60:/tmp/backups  
```

4. Now if you want to fetch a file from remote server you will use the following command:  
```  
sudo rsync -avzh habiba@10.10.10.60:/home/habiba/sania /tmp/backups

```

# System Updates & Repos:
Imp topic for installing new packages in system
 
 => yum for (CentOs) 
 (downloading package and installing package )
 => rpm(Red hat Package Manager)
```
 yum install bind
```
 to check we have a package installed , command used 
```
   rpm -qa  |  grep bind
```
 to remove package 
```
 yum remove bind
```

# System Upgrade/Patch Management:
Two Types of Upgrades
Major version  = 5,6,7
Minor version = 7.3 to 7.4
==yum update -y==
to install rpm package :
==rpm -hiv package_name==

- upgrade :will delete all old packages
- update  : preserves old packages

to check version in linux we use the following command:
```  
lsb_release -a  
```

To update packages use the following command:  
```
apt update
```  
# Create Local Repository from DVD:

COMMMAND:
==>createrepo
Speeds up the process of installing and updating software, as accessing files from a local source is faster than downloading them.

# Advance Package Management:
most preferred way to install package :

```
yum install  ksh*(packagde name)
```
To check package is installed or not 
```
rpm   - qa |   grep   ksh
```
to remove package:
```
yum remove  ksh* (package-name)
```

if you dont have internet 
```
 wget   location of package
```
to check list of configuration  file 
```
rpm  -qc  package-fullname
```

to check path of package:
==which   ksh==

```
rpm   -qf   package-fullpath
```

# Rollback Update and Patches:
```
yum install  package-name
```

==>to undo history command used

```
yum  history  undo  id
```

