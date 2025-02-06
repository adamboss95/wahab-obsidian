Enable Passwords:

File = /etc/login.def ==more /etc/login.defs== (defs=default)

- PASS_MAX_DAYS 99999
- PASS_MIN_DAYS 0
- PASS_MIN_LEN 5
- PASS_WARN_AGE 7

**The chage(change age) command**

chage [-d lastday] [-m mindays] [-M maxdays] [-W warndays] [-I inactive] [-E expiredate] user

-d =3 . Last password change -m= 4. Minimum -M = 5. Maximum -W = 6. Warn -I = 7. Inactive -E =8. Expire

==grep username /etc/shadow==

```
chage -m 5 -M 90 -W 10 -I 3    (babubutt) user-name
```

# Switch User & Sudo Access

- su - username
- sudo command
- visudo

# File

- /etc/sudoers (to check that user have all permissions that we allowed ) ==cat /etc/sudoers==

# Monitor User :

- who ---> (how many people logged in to the system)
- last (last | more)
- w ----> (same as who , but will little more info like login time etc)
- finger (needs to install that command)
- id ---> (will give you username id )

# Talking to Users:

- users (can check how many users are )
- wall
- write (to communicate with other users )

# Linux Account Authentication:

Difference between - **Active Directory** A directory service developed by Microsoft for Windows environments - **LDAP** : Lightweight Directory Access Protocol - **IDM** Identity & Access Management - **WinBIND** : used in linux to communicate with windows - **OpenLDAP** : open source - Jumpcloud

# System Utility Commands:

- date :will tells you date and time
- uptime
- hostname
- uname : uname -a : lot more details of machine
- which : location of command that you runs
- cal : calender
- bc

# Processes & Jobs:

1. Application
2. script
3. Process
4. Daemon
5. Threads
6. Job

#### Process/Services Commands

- systemctl or service
- ps
- top

# Systemctl Command:

- to check how many service are active

```
systemctl list-units --type=service --all
```

- Start a service

```
sudo systemctl start <servicename>  
```

- Stop a service

```
sudo systemctl stop <servicename>  
```

- Check Status

```
sudo systemctl status <servicename>  
```

- Restart a service

```
sudo systemctl restart <servicename>  
```

- Enable a service to start at boot:

```
sudo systemctl enable <service_name>  
```

- Disable a service to start at boot:

```
sudo systemctl disable <service_name>  
```

#### System Management:

**reboot the system**: 

```
sudo systemctl reboot  
```

**Shutdown the system**:

```
sudo systemctl poweroff

```

**Suspend the system**: 

```
sudo systemctl suspend  
```

# PS Command:

process status will display all process running on linux system
==PID== : process id 
==TTY== : terminal type 
==TIME== : amount of CPU in minute and seconds that the process has been running 
==CMD== : name of command

ps ---> show the process of current shell ps -e ---> show all running processes ps aux ---> shows all running processes in BSD format ps -ef ---> shows all running processes in full format listing(used one) ps -u username ---> shows all running processes in specific user

# top Command:

Continuously updates, showing live CPU and memory usage. Allows you to view and manage active processes. **Process Information :  
- **PID**: Process ID.  
- **USER**: The user who owns the process.  
- **PR**: Process priority.  
- **NI**: Nice value (priority modifier).  
- **VIRT**: Virtual memory used by the process.  
- **RES**: Resident memory (physical memory used).  
- **SHR**: Shared memory used by the process.  
- **S**: The current state of the process (e.g., `S` for sleeping, `R` for running).  
- **%CPU**: CPU usage percentage.  
- **%MEM**: Memory usage percentage.  
- **TIME+**: Total CPU time used by the process.  
- **COMMAND**: The command or program running for the process.

==top -u username== For specific user

==top then press c== will show you absolute path

==top then press k== and select id and enter : will kill running process

==top then press M and P== will sort all Linux running processes

# kill Command:

is used to terminate processes manually

# kill option process-id(PID)

kill -l --->  
kill -1 ---> Restart kill -2 ---> JUST LIKE Ctrl C kill -9 ---> forcefully kill the process kill -15 ---> kill a process gracefully

# crontab Command:

-------> is used to schedule tasks **crontab -e** Edit crontab **crontab -l** LIst the crontab entries **crontab -r** Remove the crontab **crontd** service that manage scheduling

`minute (m), hour (h), day ,month (mon), enter text` ctrl + X

# at Command:

Schedules a one-time task to run at a specific time. Allows specifying a task to run once at a specific date and time in the future. `cntrl +D` ( For get-out of he command)

![[Pasted image 20250114172552(1).png]] for remove atrm #(process id) we have to give process id and will remove only the entry which not displayed yet 
![[Pasted image 20250114172352(2).png]]


# Additional cronjobs

**Crontab:** The configuration file where cron jobs are defined. Each user can have their own crontab file. - Hourly - Daily - Weekly - Monthly

==/etc/cron.hourly== or ==/etc/cron.weekly== so on ==cd cron.monthly/==

> [!NOTE] ls -l cron. *  
> cd cron.daily cd cron.hourly/