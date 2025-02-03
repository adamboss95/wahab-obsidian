##### Jan 20, 2025
# SOC Analyst Training
## Linux Training

# Module 7

### Enabling internet on Linux VM
1. Open Virtual box Manager 
2. Select the machine you cannot get internet on in the left pane 
3. Click the settings button in the top menu 
4. Click Network in the left pane in the settings window 
5. Switch to Bridged Adaptor in the Attached to drop-down menu 
6. Hit OK to save your changes 
7. Start your VM 
8. After setting your VM, go to terminal and type the code to check if its working
```
ping [www.google.com]
```

### Network Components
- **IP** = Internet Protocol

- **Subnet mask** = A 32-bit number that separates an IP address into network and host portions.

- **Gateway** = A device that acts as an entry and exit point for network traffic e.g. modem is a gateway between our systems and server

- **Static vs DHCP**
	- **Static** = Manually assigned IP address that remains constant.
	- **DHCP** = Automatically assigns IP addresses to devices on the network.

- **Interface** = A network interface is a hardware or software component that connects a computer to a network.

- **Interface MAC** = A MAC address is a unique identifier assigned to a network interface controller (NIC) for use as a network address in communications within a network segment.

### Network Files and Commands
- There are many network files and commands used to configure that is used to communicate one machine to another 
    
- Interface Detection

![[Pasted image 20250121101758.png]]

- Assigning an IP address
    
- Interface configuration files 
	- 1. /etc/nsswitch.conf (tells its system where it should resolve its hostname to IP address) 
	- /etc/hostname
	- /etc/sysconfig/network (this directory is not available in ubuntu)
	- /etc/sysconfig/network-scripts/ifcfg-nic 5 (this directory is not available in ubuntu)
	- /etc/resolv.conf 

- Network Commands
	- ping
	- ifconfig
	- ifup or ifdown (ifup enables the network, if down disables)
	- netstat (useful for monitoring and troubleshooting network issues)
	- tcpdump (sniffing command)

### NIC Information
- NIC = Network Interface Card e.g: ethtool eno1

![[Pasted image 20250121113323.png]]

- Other NICs you can see by running command ifconfig 
    
- lo = the loopback device is a special interface that your computer uses to communicate with itself. It is used mainly for diagnostics and troubleshooting and to connect to servers running on the local machine 
    
- virbr0 = The virbr0 or "Virtual Bridge 0" interface is used for NAT(Network Address Translation). Virtual environments sometimes use it to connect to the outside network.  

- You can get you ethtool enp by running ifconfig 

- After running the command ethtool enp2s0 there are few things you need for network administrator  
	1. Link mode: 1000baseT/Full 
	2. Speed: 1000Mb/s 
	3. Duplex: Full


### NIC Bonding or Port Bonding
- NIC (Network Interface Card) attached to your PC or Laptop 
    
- NIC bonding is like combining multiple internet connections into one super connection. It makes your network faster and more reliable by using multiple network cards together. 
    
- Its main purpose is to provide high availability and redundancy.
 ![[Pasted image 20250121120437.png]]
**Creating NIC Bonding**
- Add a new NIC if it does not exist
- Install bonding driver = modprobe bonding
- To list the bonding module info = modinfo bonding
		You will see the driver version as seen below if the driver is installed and loaded
		
![[Pasted image 20250121152622.png]]

**Create Bond Interface File**
-  vi /etc/sysconfig/network-scripts/ifcfg-bond0
- Add the following parameters
		DEVICE=bond0
		TYPE=Bond
		NAME=bond0
		BONDING_MASTER=yes
		BOOTPROTO=none
		ONBOOT=yes
		IPADDR=192.168.1.80
		NETMASK=255.255.255.0
		GATEWAY=192.168.1.1
		BONDING_OPTS=”mode=5 miimon=100”
- Save and exit the file
- Edit the First NIC File (enp0s3)
- vi /etc/sysconfig/network-scripts/ifcfg-enp0s3
- Delete the entire content
- Add the following parameters
		TYPE=Ethernet
		BOOTPROTO=none
		DEVICE=enp0s3
		ONBOOT=yes
		HWADDR=”MAC from the ifconfig command”
		MASTER=bond0
		SLAVE=yes
- Save and exit the file

**Create the Second NIC File (enp0s8) or Copy enp0s3**
- vi /etc/sysconfig/network-scripts/ifcfg-enp0s8
- Add the following parameters
		TYPE=Ethernet
		BOOTPROTO=none
		DEVICE=enp0s8
		ONBOOT=yes
		HWADDR=”MAC from the ifconfig command”
		MASTER=bond0
		SLAVE=yes
- Save and exit the file

**Restart the Network Service**
- systemctl restart network
- Test and verify the configuration
- ifconfig or ifconfig | more
Use following command to view bond interface settings like bonding mode & slave interface
- cat /proc/net/bonding/bond0

**Check,  Poweroff, Restore Snap**
- Check bond0 IP is MASTER and enp0's IP is SLAVE 
- Power off the VM 
- Click and Restore snapshot


### New Network Utitilities
- Gettings started with Network Manager 
    
- Network configuration methods 1. nmtui 2. nmcli 3. nm-connection-editor 4. GNOME Settings 
    
- Network Manager is a service that provides set of tools designed specifically to make it easier to manage the networking configurations on Linux system and us the default network management service on RHEL 8 and RHEL 9 
    
- It makes network management easier 
    
- It provides easy setup of connection to he user 
    
- NetworkManager offers management through different tools such as GUI , nmtui and nmcli

**Network Configuration Methods:** 
- Nmcli – short for network manager command line interface. This tool is useful when access to a graphical environment is not available and can also be used within scripts to make network configuration changes 
    
- nmtui – short for network manager text user interface. This tool can be run within any terminal window and allows changes to be made by making menu selections and entering data 
    
- nm-connection-editor – A full graphical management tool providing access to most of the NetworkManager configuration options. It can only be accessed through desktop or console 
    
- GNOME Setting – The network screen of the GNOME desktop settings application allows basic network management tasks to be performed 
    

**Practical Work: Use nmtui** 
1. Open VM and add snapshot  
    
2. Now Enable network adaptor 2nd and attach to Bridge Adaptor 
    
3. Start the VM 
    
4. Open terminal and login as root 
    
5. ifconfig to check 2 adaptors are active 
    
6. `nmtui`  
    
7. An text editor will open and select edit connection 
    
8. Delete wired connection 
    
9. Now move cursor and back to editor and quit 
    
10. `ifconfig | more` and check adaptor 1 has IP and adaptor 2 has no IP 
    
11. `nmtui` and edit connection and delete Ethernet enp2s0 and make sure only bridge is present rest will be deleted 
    
12. Back and Quit editor 
    
13. `ifconfig` and check the IP is deleted because we deleted it 
    
14. `nmtui` and edit connection now add a Team 
    
15. After selecting Team it will ask for profile name  
    
16. Profile name Team1 
    
17. Now add the Slaves and new connection will be Ethernet 
    
18. Profile name and device name will be adaptor name in my case its enp2s0 
    
19. Ok after giving name of adaptor 
    
20. Add another Slave new connection Ethernet 
    
21. Fill Profile and device name of 2nd adaptor and OK 
    
22. If you want to give a static IP you will in the IPv4 and hit show and there is Addresses where you can add a IP 
    
23. I am not selecting IP manually and go will automatic IP and it OK 
    
24. Now I can see that my Team1 is present in Team 
    
25. Back and Quit 
    
26. Now if you will ifconfig you will see nm-team which will show you your Ethernet information 
    

**Manage Linux Networking using nmcli to configure static IP:** 
- nmcli device (Get the listing of network interface) 
    
- nmcli connection modify enp20s ipv4.addresses 10.10.10.56/24(IP no one is using) 
    
- nmcli connection modify enp2s0 ipv4.gateway 10.10.10.60 
    
- nmcli connection modify enp2s0 ipv4.method manually 
    
- nmcli connection modify eno2s0 ipv4.dns 8.8.8.8 
    
- nmcli connection down enp2s0 && nmcli connection up enp2s0 
    
- ip address show enp2s0  
    

**Manage Linux Networking Adding secondary static IP using nmcli:** 
- `nmcli device status` 
    
- `nmcli connection show-active` 
    
- `ifconfig` 
    
- `nmcli connection modify enp2s0 +ipv4.addresses 10.10.10.56/24` 
    
- `nmcli connection reload` 
    
- `systemctl reboot `
    
- `ip address show`

### Download Files or Apps

- Example of Windows browser Google 
    
- Linux = wget e.g: `wget http://website.com/filename` 
    
- Why Most of the servers in corporate environment do not have internet access 
    
- Just copy image/file link and paste in you terminal with wget link

### Curl and Ping Commands
- Example of Windows brower Google 
    
- Linux = curl – it is used for url 
    
- Linux = ping – it is used to check for server is up or not 
    
- Example: `curl http://website.com.filename` , `curl –o http://website.com/filename`, `ping www.google.com`

### FTP - File Transfer Protocol
- The FTP is a standard network protocol used for the transfer of computer files between client and server on a computer network. FTP is built on a client server model architecture using separate control and data connections between the client and the server. 
    
- Protocol = set of rules used by computer to communicate 
    
- Default FTP Port = 21 
- Default SSH Port = 22 
- Default DNS Port = 53

![[Pasted image 20250122112633.png]]


**Install and Configure FTP on the remote server** 
1. Become root
2. `rpm –qa | grep ftp` 
3. `ping [www.google.com]` 
4. `dnf install vsftpd` ==(dnf is the next generation package installer, yum can also be used to install)==
5. `vi /etc/vsftpd/vsftpd.conf`  (make copy first) 
6. Find the following lines and make the changes as shown below: 
	1. Disable anonymous login anonymous_enable=NO 
	2. Uncomment ascii_upload_enable=YES ascii_download_enable=YES 
	3. Uncomment (Enter you welcome message)(optional) ftpd_banner=Welcome to UNIXMEN FTP service 
	4. Add at the end of this file use_localtime=YES 
7. `systemctl start vsftpd` 
8. `systemctl enable vsftpd` 
9. `systemctl stop firewalld` 
10. `systemctl disable firewalld` 
11. useradd wahab (if user does not exist) 

**Install FTP client on the client server** 
1. become root 
2. dnf install ftp 
3. su – wahab 
4. `touch kruger` 
    
**Commands to transfer file to the FTP server:** 
1. `ftp 192.168.56.102 `
2. Enter username and password 
3. bin 
4. hash 
5. put kruger 
6. bye (to exit ftp)

- The file is sent successfully.

### SCP - Secure Copy Protocol
- The SCP helps to transfer computer file securely from a local to a remote host. It is somewhat similar to FTP but it add security and authentication. 
    
- Protocol = set of rules used b computer to communicate 
    
- Default SCP Port = 22 (same as SSH)

![[Pasted image 20250122124728.png]]

- SCP commands to transfer file to the remote server: 
    
- Login as yourself (wahab) 
    
- `touch jack `
    
```
scp jack wahab@192.168.56.102:/home/wahab 
```
    
- Enter password


### rsync – Remote Synchronization 
- It is same as SCP but it works in a way that suppose 1 file is transfer it's of 2 gig and again its transfer this time file is 4 gig so the one 2 gig updated file data will be transferred. 
    
- rsync is a utility for efficiently transferring and synchronizing files within the same remote computer by comparing the modification times and size of files. 
    
- rsync is a lot faster that ftp or scp. 
    
- This utility is mostly used to backup the files and directories from one server to another. 
    
- Default rsync Port = 22 (same as SSH)

![[Pasted image 20250122144925.png]]


**Basic syntax of rsync command** 
- rsync options source destination 
- `Install rsync in your Linux machine` (check if it already exists) 
- `yum install rsync` (On CentOS/Redhat based systems) 
- `apt-get install rsync` (On Ubuntu/Debian based systems) 

**rsync a file on a local machine** 
- `tar cvf backup.tar .` (tar the entire currently open directory /home/wahab) 
- `mkdir /tmp/backups` 
- `rsync -zvh backup.tar /tmp/backups/` 

**rsync a directory on a local machine** 
- `rsync -azvh /home/wahab /tmp/backups/` 

**rsync a file to a remote machine** 
- `mkdir /tmp/backups` (create /tmp/backups dir on remote server) 
- `rsync -avz backup.tar wahab2@192.168.56.102:/tmp/backups` 

**rsync a file from a remote machine** 
- `touch serverfile` (create directory on the remote machine)
- `rsync -avzh wahab2@192.168.1.x:/home/wahab/serverfile /tmp/backups`

### System Updates and Repos 
- yum (CentOS), apt-get (other Linux) 
    
- rpm (Red hat package Manager)

### System Update/Patch Management 
**Two types of upgrades** 
- Major version = 5,6,7 
- Minor version = 7.3 to 7.4  
- Major version = yum command (NO, yum command doesnt update or upgrade major version) 
- Minor version = yum update (yes, yum command can update or upgrade minor version)  Example: `yum update –y`

![[Pasted image 20250122154755.png]]


### Create Local Repository from DVD

![[Pasted image 20250122163002.png]]

- Command for creating local repository `createrepo`

**Practical Work:** 

	1. Open VM 
	    
	2. Take snapshot (name snapshot your date) 
	    
	3. Start machine 
	    
	4. Become root 
	    
	5. Devices -> choose disk -> choose iso image 
	    
	6. It will create a icon on your desktop 
	    
	7. Create directory in cd/ 
	    
	8. mkdir localrepo 
	    
	9. cd /run/media/username[ruhabqureshi] 
	    
	10. In ISO image there will be spaces and to fill it run command 
	    
	11. cd /run/media/username/[hit tab and file name will be auto filled without spaces] 
	    
	12. pwd 
	    
	13. cd packages/ [there all rpm are] 
	    
	14. ls –ltr | wc –l [amount of packages] 
	    
	15. du –sh . [show space of current directory] 
	    
	16. df –h [to see detail space available] 
	    
	17. cp –rv /run/media/ruhabqureshi/filename [copy every rpm] 
	    
	18. rm –rf /etc/yum.repos.d/* [remove everything and make sure you created a snapshot] 
	    
	19.  ls –ltr [check everything is deleted] 
	    
	20. vim local.repo 
	    
	21. edit and add this in the local.repo
	    [centos9] 
		name=centos9 
		baseurl=file:///localrepo/ 
		enabled=1 
		gpgcheck=0 
	    
	22. Save the vi file 
	    
	23. Install if not already yum install createrepo 
	    
	24. createrepo /localrepo/ [it will tell you number of packages available] 
	    
	25. yum clean all [it will clean previous cache] 
	    
	26. yum repolist all [show full list of repo] 
	    
	27. yum install tomcat [just to check installation]

### Advance Package Management
- Install packages 
    
- Upgrading packages 
    
- Deleting packages 
    
- View details information about packages 
    
- Identify source or location information  
    
- Package configuration files

The **rpm** command is a powerful tool used primarily in Red Hat-based Linux distributions like Fedora, CentOS, and Red Hat Enterprise Linux. It stands for Red Hat Package Manager and allows users to manage software packages. 

Here are some of the key functions of the rpm command:
1. Install Packages: You can install software packages using the -i option. 
	`sudo rpm -ivh package_name.rpm`   

2. Upgrade Packages: The -U option allows you to upgrade an existing package. 
	`sudo rpm -Uvh package_name.rpm`   

3. Remove Packages: To remove a package, use the -e option. 
	`sudo rpm -e package_name`   

4. Query Packages: You can query the package database to get information about installed packages using the -q option. 
	`rpm -q package_name`   

5. Verify Packages: The -V option helps verify the integrity of installed packages. 
	`rpm -V package_name`   

6. List Files in a Package: The -l option lists all files in a package. 
	`rpm -ql package_name`

7. To find out which package is running the command
- needs full path of the command run which command to find the path followed by the command e.g. `which pwd`
	`rpm -qf /usr/bin/pwd`

### Rollback Updates and Patches
1. Virtual Machine – you are using 
    - Before updating create a snapshot, if something goes wrong you can always revert back 
        
2. Physical Machine

**Rollback a package or patch** 
- `yum install <package-name>` 
- `yum history undo <history-id>`
**Rollback an update** 
- Downgrading a system to mirror version (ex RHEL7.1 to RHEL7.0) is not recommended at this might leave the system in undesired or unstable state 
- `yum update` [update will preserve packages] 
- `yum upgrade` [upgrade will delete obsolete packages] ==(always use update to be safe)==
- `yum history undo <id>`


### SH and TELNET 
- Telnet = Un-secured connection between computers 
- SSH = Secured 
- Two type of packages for most of the services 

	1. Client package 
	    
	2. Server package


### Domain Name Server
Create a snapshot of your virtual machine 

• Setup: 

• Master DNS 

• Secondary or Slave DNS 

• Client 

• Domain Name = lab.local 

• IP address = My local IP address on enp0s3 

1. Install DNS package 
    
    • yum install bind bind-utils –y 
    
2. Configure DNS (Summary) 
    
    • Modify /etc/named.conf 
    
    • Create two zone files (forward.lab and reverse.lab) 
    
    • Modify DNS file permissions and start the service 
    

• Revert back to snapshot 

- Edit the Line listen-on port 53 { 127.0.0.1; }; with listen-on port 53 { 127.0.0.1; 10.10.10.56; }; 
    

- Go to the bottom of the file /etc/named.conf before include line and add 
    

zone "lab.local" IN { type master; file "forward.lab"; allow-update { none; } ; }; 

zone "1.168.192.in-addr.arpa" IN { type master; file "reverse.lab"; allow-update { none; } ; }; 

include "/etc/named.rfc1912.zones"; 

include "/etc/named.root.key"; 

- Save and Quit 
    

3. Create Zone Files in cd /var/named 
    

cd /var/named 

touch forward.lab (create forward.lab file) 

touch reverse.lab (create reverse.lab file) 

4. Modify the newly created forward.lab zone file 
    
    - Add the following lines  in forward.lab
		$TTL 86400 
		@ IN SOA masterdns.lab.local. root.lab.local. ( 
		2011071001 ;Serial
		3600 ;Refresh 
		1800; Retry 
		604800; Expire 
		86400; Minimum TTL
		) 
		@ IN NS masterdns.lab.local. 
		@ IN A 192.168.1.29 
		masterdns IN A 192.168.56.101 
		clienta IN A 192.168.56.102 
		clientb IN A 192.168.56.103
5. Modify the newly created reverse.lab zone file
    
    - Add the following line  in reverse.lab
	    $TTL 86400 
	    @ IN SOA masterdns.lab.local. root.lab.local. ( 
	    2011071002 ;Serial 
	    3600 ;Refresh 
	    1800; Retry 
	    604800; Expire 
	    86400; Minimum TTL 
	    ) 
	    @ IN NS masterdns.lab.local. 
	    @ IN PTR lab.local. 
	    masterdns IN A 192.168.1.29 
		158 IN PTR masterdns.lab.local. 
		102 IN PTR clienta.lab.local. 
		103 IN PTR client.lab.local. 
        
6. Start the DNS Server 
	`systemctl start named` 
	`systemctl enable named` 
    
7. Disable firewalld 
	`systemctl stop firewalld` 
	
	`systemctl disable firewalld` 

8. Configuring permissions, ownership and SELinux 
	`chgrp named –R /var/named` 
	
	`chown –v root:named /etc/named.conf `
	
	`restorecon –rv /var/named` 
	
	`restorecon /etc/named.conf` 


9. Test DNS configuration and zone files for any syntax errors 
	`named-checkconf /etc/named.conf` 
	
	`named-checkzone lab.local /var/named/forward.lab` 
	
	`named-checkzone lab.local /var/named/reverse.lab` 

10. Add DNS server information to network file 
	`vi /etc/sysconfig/network-script/ifcfg-enp0s8` 
	DNS=192.168.56.101 
    
11. Modify /etc/resolv.conf 
	`vim /etc/resolv.conf`
	nameserver 192.168.56.101 
    
12. Restart network service 
	`systemctl restart network` 
	
13. Go and edit reslov.conf and change the name server
	nameserver 192.168.56.101 ==(after restarting network nameserver go back to its default so need to change)==
    
14. Test DNS Server 
	dig masterdns.lab.local 
	nslookup masterdns.lab.local (forward check hostname to ip)
	nslookup clienta.lab.local (forward check hostname to ip)
	nslookup clientb.lab.local (forward check hostname to ip)
	nslookup 192.168.1.240 (reverse check ip to hostname)
	nslookup 192.168.1.241 (reverse check ip to hostname)


### Hostname /IP Lookup
- Commands used for DNS lookup 
	1. nslookup 
	2. Dig

1. Nslookup: 
    
	- The nslookup command is used to query DNS servers and obtain domain name or IP address mapping information. It can operate in both interactive and non-interactive modes: 
	    
	- Interactive Mode: Allows you to query multiple DNS records in a single session. 
	    
	- nslookup   
	    
	- Then, you can type domain names to get their IP addresses. 
	    
	- Non-Interactive Mode: Used for single queries. 
	    
	- nslookup example.com   
	    
	- You can also specify the type of DNS record you want to query, such as A, MX, or NS records
	
2. Dig: 
    
	- The dig (Domain Information Groper) used for its advanced features and flexibility. It allows for detailed and customizable DNS querie
	    
	- Basic Query: Retrieves information about a domain. 
	    
	- dig www.hotmail.com   
	    
	- Query Specific Record Types: You can specify the type of DNS record you want to query, such as A, MX, or TXT. 
	    
	- dig example.com MX   
	    
	- Short Output: Provides a concise output. 
	    
	- dig +short example.com   
	    
	- dig -x 192.168.1.1   
	    
	- The dig command is known for its detailed output, which includes information about the query time, server used, and more


### NTP - Network Time Protocol

- Purpose? 
	Time synchronization 

- File 
	/etc/ntp.conf 

- Service 
	systemctl restart ntpd 

-  Command 
	ntpq 

- Practical Work: 
	1. Login as root 
	    
	2. Run command rpm –qa | grep ntp to check ntp package is install or not 
	    
	3. If your ntp package is not install then install it by apt install ntp or ntpq 
	    
	4. Now you have to do some changes in vi /etc/ntp.conf 
	    
	5. Add service 8.8.8.8  
	    
	6. Save and exit file 
	    
	7. Not start service by systemctl start ntpd 
	    
	8. To enable service – systemctl enable ntpd 
	    
	9. To check status of service its running or not – systemctl status ntpd 
	    
	10. ntpq will bring you in Intractive mode  
	    
	11. Type peers and it tells you which server you are connected to get your time 
	    
	12. Type exit to exit intractive mode


### Chronyd
21. Chronyd 
    

- Chronyd is the latest version to replace ntpd 
    
- Purpose?
	time synchronization
- Package name
	chronyd
- Configuration file
	/etc/chronyd.conf
- Log file
	/var/log/chrony
- Service
	Systemctl start/restart chronyd
- Program command
	`chronyc`
    

- Practical Work: 
    
	1. Become root 
	    
	2. Check package `chronyd by rpm –qa | grep chrony` 
	    
	3. If not install then `dnf install chrony` 
	    
	4. `vim /etc/chrony.conf `
	    
	5. Go to line pool 2.centos.pool.otp.org.. and below add new line server 192.168.56.102 iburst
	    
	6. Save and exit file 
	    
	7. Check service is running `systemctl status chronyd` 
	    
	8. Don’t start ntp and chrony at the same time if ntp is running stop it and then run chrony systemctl start chronyd ==(centos9 theres no ntp)==
	    
	9. Chronyc will bring you in interactive mode 
	    
	10. Check server by typing sources ==(alternate `chronyc sources` does the same)==
	    
	11. To exit type quit 
	    
	12. Modify file vim /etc/chrony.conf back to what it originally was by deleting what we did at 5.
	    
	13. Restart every time when modify file by `systemctl restart chronyd`


### New System Utility Command (`timedatectl`)

- The timedatectl command is a new utility for RHEL/CentOS 7/8 based distributions, which comes as a part of the systemd system and service manager 

- It is a replacement for old traditional date command 

- The timedatectl command shows/change date, time, and timezone 

- It synchronizes the time with NTP server as well 

- You can either use chronyd or ntpd and make the ntp setting in timedatectl as yes 

- Or we can use systemd-timesyncd daemon to synchronize time which is a replacement for ntpd and chronyd 

Please note: 
	Redhat/CentOS does not provide this daemon in its standard repo. You will have to download it separately. 

- Practical work: 

	- To check time status 
	
		timedatectl 
	
	- To view all available time zones 
	
		timedatectl list-timezones 
	
	- To set the time zone 
	
		timedatectl set-timezone “America/New_York“ 
	
	- To set date 
	
		timedatectl set-time YYYY-MM-DD 
	
	- To set date and time 
	
		timedatectl set-time '2015-11-20 16:14:50’ 
	
	- To start automatic time synchronization with a remote NTP server 
	
		timedatectl set-ntp true.


### Sendmail

Purpose? 

Send and receive emails 

- Files 

	/etc/mail/sendmail.mc [medium that receives and deliver mails] 

- vi sendmail.mc 
    
- Come to line below where written smart host 
    
- Hostname.domainname.com 
    
- Start service systemctl restart sendmail 
    

	/etc/mail/sendmail.cf 
	
	/etc/mail 

- Service 

systemctl restart sendmail 

- Command 

	1. mail –s “subject line” [email@mydomain.com]
	    
	2. type the message 
	    
	3. Crtl+D will get you out of mail program 
    

- Install packages: 
    

1. Apt install sendmail 
    
2. Apt install sendmail-cf 
    

- Sendmail is a program in Linux operating systems that allows 

	systems administrator to send email from the Linux system 

- It uses SMTP (Simple Mail Transfer Protocol) 

- SMTP port = 25 

- It attempts to deliver the mail to the intended recipient immediately and, if the recipient is not present, it queues messages for later Delivery. 

Sendmail installation and configuration 

`su –` (Login as root) 

`rpm –qa | grep sendmail` (verify if it is already installed) 

`dnf install sendmail sendmail-cf` 

`vi /etc/mail/sendmail.mc` 

`systemctl start sendmail` 

`systemctl enable sendmail` 

`systemctl stop firewalld` 

`systemctl disable firewalld`

### Web Server (httpd) 
    
- Purpose = Serve webpages 

- Service or Package name = httpd 

- Files  

	= /etc/httpd/conf/httpd.conf 
	
	= /var/www/html/index.html 

- Log Files = /var/log/httpd/ 

- Service 

	`systemctl restart httpd` 
	`systemctl enable httpd` 

Practical Work: 
1. Install httpd `dnf install httpd` 
2. Create a file index.html ==(it will only work if the file name is "index.html" for some reasons)== 
3. vim mywebpage.html 
    
- add the following lines in the mywebpage.html 

<!DOCTYPE html> 
<html> 

<body style="background-color:lightgrey;"> 

<br> 

<h1 style="text-align:center;">Good Evening Ladies and Gentlemen</h1> 

<br> 

<h4 style="text-align:center;">We are tonight's Entertainment</h4> 

<br> 

</body> 

</html> 

4. Access the file by putting ip on the web browser

5. open browser -> add the system ip and enter
6. if the web page does not display -> restart httpd and turn off firewall
		`systemctl restart httpd`
		`systemctl enable httpd`
		`systemctl stop firewalld`
		`systemctl disable firewalld`


### Central Logger (rsyslog)

- Purpose = Generate logs or collect logs from other servers 

- Port 514 
    

- Service or package name = rsyslog 

- Configuration file= /etc/rsyslog.conf 

- Service 

		systemctl restart rsyslog 
		
		systemctl enable rsyslog


![[Pasted image 20250124095701.png]]



### Linux OS Hardening

- User Account 
    
- Remove un-wanted packages 
    
- Stop un-used Services 
    
- Check on Listening Ports 
    
- Secure SSH Configuration 
    
- Enable Firewall (iptables/firewalld) 
    
- Enable SELinux 
    
- Change Listening Services Port Numbers 
    
- Keep your OS up to date (security patching) 
    

Practical Work: 

1.  To check users cat /etc/passwd 
    
2. When you create a user its user id should be above 10000 
    
3. When you create a user its name should be complex like instead of admin use tadmin or sadmin or systemdlmn, so that others dont know that this is a user account name
    
4. View last password change chage –l username 
    
5.  To check number of packages installed on your system rpm -qa 
    
6. To count number of packages installed on your system rpm -qa | wc -l 
    
7. To remove unwanted packages  `dnf remove package_name` 
    
8. Check all services active and unactive `systemctl –a` 
    
9. Check on listening ports `netstat –tunlp` 
    
10. To secure SSH go in `cd /etc/ssh/` directory and more `sshd_config | more` now change port and PermitRootLogin to No
    
11. To enable services, ports in firewall type f`irewall-config` an GUI wall open where you can made changes using GUI 
    
12. To made changes in command base type `firewall-cmd –help` and you can check options to save changes 
    
13. How to change the permission of process or application  
    
14. See SELinux status by `sestatus`

15. `stat filename` to check detail description of file size, access etc

16. Always keep upto date with the new patches by subscribing to redhat, centos or ubuntu whichever os you are using and update as soon as possible, to secure system.


### Open LDAP Installation

- It’s a protocol  
    
- Lightweight active directory protocol LDAP 
    
- Open source 
    
- Service slapd 
    
- Start service  systemctl start slapd 
    
- Enable service  systemctl slapd 
    
- Configuration files  /etc/openldap/slapd.d 
    

Practical Work: 

1. Login as root 
    
2. Install  sudo apt install slapd ldap-utils 
    
3. Path will be  /etc/ldap/slapd.d 
    
4. Go in file  more nsswitch.conf 
    
5. Passwd is etc password file


### Trace Network Traffic (traceroute)

- Learn troubleshoot network issues 
    
- Where your traffic is going 
    
- Which gateway or which DNS its going from one to another till reach its final destination 
    
- To trace the network traffic we use command `traceroute` 
    

- The traceroute command is used in Linux to map the journey that a packet of information undertakes from its source to its destination. One use for traceroute is to locate when data loss occurs throughout a network, which could signify a node that's down. 

- Because each hop in the record reflects a new server or router between the originating PC and the intended target, reviewing the results of a traceroute scan also lets you identify slow points that may adversely affect your network traffic. 

• Example 

`traceroute www.google.com`
`traceroute 192.168.56.101` (my vm ip)


### How to open an Image File
1. Install a program that will allow us to open image file 

	- ImageMagick -> install using -> `dnf install ImageMagick`

2. Command syntax to open image file in GUI 

	- `display filename.jpg`


### Configure and Secure SSH

SSH: 

- SSH stands for secure shell which provides you with an interface to the Linux system. It takes in your commands and translate them to kernel to manage hardware. 
    

- Open SSH is a package/software 

- Its service daemon is sshd 

- SSH port # 22 

![[Pasted image 20250124152238.png]]

- SSH itself is secure, meaning communication through SSH is always encrypted, but there should be some additional configuration can be done to make it more secure 

- Following are the most common configuration an administrator should take to secure SSH 

**Configure Idle Timeout Interval SSH** 

Avoid having an unattended SSH session, you can set an Idle timeout interval 

1. Become root 

2. Edit your /etc/ssh/sshd_config file and add the following line: 

3. ClientAliveInterval 600 

4. ClientAliveCountMax 0 

5. `systemctl restart sshd` 

- The idle timeout interval you are setting is in seconds (600 secs = 10 minutes). Once the interval has passed, the idle user will be automatically logged out 

**Disable root login** 

- Disabling root login should be one of the measures you should take when setting up the system for the first time. It disable any user to login to the system with root account 

1. Become root 

2. Edit your /etc/ssh/sshd_config file and replace PermitRootLogin yes to no 

3. PermitRootLogin no 

4. `systemctl restart sshd` 

**Disable Empty Passwords** 

- You need to prevent remote logins from accounts with empty passwords for added security. 

1. Become root 

2. Edit your /etc/ssh/sshd_config file and remove # from the following line 

3. PermitEmptyPasswords no 

4. systemctl restart sshd 

**Limit Users’ SSH Access** 

- To provide another layer of security, you should limit your SSH logins to only certain users who need remote access 

1. Become root 

2. Edit your /etc/ssh/sshd_config file and add 

3. AllowUsers user1 user2 

4. systemctl restart sshd 

**Use a different port** 

- By default SSH port runs on 22. Most hackers looking for any open SSH servers will look for port 22 and changing can make the system much more secure 

1. Become root 

2. Edit your /etc/ssh/sshd_config file and remove # from the following line and change the port number 

3. Port 22 

4. systemctl restart sshd 

### SSH-Keys - Access Remote Server without Password

Access Remote Server without Password (SSH-Keys) 

- Two reasons to access a remote machine 

- Repetitive logins means login once and have access anytime 

- Automation through scripts 

2. Keys are generated at user level     

- wahab 

- root

![[Pasted image 20250124170304.png]]

Practical Work: 

1. Open your two devices terminal 
    
2. Make sure you are root on both terminals 
    
3. Firstly ifconfig to check the IP and port then ifconfig enp0s3 and verify the IP 
    
4. On client side run command `ssh-keygen` and hit enter and follow the prompt
    
5. Set phrase or not upto you and continue 
    
6. `ssh-copy-id root@198.168.56.101` 
    
7. Enter password 
    
8. Now go on server and check if key is there `cd /root/.ssh/` 

9. check and confirm if the key is there `cat authorized_keys`
    
10. Now go on client side and `ssh root@192.168.56.101`
    
11. You are logged in remotely

> [!NOTE]
> dont forget to give "PermitRootLogin yes" by editing the /etc/ssh/sshd_config


### Cockpit

**Cockpit** is a web-based graphical interface for managing servers, designed to make Linux administration easier and more accessible. It provides a user-friendly, browser-based interface for performing various system administration tasks

Cockpit is a server administration tool sponsored by Red Hat, focused on providing a modern-looking and user-friendly interface to manage and administer servers 

- Cockpit is the easy-to-use, integrated, glance-able, and open web-based interface for your servers 

- The application is available in most of the Linux distributions such as, CentOS, Redhat, 

**Centos9** 

- It is installed in Centos9 by default  

- It can monitor system resources, add or remove accounts, monitor system usage, shut down the system and perform quite a few other tasks all through a very accessible web connection 

**Install, Configure and Manage Cockpit:** 

-  Check for network connectivity 
    
    ping www.google.com 
    

- Install cockpit package as root 
    
    yum/dnf install cockpit –y (For RH or CentOS) 
    
    apt-get install cockpit (For Ubuntu) 
    

- Start and enable the service 
    
    systemctl start cockpit 
    
- Check the status of the service 
    
    systemctl status cockpit 
    
- Access the web-interface 
		https://10.0.2.15:9090
		Enter Username and Password

> [!NOTE]
> root wont login, "/etc/pam.d/cockpit" configuration are causing root login to be denied, check "/etc/cockpit/disallowed-users" , root is there, we need to remove root from there by editing 'vim /etc/cockpit/disallowed-users" to login through cockpit

![[Pasted image 20250127121507.png]]

### Introduction to Firewall

**What is Firewall** 
-  A wall that prevents the spread of fire 
- When data moves in and out of a server its packet information is tested against the firewall rules to see if it should be allowed or not 

- In simple words, a firewall is like a watchman, a bouncer, or a shield that has a set of rules given and based on that rule they decide who can enter and leave 
    
There are 2 type of firewalls in IT 
    
1. **Software** = Runs on operating system 
    
2. **Hardware** = A dedicated appliance with firewall software

![[Pasted image 20250127120950.png]]


**FIREWALL (iptables – tables, chains and targets)**
- There are 2 tools to manage firewall in most of the Linux distributions 

1. iptables = For older Linux versions but still widely used 
2. firewalld = For newer versions like 7 and up 
    
- You can run one or the other 
    
**iptables**
- Before working with iptables make sure firewalld is not running and disable
- systemctl stop firewalld = To stop the service 
- systemctl disable firewalld = To prevent from starting at boot time 
- systemctl mask firewalld = To prevent it from running by other programs


Now check if you have iptables-services package installed 
    
    • rpm –qa | grep iptables-services 
    • yum install iptables-services - If not installed then


Start the service 
    
    • systemctl start iptables 
    
    • systemctl enable iptables


To check the iptables rules    
```
iptables –L
```
    
- To flush iptables 
```
iptables –F
```


The function of iptables tool is packet filtering. 

The packet filtering mechanism is organized into three different kinds of structures: tables, chains and targets 

1. **tables** = table is something that allows you to process packets in specific ways. There are 4 different types of tables, filter, mangle, nat and raw 

2. **chains** = The chains are attached to tables, These chains allow you to inspect traffic at various points. There are 3 main chains used in iptables 
	
	**INPUT** = incoming traffic 
	
	**FORWARD** = going to a router, from one device to another 
	
	**OUTPUT** = outgoing traffic 
	
	chains allow you to filter traffic by adding rules to them 


**Rule** = if traffic is coming from 192.168.1.35 then go to defined target 


3. **targets** = target decides the fate of a packet, such as allowing or rejecting it. There are 3 different type of targets 

	**ACCEPT** = connection accepted 
	
	**REJECT** = Send reject response 
	
	**DROP** = drop connection without sending any response


![[Pasted image 20250127122109.png]]


Drop all traffic coming from a specific IP (192.168.0.25) 
	`iptables –A INPUT –s 192.168.0.25 –j DROP` 

Drop all traffic coming from a range of IPs (192.168.0.0) 
	`iptables –A INPUT –s 192.168.0.0/24 –j DROP` 
    
List all rules in a table by line numbers    
	`iptables –L --line-numbers `
    
Delete a specific rule by line number 
	`iptables –D INPUT 1` 
    
To flush the entire chain 
    `iptables –F `
    
To block a specific protocol with rejection (e.g. ICMP) 
    `iptables -A INPUT -p icmp -j REJECT `
    
To block a specific protocol without rejection (e.g. ICMP) 
    `iptables -A INPUT -p icmp -j DROP `
    
To block a specific port # (e.g. http port 80) 
    `iptables -A INPUT -p tcp --dport 80 -j DROP`


==The iptables read the rules in sequence== 
- If you have a **DROP** rule before an **ACCEPT** rule for the same type of traffic, the **DROP** rule will take precedence, and the traffic will be dropped before it even reaches the **ACCEPT** rule.

Drop before Accept
```
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

Accept before Drop
```
sudo iptables -I INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
```



**LINUX FIREWALL (iptables)** 
**Practical:** 

- Block connection to a network interface 
    
     `iptables -A INPUT -i enps03 -s 192.168.0.25 -j DROP` 
    
- Drop all traffic going to www.facebook.com 

To Find IP of facebook
```
host -t a www.facebook.com = find IP address
```

Drop all traffice going to facebook IP
```
iptables –A OUTPUT –d facebook-IP –j DROP
```    
 
    
- Block all outgoing traffic to a network range 
    
    `iptables –A OUTPUT –d 31.13.71.0/24 –j DROP` 
    
- Block all incoming traffic except SSH 
    
    `iptables -A INPUT -p tcp --dport 22 -j ACCEPT` 
    
    `iptables -P INPUT DROP` 
    
- After making all the changes, save the iptables. Again make sure firewalld is not running 
    
     iptables-save = The file is save in /etc/sysconfig/iptables 
    
- iptables saved file can also be restored 
    
     iptables-restore /LOCATION/FILENAME 
    
- By default everything is logged in 
    
    /var/log/messages 


**Firewalld**

Firewalld works the same way as iptables but of course it has it own commands 
    `firewall-cmd` 
    
It has a few pre-defined service rules that are very easy to turn on and off 
- Services such as: NFS, NTP, HTTPD etc. 
    

Firewalld also has the following: 
**Table** 
**Chains** 
**Rules** 
**Targets** 

Firewall (firewalld) 

- You can run one or the other 
    
     iptables or firewalld 
    
- Make sure iptables is stopped, disabled and mask 
    
    `systemctl stop iptables` 
    
    `systemctl disable iptables` 
    
    `systemctl mask iptables` 
    
- Now check if filewalld package is installed 
    
    `rpm –qa | grep firewalld` 
    
- Start firewalld 
    
    `systemctl start/enable firewalld` 
    
- Check the rule of firewalld 
    
    `firewall-cmd --list-all` 
    
- Get the listing of all services firewalld is aware of: 
    
    `firewall-cmd --get-services` 
    
- To make firewalld re-read the configuration added 
    
    `firewall-cmd –reload` 
    

**Firewall (firewalld)**
**Practical:**

- The firewalld has multiple zone, to get a list of all zones 
    
    `firewall-cmd --get-zones` 
    
- To get a list of active zones 
    
    `firewall-cmd --get-active-zones` 
    
- To get firewall rules for public zone 
    
    `firewall-cmd --zone=public --list-all` 
    
    OR 
    
    `firewall-cmd --list-all` 
    
- All services are pre-defined by firewalld. What if you want to add a 3rd party service 
    
    /usr/lib/firewalld/services/allservices.xml 
    
    Simply cp any .xml file and change the service and port number


![[Pasted image 20250127124627.png]]


- To add a service (http) 
    
    `firewall-cmd --add-service=http` 
    
- To remove a service 
    
    `firewall-cmd --remove-service=http` 
    
- To reload the firewalld configuration 
    
    `firewall-cmd --reload` 
    
- To add or remove a service permanently 
    
    `firewall-cmd --add-service=http --permanent` 
    
    `firewall-cmd --remove-service=http --permanent` 
    
- To add a service that is not pre-defined by firewalld 
    
    /usr/lib/firewalld/services/allservices.xml 
    
    Simply cp any .xml file sap.xml and change the service and port number (32) 
    
    `systemctl restart firewalld` 
    
    `firewall-cmd --get-services` (to verify new service) 
    
    `Firewall-cmd --add-service=sap` 
    
- To add a port 
    
    `firewall-cmd --add-port=1110/tcp` 
    
- To remove a port 
    
    `firewall-cmd --remove-port=1110/tcp` 
    
- To reject incoming traffic from an IP address 
    
    `firewall-cmd --add-rich-rule='rule family="ipv4" source address=“192.168.0.25" reject’` 
    
- To block and unblock ICMP incoming traffic 
    
    `firewall-cmd --add-icmp-block-inversion` 
    
    `firewall-cmd --remove-icmp-block-inversion` 
    
- To block outgoing traffic to a specific website/IP address 
```
host -t a www.facebook.com = find IP address 
```

```
firewall-cmd --direct --add-rule ipv4 filter OUTPUT 0 -d 31.13.71.36 -j DROP
```
    


### Tune System Performance

Linux system comes fined tunned by default when you install, however there are a few tweaks that can be done based on system performance and application requirements 

In this lesson we will learn… 

- Optimize system performance by selecting a tuning profile managed by the tuned daemon 
    
- Prioritize or de-prioritize specific processes with the nice and renice commands 
    

What is tuned? 

-  Tuned pronounced as tune-d 
    
-  Tune is for system tuning and d is for daemon 
    
-  It is systemd service that is used to tune Linux system performance 
    
-  It is installed in CentOS/Redhat version 7 and 8 by default 
    
-  tuned package name is tuned 
    
-  The tuned service comes with pre-defined profiles and settings (List of profile will be discussed in the next page) 
    
-  Based on selected profile the tuned service automatically adjust system to get the best performance. E.g. tuned will adjust networking if you are downloading a large file or it will adjust IO settings if it detects high storage read/write 

-  The tuned daemon applies system settings when the service starts or upon selection of a new tuning profile.


![[Pasted image 20250127155530.png]]


- Check if tuned package has been installed 
    `rpm –qa | grep tuned` 
    
- Install tuned package if NOT installed already 
    `yum install tuned` 
    
-  Check tuned service status 
    `systemctl status|enable|start tuned` 
    `systemctl enable tuned` (To enable at boot time) 
    
-  Command to change setting for tuned daemon 
    `tuned-adm` 
    
-  To check which profile is active 
    `tuned-adm active` 
    
-  To list available profiles 
    `tuned-adm list` 
    
- To change to desired profile 
    `tuned-adm profile profile-name`  e.g. `tuned-adm profile balanced`
    
-  Check for tuned recommendation 
    `tuned-adm recommend` 
    
-  Turn off tuned setting daemon 
    `tuned-adm off` 
    
-  Change profile through web console 
    
    Login to https://10.0.2.15:9090 
    
    Overview → Configuration -> Performance profile -> select profile

![[Pasted image 20250127160518.png]]

-  Another way of keeping your system fine-tuned is by prioritizing processes through nice and renice command 

-  If a server has 1 CPU then it can execute 1 computation/process at a time as they come in (first come first served) while other processes must wait 

-  With nice and renice commands we can make the system to give preference to certain processes than others 

-  This priority can be set at 40 different levels 
    
-  The nice level values range from -20 (highest priority) to 19 (lowest priority) and by default, processes inherit their nice level from their parent, which is usually 0.


![[Pasted image 20250127161629.png]]


Nice value is a user-space and priority PR is the process's actual priority that use by Linux kernel. In Linux system priorities are 0 to 139 in which 0 to 99 for real time and 100 to 139 for users 

-  Process priority can be viewed through ps command as well with the right options 
    
    `ps axo pid,comm,nice,cls --sort=-nice` 
    
-  To set the process priority 
    
    `nice –n # process-name` 
    
    e.g. `nice –n -15 top` 
    
-  To change the process priority 
    
    `renice –n # process-name` 
    
    e.g. `renice –n 12 PID`


### Run Containers

What is a Container? 

- A **container** in Linux is a lightweight, standalone, and executable package that includes everything needed to run a piece of software: code, runtime, system tools, libraries, and settings. Containers provide an efficient way to develop, ship, and run applications by abstracting the application from the underlying host system, ensuring it runs consistently regardless of the environment.

> [!NOTE]
> Container technology is mostly used by developers or programmers who write codes to build applications, As a system Administrator Your Job Is to install, configure and manage them.

![[Pasted image 20250128092837.png]]


**Docker**: 

• Docker is the software used to create and manage containers

• Just like any other package, docker can be installed on your Linux system and its service or daemon can be controlled through native Linux service management tool


**Podman**: 

• Podman is an alternative to docker 

• Docker is not supported in RHEL 8 

• It is daemon less, open source, Linux-native tool designed to develop, manage, and run containers. 


###### Getting Familiar with Redhat Container Technology 

Red Hat provides a set of command-line tools that can operate without a container engine, these include: 

- podman - for directly managing pods and container images (run, stop, start, ps, attach, etc.) 
    
- buildah - for building, pushing, and signing container images 
    
- skopeo - for copying, inspecting, deleting, and signing images 
    
- runc - for providing container run and build features to podman and buildah 
    
- crun - an optional runtime that can be configured and gives greater flexibility, control, and security for rootless containers. 

###### Getting Familiar with Podman Container Technology 

When you hear about containers then you should know the following terms as well 

- images – containers can be created through images and containers can be converted to images 
    
- pods – Group of containers deployed together on the host. In the podman logo there are 3 seals grouped together as a pod. 

###### Building, Running and Managing Containers 

- To install podman 

For Podman
```
yum/dnf install podman –y 
```

For Docker
```
yum install docker –y
```
    
    
- Creating alias to docker 
```
alias docker=podman 
```
    
- Check podman version 
```
podman –v 
```
    
- Getting help 
```
podman -–help or man podman 
```

    
- Check podman environment and registry/repository information podman info (If you are trying to load a container image, then it will look at the local machine and then go through each registry by the order listed) 

- To search a specific image in repository. 
```
podman search httpd 
```

- To list any previously downloaded podman images 
```
podman images 
```

    
- To download available images 
```
podman pull docker.io/library/httpd 
```

Check downloaded image status
```
podman images 
```
    

    
- To list podman running containers 
```
podman ps 
```

    
- To run a downloaded httpd containers 
```
podman run -dt -p 8080:80/tcp docker.io/library/httpd
```
 
    
(d=detach, t=get the tty shell, p=port) 
    
podman ps or Check httpd through web browser 
    
- To view podman logs. 
```
podman logs –l
```
 

- To stop a running container
```
podman stop con-name
```
con-name from podman ps command

```
podman ps
```
To list running containers 
    
- To run a multiple containers of httpd by changing the port # 
```
podman run -dt -p 8081:80/tcp docker.io/library/httpd
```
```
podman run -dt -p 8082:80/tcp docker.io/library/httpd
```

```
podman ps 
```
to check the current podman processes

    
- To stop and start a previously running container 
```
podman stop|start con-name 
```

    
- To create a new container by name sweetLeslie from the downloaded image 
```
podman create –-name sweetLeslie docker.io/library/httpd 
```

==sweetLeslie is the name of container i created==

- To start the newly created container 
```
podman start sweetLeslie 
```

```
podman ps
```
to check if the container sweetLeslie is running

- go to this directory /etc/systemd/system

###### Manage containers through systemd 

- First you have to generate a unit file 
```
podman generate systemd –-new –-files –-name sweetLeslie 
```

> [!NOTE]
> `podman generate systemd`**:** This command was used to generate systemd service unit files to manage Podman containers. However, it has been deprecated in favor of Quadlets.
Read about quadlets

- ls -ltr to check, the container would be there by name container-sweetLeslie.service

- Copy it systemd directory 
```
cp /root/container-sweetLeslie.service /etc/systemd/system
```    
 
    
- Enable the service 
```
systemctl enable container-sweetLeslie.service
```
 
    
- Start the service. 
```
systemctl start container-sweetLeslie.service
```

![[Pasted image 20250128102701.png]]


### KickStart (Automate Linux Installation)

Kickstart is a method to automate the Linux installation without the need for any intervention from the user 

With the help of kickstart you can automate questions that are asked during the installation. e.g. 

- Language and time zone 

- How the drives should be partitioned 

- Which packages should be installed etc.


Purpose?
- Helpful when it comes to installation on multiple systems

![[Pasted image 20250128124829.png]]

###### To use Kickstart, you must: 
1. Choose a Kickstart server and create/edit a Kickstart file 

2. Make the Kickstart file available on a network location 

3. Make the installation source available 

4. Make boot media available for client which will be used to begin the installation 

5. Start the Kickstart installation


![[Pasted image 20250128125032.png]]

###### Centos9 
- the kickstart gui is not available on centos9 and cannot be installed
- instead the /root anaconda-ks.cfg file can be used for automation
- make sure to configure the anaconda-ks.cfg file for users and hostname


###### Procedure
1. Identify the server 
    
2. Take a snapshot of the server

3. Make sure httpd package is installed, if not then install the package and start the httpd service 

```
rpm –qa | grep http 
```

```
yum/dnf install httpd 
```

```
systemctl start httpd 
```

```
systemctl enable httpd 
```



1. Copy kickstart file to httpd directory and change the permissions 

```
cp /root/anaconda-ks.cfg /var/www/html
```
 
```
chmod a+r /var/www/html/anaconda-ks.cfg 
```

```
systemctl stop|disable firewalld
```
 

Check file through browser on another PC http://192.168.56.101/anaconda-ks.cfg 

5. Create a new VM and attach the CentOS iso image 
    
6. Change the network adapter to Bridged adapter 
    
7. Hit Esc 
    
8. Type: ==boot: linux ks=http://192.168.56.101/anaconda-ks.cfg== 
    
    For NFS → ==boot: linux inst.ks=nfs:192.168.56.101:/rhel8== 
    
9. Enter then Wait and enjoy the automated installation 
    

Kickstart for clients with static IP 

==boot: linux ks=http://server.example.com/ks.cfg ksdevice=eth0 IP:192.168.1.50 netmask=255.255.255.0 gateway=192.168.1.1== 

Where: 

ksdevice = is the network adapter of the client 

IP = IP you are assigning to the client 

Netmask = Subnet mask for the client 

Gateway = Gateway IP address for the client


### DHCP

> [!NOTE]
> This lecture show how to setup DHCP server conceptually because if you want to setup DHCP server on your Linux machine then you will have to re-configure your router/modem in your home which can route DHCP traffic to your new DHCP server. 
> Reconfiguring router/modem will make all your devices at home lose the network connectivity
> 

- DHCP stands for Dynamic Host Configuration Protocol 
    
- In order to communicate over the network, a computer needs to have an IP address 
    
- DHCP server is responsible to automatically assign IP addresses to servers, laptops, desktops, and other devices on the network 

- Right now in our home how IPs are assigned to our devices? 
     Answer → The router or gateway given to you by your ISP provider 
    
- How IPs are assigned in corporate world? 
    Answer → Dedicated routers run DHCP service to assign IPs on the network 
    
###### Step by steps instructions 

- Pick a server to be your DHCP and take a snapshot 
    
- Assign a static IP to the DHCP server 
    
    vi /etc/sysconfig/network/enp0s3 
    
    Or simply run nmtui command to use GUI based network tool


![[Pasted image 20250128142715.png]]

###### Install dhcp server package 
for centos version 7
```
 yum install dhcp 
```

version 8
```
dnf install dhcp-server 
```


    
###### Edit the configuration file with desired parameters 

```
vi /etc/dhcp/dhcp.conf
```    
 
```
cp /usr/share/doc/dhcp-x.x.x/dhcpd.conf.example /etc/dhcp/dhcpd.conf
```

![[Pasted image 20250128143000.png]]


###### Start dhcpd service 

```
systemctl start dhcpd
```
 
```
systemctl enable dhcp
```
 
###### Disable firewalld or allow dhcp port over firewall 

```
systemctl stop firewalld 
```

OR 
```
firewall-cmd --add-service=dhcp –permanent 

firewall-cmd –reload
```
 
###### Switch DHCP service from your router/modem to your new DHCP server 

- Login to your ISP provided router 

- Disable dhcp and enable forwarding to the new dhcp server.











