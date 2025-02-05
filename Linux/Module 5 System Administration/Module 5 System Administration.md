##### Jan 13, 2025
# SOC Analyst Training
## Linux Training

## Module 5
1. **Linux File Editor**
- Introduction to vi
	- vi common keys for:
		- i = insert
		- Esc = escape out of any mode
		- r = replace
		- d = delete
		- u = undo
		- x = to delete one character
		- :q! - quit without saving
		- :wq! - save and quit or shift zz
2. **Difference between vi and vim Editor**
- `vi` is a basic text editor, while `vim` (Vi IMproved) offers enhanced features like syntax highlighting, multi-level undo, and extensive customization.
3. **sed Command**
- Replace a string in a file with a newstring
	- syntax = `sed 's/keyword/replaceWith/g' filename` = s for substitute, keyword the word that will replace, replaceWith is the word to replace, g for global
	- `sed 's/keyword/replaceWith/g' filename` = doesnt make change to the file
	- `sed -i 's/keyword/replaceWith/g' filename` = i is used to make change in the file
	- `sed 's/keyword//g' filename`
	- `sed -i 's/keyword//g' filename` = replacing with empty
	- `sed '11!s/keyword/replaceWith/' filename` = replace the word except line 11
![[Pasted image 20250114092648.png]]
![[Pasted image 20250114092721.png]]
![[Pasted image 20250114093240.png]]
![[Pasted image 20250114093328.png]]
![[Pasted image 20250114103517.png]]
- Find and delete a line
	- `sed '/keyword/d' filename`
	- ==use -i to make changes in file==
![[Pasted image 20250114093920.png]]
- Remove empty lines
	- `sed '/^$/d' filename`
	- `sed -i '/^$/d' filename`
![[Pasted image 20250114094526.png]]
- Remove the first or n lines in a file
	- `sed '1d' strawhats`
	- `sed '1,2d' strawhats`
![[Pasted image 20250114095730.png]]
- To replace tabs with spaces
	- `sed 's/\t/ /g' filename`
	- `sed -i 's/\t/ /g' filename`
![[Pasted image 20250114100746.png]]
- To replace spaces with tabs
	- `sed 's/ /\t/g' filename`
![[Pasted image 20250114101210.png]]
- Show defined lines from a file
	- `sed -n 3,6p filename` = shows line 3 to 6
	- `sed -n 3p filename` = shows line 3
	- `sed 5,7d filename` = deletes line 5 to 7
	- `sed G filename` = puts an empty line after each line
![[Pasted image 20250114102215.png]]
![[Pasted image 20250114102234.png]]
![[Pasted image 20250114102417.png]]
![[Pasted image 20250114102622.png]]
- Substitute within vi editor
	- go into editor using `vi filename` > ":%s/keyword/replaceWith/" enter

4. **User Account Management**
- Commands
	- useradd
		- `useradd admiral` = needs root access to create user so use `sudo` at the start or change user to root using `su -` or `sudo su` (it doesnt create a directory in home, to create directory in home for user, use `useradd -m username`) 
		- `useradd -g emperor -s /bin/bash -c "sea emperor" -m -d /home/emperorTeach emperorTeach` = create and add the user to the group emperor 
	- ![[Pasted image 20250114111249.png]]
	- groupadd
		- `groupadd groupName` = creates a group account named emperor 
	- userdel
		- `userdel username` = deletes user but doesnt delete directory, to remove user directory also in home use `userdel -r username`
	- ![[Pasted image 20250114111901.png]]
	- groupdel
		- `groupdel groupUsername`
	- usermod
		- `usermod -G groupname username` = adds the user to the group
	- ![[Pasted image 20250114113132.png]]
- Files (created account record is in three different files /etc/passwd , /etc/group , /etc/shadow)

5. **The /etc/login.defs File**
- The chage command - per user
	- chage (-m mindays) (-M maxdays) (-d lastday) (-I inactive) (-E expiredate) (-W warndays) user
- File = /etc/login.defs 
	- `more /etc/login.defs` = shows info on the login.defs file
	- PASS_MAX_DAYS 99999
	- PASS_MIN_DAYS 0
	- PASS_MIN_LEN 5
	- PASS_WARN_AGE 7
- `sudo chage -m 5 -M 90 -W 10 -I 3 username`
![[Pasted image 20250114141642.png]]

6. **Switch Users and sudo Access**
- commands
	- su - username = swtich to a username
	- sudo = to get super user access
	- visudo = used to safely edit the `/etc/sudoers` file. The `/etc/sudoers` file determines which users and groups have sudo privileges, allowing them to execute commands with superuser (root) privileges. (ctrl+x to exit the visudo editor)
	- `usermod -aG sudo username` = adds the username to the group sudo, the -aG means to add the username to the group without removing it from other groups

7. **Monitor Users**
- `who` = used to display information about the users currently logged into the system.
![[Pasted image 20250114152715.png]]
- `last` = displays all the details of all users logged in since day 1
	- `last | awk '{print $1}'` = to display the first column of last command
	- `last | awk '{print $1}' | sort | uniq` = show uniq first column of last command
- w = provides more detailed information about the users logged into the system, including what each user is currently doing.
![[Pasted image 20250114154051.png]]
- `finger` = display detailed information about system users
![[Pasted image 20250114154602.png]]
- `id username` = shows the id information of the username

8. **Talking to Users**
- `users` = shows the current logged in users
- wall = used to broadcast a message to all users (ctrl+d to exit the wall editor)
- `write username` = write message to a specific username

9. **Linux Account Authentication**
- Types of accounts
	- Local accounts
	- Domain/Directory accounts

10. **Difference between Active Directory, LDAP, IDM, WinBIND, OpenLDAP etc.**
- Active Directory = Microsoft
- IDM = An Identity Manager is a tool or system used for identity and access management (IAM)
- WinBIND = used in Linux to communicate with Windows (Samba)
- OpenLDAP (open source)
- IBM Directory Server
- JumpCloud
- LDAP = Lightweight Directory Access Protocol

11. **System Utility Commands**
- `date`
- `uptime`
- `hostname` = shows hostname
- `uname` = shows the system name
- `which command` = shows the location of command
- `cal` = shows calendar
- bc = binary calculator

12. **Processes and Jobs and Scheduling**
- Processes and Jobs
	- Application = Service
	- Script = script/commands e.g. adduser, whoami etc
	- Process = process runs as soon as an application is being run
	- Daemon = daemon keeps running in the background until it is interrupted
	- Threads = often referred as lightweight processes because it can run in parallel, allowing for more efficient use of resources and better performance in multi-core systems.
	- Job = created by schedular to run application and services 
- Process/Services Commands
	- systemctl or service
	- ps
	- top
	- kill
	- crontab
	- at

13. **systemctl command**
- systemctl command
	- systemctl start | stop | status servicename.service (firewalld)
		- ![[Pasted image 20250115095942.png]]
		- ![[Pasted image 20250115100028.png]]
		- ![[Pasted image 20250115100132.png]]
	- `systemctl enable servicename.service` , `systemctl disable servicename.service`
		- ![[Pasted image 20250115100044.png]]
		- ![[Pasted image 20250115100106.png]]
	- systemctl restart | reload servicename.service
	- systemctl list-units --all
		- ![[Pasted image 20250115095712.png]]
		- ![[Pasted image 20250115101111.png]]
- To add a service under systemctl management:
	- Create a unit file in /etc/systemd/system/servicename.service
- To control system with systemctl
	- systemctl poweroff = poweroff entire system
	- systemctl halt = halt entire system
	- systemctl reboot = reboot entire system

14. **ps command**
- ps = process status, displays all currently running processes in the linux system
	- ![[Pasted image 20250115102415.png]]
	- ![[Pasted image 20250115102010.png]]
- ps -e = show all running processes
- ps aux = shows all running process in BSD (berkley system description) format
- ps -ef = shows all running processes in full format listing (most commonly used)
	- ![[Pasted image 20250115102352.png]]
- ps -u username = show all processes by username
	- ![[Pasted image 20250115102550.png]]

15. **top**
- top = shows the Linux processes and it provides a real-time view of the running system
	- ![[Pasted image 20250115103657.png]]
- top -u username = shows task/processes by user owned
	- ![[Pasted image 20250115103808.png]]
- top then press c = shows commands absolute path
	- ![[Pasted image 20250115103938.png]]
- top then press k = kill a process by PID (process ID) within top session
- top then M and P = to sort all linux running process by memory usage
- ==top command refreshes information every 3 second==

16. **kill Command**
- kill = used to terminate processes manually
- kill (option) (PID) = option (signal name or signal numer/ID)
- kill -l = get a list of all signal names or signal number
- kill PID = kill a process with default signal
- kill -1 (PID) = Restart process
- kill -2 = Interrupt from the keyboard just like Ctrl C
- kill -9 (PID) = forcefully kill the process
- kill -15 = kill a process gracefully
- killall = kill all processes
- pkill = kill by process name

17. **crontab command**
- crontab = used to schedule task
- crontab -e = edit the crontab
- crontab -l = list the crontab entries
- crontab -r = remove the crontab
- crond = crontab daemon/service that manages scheduling
- systemctl status crond = manage the crond service
- Crontab Fields
	- **Minute**: The minute of the hour (0-59).
	- **Hour**: The hour of the day (0-23).   
	- **Day of the Month**: The day of the month (1-31).
	- **Month**: The month of the year (1-12).   
	- **Day of the Week**: The day of the week (0-7) where both 0 and 7 represent Sunday.
	- **Command**: The command or script to be executed.
- crontab -e
	- min hour day month week echo "hello this is my first crontab entry" > filename (* in the code means every day or every week where it is used)
	- ![[Pasted image 20250115113039.png]]
- crontab -r = deletes the crontab entry in the same directory
- crontab -l = shows content of crontab in the same directory

18. **at command**
- at = like crontab allows you to schedule jobs but only once
- when command is run, it enters interactive mode and you can get out by pressing Ctrl D
- syntax `at HH:MM PM` = schedule a job
	- ![[Pasted image 20250115115105.png]]
- atq = list the at entries
	- ![[Pasted image 20250115115205.png]]
- atrm # = remove at entry
	- ![[Pasted image 20250115115209.png]]
- atd = at daemon/service that manages sheduling
- systemctl status atd = to manage the atd service
- `at 2:45AM 10162025` = schedule a job to run on Oct16, 2025
- `at 4 PM + 4 days` = schedule a job at 4pm four days from now
- `at now + 5 hours` = schedule a job five hours from now
- `at 8:00 AM Sun` = Schedule a job to 8am on coming Sunday
- at 10:00 AM next month = schedule a job to 10am next month

19. **Additional Cron Jobs**
- By default 4 different types of cronjobs
	- hourly
	- daily
	- weekly
	- monthly
- all the above crons are steup in
	- /etc/cron.... (directory)
- Timing for each are set in
	- /etc/anacrontab -- except hourly
- For hourly
	- /etc/cron.d/0hourly
- ls -l /etc/ | grep cron
	- `cron.d` =This directory contains individual cron job files. Each file in this directory can specify its own scheduling, similar to how entries are made in the main crontab file.
	- cron.hourly = Scripts in this directory are executed once per hour. It's useful for tasks that need frequent updates or checks.
	- cron.monthly = Scripts placed here are executed once a month, typically at the start of the month. It's good for monthly maintenance tasks or reports.
	- crontab = This refers to the crontab file or the command used to edit the crontab file. The crontab file contains the schedule and commands for individual users.
	- cron.weekly = Scripts in this directory are executed once a week, usually on Sundays. It's useful for weekly maintenance tasks.

20. **Process Management**
- Background = ctrl-z, jobs and bg
- Foreground = fg
- Run process even after exit = nohup process & OR = nohup process > /dev/null 2>&1 &
	- ![[Pasted image 20250115150253.png]]
	- ![[Pasted image 20250115150354.png]]
- Kill a process by name = pkill
- Process priority = nice (e.g. nice -n 5 process)
	- The nice scale goes from -20 to 19. The lower the number more priority that task gets
- Process monitoring = top
- List process = ps
	- `ps -ef | grep sleep` = to search sleep process

21. **System Monitoring**
- `top` = command is a powerful utility in Linux used to display real-time information about the system’s processes, resource usage, and overall performance. It provides a dynamic, interactive view of what's happening on the system.
- `df` = displays disk space usage information
	- `df -h` = display disk space usage in a human-readable format.
	- `du` (disk usage)= estimate the space used by files and directories.
		- `du -h` = more human readable format
- dmesg = examine and control the kernel ring buffer. It displays messages from the kernel, which can be helpful for diagnosing and troubleshooting system and hardware issues
	- sudo dmesg -H = more human readable format
- `iostat` = command in Linux is used to monitor system input/output device loading by observing the time the devices are active relative to their average transfer rates. It can provide useful information about disk I/O, CPU utilization, and network interface statistics
	- i`ostat -1` = refreshes the iostat every 1 second
- `netstat` = provides information about network connections, routing tables, interface statistics, masquerade connections, and multicast memberships. It is used for troubleshooting network issues and monitoring network activity
	- `netstat -rmv` = display the kernel IP routing table with numerical addresses and no DNS lookup
		- `r`: Displays the kernel routing table.
		- `-n`: Shows addresses and port numbers in numerical form (without DNS resolution).
		- `-v`: Provides verbose output, giving additional details if available.
		- ![[Pasted image 20250115154102.png]]
- free = system's memory usage, including total, used, free, shared, buffer/cache, and available memory information
	- ![[Pasted image 20250115154914.png]]
- cat /proc/cpuinfo = shows cpu information
- cat /proc/meminfo = shows memory information

22. **System Log Monitoring**
- /var/log = all logs generated are in log directory
	- boot = system boot information are in boot
	- chronyd = NTP = Chrony is an implementation of the Network Time Protocol (NTP) designed to keep the system clock in sync with remote NTP servers. It is particularly useful on systems that are not always connected to the network or have variable latency, such as laptops or virtual machines
	- cron = logs
	- maillog = logs
	- secure = logs related to logged in users
		- `sudo less /var/log/auth.log` instead of secure
		- `tail -f secure` or `tail -f auth.log`= displays the last log related to users logged in
			- ![[Pasted image 20250115163603.png]]
	- messages = logs
		- `cat syslog`
		- `sudo tail -f /var/log/syslog`
		- ![[Pasted image 20250115163934.png]]
	- httpsd = apache application log

23. **System Maintenance Commands**
- shutdown = shutdown in a safe way. It also allows to schedule a shutdown or reboot after a specified time.
	- shutdown (options) (time (message)
		- Options:
			- `-h`: Halts the system.
			- `-r`: Reboots the system.
			- `-c`: Cancels a scheduled shutdown.
	- `sudo shutdown -h now` = shutdown system immediately
	- `sudo shutdown -r +5` = reboot the system in 5 minutes
- init 0-6 = change the runlevel of the system. It directly interacts with the `init` process, which is the parent of all processes
	- **Runlevels**:
		- `0`: Halt the system.
		- `1`: Single-user mode.
		- `3`: Multi-user mode without GUI.
		- `5`: Multi-user mode with GUI.
		- `6`: Reboot the system.
	- sudo init 6 = reboots the system
- reboot = restart the system
	- `shutdown -r now` is alternate command to reboot
- halt = stops all processes and halts the system. It’s equivalent to running `shutdown -h now`

24.  **Changing System Hostname**
- `hostnamectl - set-hostname newhostname` OR `vi /etc/hostname` (change hostname in the editor)
- path /etc/hostname

25. **Finding System Information**
- `cat /etc/os-release` = displays OS information
- `uname -a` = displays information about OS
- `dmidecode` = shows SMBIOS (System Management BIOS) data, including hardware details such as the system manufacturer, BIOS version, serial numbers, and more.

26. **System Architecture**
- Differences between a 32-bit and 64-bit CPU
	- 32-bit CPUs: Suitable for basic computing tasks and older systems with limited RAM. use the x86 architecture
	- 64-bit CPUs: Better for modern computing needs, supporting more RAM, improved performance, and enhanced security features. use the x86-64 (or AMD64) architecture
- `arch` = shows if cpu is 32bit or 64bit 

27. **Terminal Control Keys**
- Key combinations
	- ctrl+u = erase everything typed on the command line
	- ctrl+c = stop/kill a command
	- ctrl+z = suspend a command
	- ctrl+d = exit from an interactive program (signals end of data)

28. **Terminal Commands**
- clear = clears screen
- exit = exit out of shell, terminal or a user session
- script = stores terminal activities in a log file that can be named by a user, when a name is not provided by a user, the default file name, typescript is used

29. ==Recover Root Password==
- Restart computer
- Edit grub
	- press e instead of enter to edit when selecting the OS
	- then search for ro
	- remove ro and type there `rw init=/sysroot/bin/sh` > ctrl+x > it will start the computer in single mode user
	- then type `chroot /sysroot` press enter and then type `passwd root` to change root password, enter then type `touch /.autorelabel` to update selinux information, then type `exit` to exit out of sysroot > then type `reboot` to reboot the system
- Change password
- Reboot

30. **SOS Report**
- What is SOS Report?
	- Collect and package diagnostic and support data
- Package name
	- sos-version
- Command
	- sosreport

31. Environment Variables
- What are environment variables?
	- a dynamic-named value that can affect the way running processes will behave on a computer. They are part of the environment in which a process runs
- To view all environment variables
	- printenv OR env
- To view ONE environment variable
	- echo $SHELL
- To set the environment variables
	- export TEST=1
	- echo $TEST
- ![[Pasted image 20250116112130.png]]
- To set environment variable permanently
	- vi .bashrc
	- TEST='123'
	- export TEST
- To set global environment variable permanently
	- vi /etc/profile or /etc/bashrc
	- Test='123'
	- export TEST

32. Special Permissions
- All permissions on a file or directory are referred as bits
	- -rwx rwx rwx
		- 1st three are for Users, 2nd three for Groups and 3rd for Others
- There are 3 additional permissions in Linux
	- setuid: bit tells Linux to run a program with the effective user id of the owner instead of the executor: (e.g. passwd command) -> /etc/shadow
	- setgid: bit tells linux to run a program with the effective group id of the onwer instead of the executor: (e.g. locate of wall command)
		- note: this bit is present for only files which have executable permissions
	- sticky bit: a bit set on files/directories that allows only the owner or root to delete those files
- ![[Pasted image 20250116114341.png]]
- To assign special permissions at the user level
	- `chmod u+s xyz.sh`
- To assign special permissions at the group level
	- `chmod g+s xyz.sh`
- To remove special permissions at the user or group level
	- `chmod u-s xyz.sh`
	- `chmod g-s xyz.sh`
- To find all executables in Linux with setuid and setgid permissions
	- find / -perm /6000 -type f
- Stick bit
	- It is assigned to the last bit of permissions
- ==These bits work on c programming executables not on bash shell scripts==
- ![[Pasted image 20250116121216.png]]

- Lab Exercise:
	- Become root and create a directory allinone in / = mkdir /allinone
	- Assign all rwx permissions to that directory = chmod 777 /allinone
	- Become abdulwahab and create directory inside of /allinone = mkdir dir1
	- Give all rwx permissions to that directory = chmod 777 dir1
	- Create 3 files in that directory = touch a b c
	- Open another terminal and login as another user
	- Go to /allinone directory and delete dir1 directory = rm -rf dir1
		- you will see the directory is deleted
	- Now become root again and assign sticky bit permission to /allinone = chmod +t /allinone
	- Become abdulwahab and create directory again inside of /allinone = mkdir dir1
	- Give all rwx permissions to that directory = chmod 777 dir1
	- Create 3 files in that directory = touch a b c
	- Open another terminal and login as another user
	- Go to /allinone directory and delete dir1 directory = rm -rf dir1
		- this time it wont delete because of the sticky that we assigned to /allinone