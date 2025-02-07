# Network Components:
IP : IPV4 OR IPV6 
#### Subnet mask:
> [!NOTE]
> 
>  A subnet mask is a 32-bit number that divides an IP address into network and host portions. It's used in IP networking to create subnetworks (subnets) within a larger network, allowing for efficient management and use of IP addresses.

#### Gateway :
It's essentially a **translator** between networks, enabling communication between devices on different subnetworks or networks.
**Packet Forwarding**: Forwards data packets between different networks.
#### static vs DHCP:

When configuring network settings, there are two common methods for assigning IP addresses to devices: 
==Static IP :==
**Manual Configuration**: The IP address is manually assigned to a device and remains constant.

==DHCP (Dynamic Host Configuration Protocol)==
**Automatic Configuration**: The IP address is automatically assigned by a DHCP server.

#### interface:
 it enables devices to communicate with each other over a network.
#### Interface MAC:(media access control)
The unique hardware identifier for a network interface.
mac address is hexa decimal 
MAC address is typically written as six pairs of hexadecimal digits separated by colons (e.g., 00:1A:2B:3C:4D:5E).

# Network Files & Commands:
1. Intrface Detection 
2. Assigning an IP Address
3. Interface Configuration files
        - /etc/nsswitch.conf
        - /etc/hosts :This file maps hostnames to IP addresses.
        - /etc/sysconfig/network:
        - /etc/sysconfig/network-scripts/ifcfg-nic
        - /etc/resolv.conf (specify your DNS server)
        
 Network Commands:
 - ping
 - ifconfig
 - ifup or ifdown
 - netstat
 - tcpdump :every transactions that leaving your machines and coming into your machine

 ## NIC Information:(Network interface Card)
 
its internet port behind the pc or laptop
**is a hardware component that allows a computer or device to connect to a network**
 ==ethtool    enp0s3=(interface)== ----->(imp)
 used to communicate with other system
 lo : loop-back device is special interface that your system uses to communicate to its-self, mainly used for troubleshooting and diagnostic
 
# NIC Bonding(Network interface Card):
its network bonding 
combination of multilple NIC into single bond interface
main purpose is 
==1:  high availability==:   Ensures that your network connection stays active, even if one of the NICs fails.
==2:  redundancy  :==   Provides backup paths for data to ensure continuous network service.

# New Network Utilities :

- **nmcli** stands for **Network-Manager Command Line Interface**
    --->Manage network settings without needing a graphical interface. making it suitable for servers and headless machines
    --->Create, edit, delete, activate, and deactivate network connections
    --->Control and display network device status
    
- **nmtui** stands for **Network-Manager Text User Interface**
    ---> It provides a text-based interface for managing network connections, which is useful when you don't have access to a graphical environment
    --->Manage network connections  such as activating/deactivating and editing connection settings

- **nm-connection-editor** is a graphical user interface tool for managing network connections
    ---> Add, remove, and modify network connections stored by Network-Manager

- GNOME settings

### Download Files or Apps:
Linux :   wget 
yum install putty (vm is on NAT)

# curl and ping Commands:

#### curl
**Data Transfer**: Transfer files or data between your local system and a remote server.
 **Supports Multiple Protocols**: HTTP, HTTPS, FTP, SFTP, and more.
to communicate with 1 server to another use ports
-  HTTP uses   **port 80**.
- HTTPS uses  **port 443**.
- FTP uses     **port 21**
- SCP uses  **port 22**
```
  # Download a file from a URL
curl -O http://example.com/file.txt

 # Send a POST request with data
curl -X POST -d "param1=value1&param2=value2" http://example.com/api
```

#### ping
**Network Connectivity**: Check if a host is reachable.
**Troubleshoot Network Issues**: Identify network problems such as packet loss or high latency.

```
ping   www.google.com
```

# FTP (File Transfer Protocol):

It's one of the oldest methods used to transfer files between a client and a server over a network.

![[Pasted image 20250121172847.png]]
how to transfer file:

![[Pasted image 20250121172927.png]]

# SCP (Secure Copy Protocol ):  
its more secure & authenticated method than FTP  
Transfer file from local to remote host

-r is for directory and for file we dont need to use -r
> [!NOTE]  
> scp    -r    file-name    remote-user-name@if of remote:path of remote user where file is going to send
> 

to locate path of file name if have  space 

```
cd "/home/test/Documents/Obsidian Vault"
```

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


# SSH & TELNET:  

SSH    : is more secure (secure shell )
SSHd  : (works on servers side which is on back-end, **Daemon** never stops and keep running as a process to listen requests that comes in )
Telnet : unsecured connection between computer

TO check SSH logs:
```
/etc/ssh/sshd_config
```
TO check stop /start and check status  of ssh
```  
=>systemctl stop ssh
=>systemctl start ssh
=>systemctl status ssh
```
to check that ssh process is active or not
```  
ps -ef | grep ssh 
```

 # DNS (Domain Name Server):
 
**its main purpose is** :

Host-name to IP                   ====> A Record
IP  Address to Host-name   ====> PTR Record
Host-name to Host-name    ====> CName Record
**DNS Listen on Port =  53**

Files:
==/etc/named.conf==
This file contains the settings and options that control the behavior of the DNS server.
==/var/named==( its directory have all stuff for DNS RECORDS)

Services:
==systemctl restart named==
The `named` service is responsible for translating domain names into IP addresses

Insall DNS package:
```
yum    install   bind   bind-utils  -y
```

# Host name /IP Lookup:

Commands used for DNS lookup
1. ==nslookup==
`nslookup` is a simple tool for querying DNS servers to get information about a domain name or IP address.

```
nslookup www.google.com
nslookup IP 
```
3. ==dig==
`dig` is a more versatile and powerful tool than `nslookup`, often preferred by network administrators for its detailed output and flexibility.
```
dig  www.facebook.com
dig +short  example.com
```

# NTP(Network time protocol):

=>  **Time Synchronization**: Synchronizes the system clock with highly accurate time servers.
=>  Can handle multiple time sources and automatically switch to an alternative source if the primary one fails.

services:
```
sudo systemctl start ntpd
sudo systemctl enable ntpd
```
**Configure NTP**: 
=>to add or modify time servers into file 
      ==etc/ntp.conf==

# chronyd:

**Faster Synchronization**: Provides faster initial synchronization and better handling of intermittent connections.
Designed as a modern replacement for `ntpd`, with improved features for mobile and intermittent network environments.

same as ntp , 
Purpose :                   ==>      Time Synchronization
Package Name:         ==>      chronyd
configuration file       ==>     /etc/chrontd.conf
Log File:                     ==>      /var/log/chrony
service:                      ==>      systemctl start/restart chronyd
Program Command   ==>     chronyc
# New system Utility Command:

(time+date+control)

 to view all available time-zone list:
```
  timedatectl   list-timezones
```
how to set time-zone :
```
timedatectl   set-timezone "America/New_York"
```
To set date:
```
timedatectl   set-time     year-month-day
```
To set date & time
```
timedatectl   set-time     '2015-11-20  16:14:50'
```
To automatic time synchronization with a remote NTP server
```
timedatectl  set-ntp  true
```

The command   **timedatectl   set-ntp   true** is used to enable automatic time synchronization with NTP servers on systems running **systemd**

# Sendmail:
Purpose :               ==>      Send and recieve mail
configuration file   ==>   /etc/mail/sendmail.mc , /etc/mail/sendmail.cf ,/etc/mail
service:                  ==>      systemctl   start/restart    sendmail

command:
```
mail -s  "subject line "  email@mydomain.com
```
 
 ==> yum install sendmail-
 
  **to install configuration of sendmail**
  ==>yum install sendmail-cf
  
  # Web Server (httpd):
  
Purpose :                   ==>      Serve webpages
Package Name:         ==>      httpd
configuration file       ==>   /etc/http/conf/httpd.conf = /var/www/html/index.html
Log File:                     ==>      /var/log/http/
service:                      ==>      systemctl   start/restart/enable   httpd

1. Install apache2 instead of httpd if on Ubuntu or yum install httpd  
2. /var/www/html/index.html
  1. Create a file index.html   
  2. Nano index.html  
  3. write program

<!DOCTYPE html> 

<html> 

<body > 

<br> 

<h1 style="text-align:center;">Welcome</h1> 

<br> 

<h4 style="text-align:center;">Sania</h4> 

<br> 

</body> 

</html>
5. systemctl stop firewalld
6. systemctl restart httpd
7. copy ip and search on same browser

# Central Logger (RSYSLOG):

Purpose :                   ==>      Generate logs or collect logs from other servers
Package Name:         ==>      rsyslog
configuration file       ==>     /etc/rsyslog.conf
Log File:                     ==>      /var/log/rsyslog
service:                      ==>      systemctl   start/restart/enable  rsyslog
# Linux OS Hardening:

#### User account:

Hardening user accounts on a Linux system is crucial for security. It helps to minimize the attack surface by controlling who can access the system, what they can do, and how their access is managed. Below are some common **Linux OS hardening commands** related to **user account management**:

to check details of password (last time changed etc)
```
chage -l test
```
1. **Create Strong User Passwords**  
- To enforce strong passwords for user accounts, configure password policies. This can be done using the **`/etc/login.defs`** file or by using the **`pam_pwquality.so`** module for password strength enforcement.

- **Enforce password complexity**: Edit the **`/etc/security/pwquality.conf`** or **`/etc/pam.d/common-password`** file (depending on your distribution):

```  
sudo nano /etc/pam.d/common-password  
```

modify this:  
```  
password requisite pam_pwquality.so retry=3 minlen=12 minclass=3  
```

- **Enforce password expiration**: Set a maximum password age to require users to change passwords periodically:  
```  
sudo chage -M 30 username  
```  
This will cause the password to expire after 30 days.

2. **Lock Inactive Accounts:**

- **Lock accounts that are inactive for a set period**: Use `chage` to set an inactivity period after which the account will be locked:  
```  
sudo chage -I 30 username  
```

This locks the account 30 days after the password was last changed.

- **Find inactive accounts**: Use the `lastlog` command to see the last login times for all users:  
```  
sudo lastlog  
```  
You can then disable or remove inactive accounts.

3. **Remove Unnecessary User Accounts**  
It's important to remove any unused or unnecessary user accounts to reduce the potential attack surface.

- **Delete a user account**: If you want to remove a user and their home directory:  
```  
sudo userdel -r username  
```

- **List all users on the system**: To see all user accounts, check the `/etc/passwd` file:  
```  
cut -d: -f1 /etc/passwd  
```

#### Remove Unwanted Packages:

To check how many packages you have use the following command:  
```  
rpm -qa | wc -l  
```

To remove a package use the following command:

```  
rpm -e package name  
```

#### Stop Un-Used Services:  
To see all the services use the following command:  
```  
systemctl -a  
```

#### Check On Listening Ports:  
```  
netstat -tunlp  
```

#### Secure SSH:  
```  
cd /etc/ssh/  
```

Open sshd_config file   
```  
more sshd_config  
```

From there you can change the port and you can deny root login so the users will login by their own accounts.

#### Enable Firewall:  
To open Firewall GUI use the following command  
```  
firewall-config  
```  
For command line use the following command:  
```  
firewall-cmd --help  
```

==cd   /etc/sysconfig==  
==more  iptables-config== 

==cd /etc/firewalld/==
==more firewalld.conf==

#### Enable SELinux:
it controls the permission access of process and application
its newer technology, and hard to implement
=>check running or not :
```  
sestatus  
```
=>tell us everything about file , command used :
```  
stat filename  
```

# OpenLDAP Installation:
OpenLDAP service 

OpenLDAP Service    ==>      slapd
configuration file        ==>     /etc/openldap/slapd.d
services                      ==>      systemctl   start/restart/enable  slapd

yum  install *openldap*

for ubunto install:
```
sudo apt-get install slapd ldap-utils
```

# Trace Network Traffic (traceroute):

**Traceroute** is a network diagnostic tool that traces the path of your network traffic from the source (your computer) to the destination (a server or website). It helps identify the route taken by packets across the network and highlights where delays or issues occur.

traceroute  www.google.com

1. How To Open Image File in Linux:
2. become root
3. yum install ImageMagick -y
4. display image-file

# Configure & secure SSH:

 ==>secure shell translates commands to kernel to manage hardware 
 
 kernel secures =>Hardware  
 
 SSH shell secure (bash , csh , ksh)==> kernel ==>hardware 
 ==Configure Idle Timeout Interval steps:==
 ==> become root
 ==> cp   /etc/ssh/sshd_config etc/ssh/sshd_config.org
 ==> edit your file   nano  /etc/ssh/sshd_config 
 ==> ClientAliveInterval        600
 ==> ClientAliveCountMax    0
 ==> ClientAliveInterval 600
 ==> systemctl restat sshd
 
 #### Disable Empty Passwords  
You need to prevent remote logins from accounts with empty passwords for   
added security.   
**Steps:**  
1. Become root   
2. Edit your `/etc/ssh/sshd_config `file and remove # from the following line   
3. PermitEmptyPasswords no 

```  
sudo systemctl restart ssh.service  
```

#### Limit User's SSH Access  
To provide another layer of security, you should limit your SSH logins to only certain  users who need remote access   
**Steps:**  
1. Become root   
2. Edit your `/etc/ssh/sshd_config` file and add   
3. AllowUsers user1 user2   
```  
systemctl restart sshd  
```

#### Use a different port  
Use a different port By default SSH port runs on 22. Most hackers looking for any open SSH servers will look for port 22 and changing can make the system much more secure   
**Steps**  
1. Become root   
2. Edit your /etc/ssh/sshd_config file and remove # from the following line and change the port number   
3. Port 22   
```  
systemctl restart sshd   
```

# Access Remote Server Without Password (SSH -Keys):

Two reasons to access a remote machine
- Repetitive logins
- Automation through scripts
Keys are generated at user level
- test(user)
- root![[Pasted image 20250124170345.png]]
- ssh    root@IP-remote_server
- ssh-keygen
- ssh-copy-id root@IP-remote_server
- key will generate and than again run ssh user@IP-Remote

# Cockpit:
**Cockpit** is a powerful tool used for managing and monitoring Linux servers through a simple, web-based graphical interface
Cockpit provides a web-based graphical user interface (GUI) that's easy to navigate, making server management more accessible even for those who may not be comfortable with the command line.

Enable the Cockpit repository:
```
sudo yum install epel-release
```
- yum install cockpit -y
- apt-get install cockpit
```
- systemctl start/enable cockpit
- sudo systemctl enable --now cockpit.socket
```
- https://IP-Machine(centos):9090 ==> search on firefox
     ==> **Always use HTTPS to access Cockpit to ensure secure communication.**
- systemctl stop firewalld

# Firewall:
Firewalls act as a barrier between trusted internal networks and untrusted external networks, such as the internet, to prevent unauthorized access and cyber-attacks.

### firewall (iptables):
there are 2 tools to manage firewall in most of the Linux distribution 

- ip tables = for older Linux version but still widely used
- firewalld = for newer versions like 7 and up 


**`Before Working with iptables make sure firewalld is mot running and disble it`** 

- service OR systemctl stop firewalld        ==>    to stop service
- systemctl disable firewalld  ==>      to prevent from starting at boot time
- systemctl mask  firewalld    ==> to prevent it from running by other program

=> Now check if you have iptables-services package installed:
```
rpm -qa | grep iptables-services
```
=>  to install  iptables-services
```
yum install iptables-services
```

=> Start the service:
- systemctl   start    iptables
- systemctl   enable  iptables

=> To check the iptables rules:
```
iptables -L
```

=> To flush iptables:
```
iptables -F
```
### firewall (iptables, tables, chains & targets):
The function of iptables tool is packet filtering
organized in three different kinds of structures
1. tables
2. chains 
3. targets 
###### tables :
table is something that allows you to process packets is specific ways.There are 4 different types of tables , **filter , mangle , nat and raw** 
###### chains : 
chains are attached to tables, these chains allow you to inspect traffic at various points. There are 3 main chains used in iptables
- INPUT           =     incoming traffic
- FORWARD    =      going to a router, from one device to another
- OUTPUT       =      outgoing traffic

    -=> chains allow you to  filter traffic by adding rules to them 
    -=> ==Rule:== if traffic coming from (this IP) then go to defined target 
###### targets :
target decides the fate of a packet, such as allowing or rejecting it. There are 3 different types of targets
- ACCEPT    =    connection accepted 
- REJECT     =  send reject response
- DROP         =   drop connection without sending any response![[Pasted image 20250127125748.png]]
### Firewall (firewalld):

works the same way as iptables , nut have different commands 
==firewall-cmd==
Firewalld also has the following:
Table 
chains
Rules 
Targets

=> follow all steps same as iptables to enable
=> To check the  rules of firewalld: to check all list
```
firewall-cmd --list-all
```

=> get the listings of all services firewalld is aware of:
```
firewall-cmd --get-services
```

=>To make firewalld re-read the configuration added:```
```
firewall-cmd --reload
```

=> The firewalld has multiple zone, to get a list of all zones or for public-zone
```
firewall-cmd   --get-zones
firewall-cmd   --get-active-zones
firewall-cmd   --zones=public   --list-all
firewall-cmd --list-all
```

=> All services are pre-defined by firewalld. What if you want to add 3rd party service

   **/usr/lib/firewalld/services/allservices.xml**   
  
   **Simply cp any .xml file and change the service and port number**
    
=> To add a service (http) / To remove service
```
firewall-cmd  --add-service=http
firewall-cmd  --remove-service=http
```
=> permanently remove or add
```
firewall-cmd  --add-service=http --permanent
firewall-cmd  --remove-service=http --permanent
```
    
  => **To add a service that is not pre-defined by firewalld**
  
  - /usr/lib/firewalld/services/allservices.xml
  
   - Simply cp any .xml file sap.xml and change the service and port number (32)
     
   - systemctl restart firewalld
  
   - firewall-cmd --get-services (to verify new service)  
  
   - Firewall-cmd --add-service=sap   
  
=> **To add a port**   
  
   firewall-cmd --add-port=1110/tcp  (select random port)
  
=>**To remove a port**   
  
   firewall-cmd --remove-port=1110/tcp   
  
=> **To reject incoming traffic from an IP address**   
  
   firewall-cmd --add-rich-rule='rule family="ipv4" source address=“192.168.0.25"  reject’ 
  
=> **To block and unblock ICMP incoming traffic**   
  
   firewall-cmd --add-icmp-block-inversion   
  
   firewall-cmd --remove-icmp-block-inversion  
  
=> **To block outgoing traffic to a specific website/IP address**   :
```  
host -t a [www.facebook.com](https://www.facebook.com "https://www.facebook.com/") = find IP address   
```

```  
firewall-cmd --direct --add-rule ipv4 filter OUTPUT 0 -d 31.13.71.36 -j DROP  
```

# Tune System Permanence:
Tuning system performance means optimizing various system settings and configurations to make your system run more efficiently and effectively for specific workloads or general use. This involves adjusting parameters to enhance speed, responsiveness, resource utilization, and stability. In essence, it's about making your system perform at its best given the tasks it's handling.

==>  check package:
==rpm -qa | grep tuned==

==>  install:
==yum install tuned==

==>  check service status 
==systemctl   status|enable|start  tuned==

==>  command to change setting for tuned daemon
==tuned-adm== 

==>  check which profile is active
==tuned-adm  active==

==>  To list available profiles
==tuned-adm  list==

==>  To change to desired profile
==tuned-adm  profie   profile-name

==>  check for tuned recommendation
==tuned-adm  recommend==

==>  Turned off tuned setting daemon
==tuned-adm off

==>  change profile through web-browser
==https : // ip-address:9090==

#### nice & renice:
with nice and renice commands we can make the system to give prefrence to certain processes than others

nice level values from -20(highest priority) to 19(lowest priority)

==> process priority can be viewed through ps command as:
```
ps axo pid,comm,nice,cls --sort=nice
```

==>To set the process priority:
```
nice   -n  -15  process-name
```

==> To change the process priority
```
renice  -n    12   PID
```

# Run Containers:
Building , Running  & Managing containers

==> To install podman:
**yum install podman -y**

==> check podman version
**podman -v**

==> check podman environment and registry
**podman info**

==> To search specific image in repository
**podman search httpd**

==>To check any previous downloaded image 
**podman images**

==>To download available images
**podman  pull  docker. io/library/httpd**

==>To list podman running containers 
**podman  ps**

==>To run a download httpd containers
**podman  run  -dt  -p  8080:80/tcp  docker. io/library/httpd**
 (d=detach , t=get the  tty shell , p=port)
 
go to web-browser =localhost:8080

==>To view logs:
**podman  logs   -l**

==>To stop or start a running container (by running ps podman)
**podman   stop/start   container-name**

==>To run multiple  httpd containers:
**podman  run  -dt  -p  8081:80/tcp  docker. io/library/httpd**
**podman  run  -dt  -p  8082:80/tcp  docker. io/library/httpd**

==>To create a new container  from downloaded image:
**podman create --name  httpd  docker. io/library/httpd**

==Manage container through systemd==
==> first you have to generate a unit file :
**podman generate systemd   --new  --file  --name  httpd** 

==> Copy it systemd directory:
**cp   /root/container-httpd.services  /etc/systemd/system**

==> Enable the service
**systemctl  enable container-httpd.services**

**systemctl  start container-httpd.services**

# Kickstart =>Automated Installation:

=> Kickstart allows you to automate the installation process, reducing the need for manual intervention
=> Manual installation ke mukable, Kickstart automated installations significantly faster hoti hain, especially for repetitive installations.
=> Kickstart enables you to scale installations across large environments effortlessly.

Using Kickstart for automated installations in Linux involves several steps to create, customize, and deploy the Kickstart file
1. Create a Kickstart File
2. Make a Kickstart file available on  a network location
3. Make installation source available 
4. Make boot media available for client which will be used to begin  in the installation
5. Start the Kickstart installation

```
yum install  system-config-kickstart
```
or use 
==/root/anaconda-ks.cfg==

==> install http package
             ==rpm -qa | grep http==
             ==yum install httpd==
 1. cp /root/anaconda-ks.cfg  /var/www/html
 2. cd  /var/www/html
 3. chmod  a+r   anaconda-ks.cfg
 4. systemctl  stop|disable  firewalld
 5. check file through browser  http: //IP of centos/anaconda-ks.cfg

# DHCP :
- Dynamic Host Configuration Protocol
- Automatically assign IP addresses t o servers ,laptops, desktops and others
- This is especially useful in environments where devices frequently connect and disconnect from the network, like in large offices or home networks.

==nmtui  to manually  assign a static IP== 
yum install dhcp
start and enable dhcp service

firewall-cmd  --add-service=dhcp  -permanent
firewalld-cmd  -reload
