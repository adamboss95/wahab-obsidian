# SSH & TELNET:  

SSH    : is more secure (secure shell )
SSHd  : (works on servers side which is on back-end, **Daemon** never stops and keep running as a process to listen requests that comes in )
Telnet : unsecured connection between computer
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
DNS Listen on Port =53

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
configuration file    ==>   /etc/http/conf/httpd.conf = /var/www/html/index.html
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
