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

# OpenLDAP Insallation:
OpenLDAP service 

OpenLDAP Service    ==>      slapd
configuration file        ==>     /etc/openldap/slapd.d
services                      ==>      systemctl   start/restart/enable  slapd

yum  install *openldap*

for ubunto install:
```
sudo apt-get install slapd ldap-utils
```

# Trace Network TRaffic (traceroute):

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

