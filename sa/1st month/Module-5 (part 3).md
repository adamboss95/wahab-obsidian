# Process management:

Background = ctrl+Z , jobs , bg to check that process is running


![[Pasted image 20250115135830.png]]

#### Process States:

1. **Running**: The process is either running or ready to run.
2. **Sleeping**: The process is waiting for some event (e.g., input or a resource).
3. **Stopped**: The process is paused (could be resumed later).
4. **Zombie**: The process has finished but still has an entry in the process table.
5. **Idle**: The process is not currently doing anything but waiting for something.
    
6. **Background** = Ctrl-z, jobs and bg  
    
7. **Foreground** = fg   (will show process is running or not )
8. **Run process after exit** = nohup process &    
          OR    
      nohup process > /dev/null 2>&1 &  
9. **kill a process by name** = pkill  
10. **process priority** = nice (e.g nic -n 5 process)    
    => the nice scale goes from -20 to 19. Lower number more priority that task gets
11. **process monitoring** = top  
12. **list process** = ps

**Commands:**  
`pgrep` is a command that looks for processes by name and returns their PID if found. If no output is returned, the process is not running.

```
ps -ef | grep process_name 

pgrep process-name
```

### System Monitoring Commands:

Following are system monitoring commands:  
- **top**: Real-time process monitoring and system resource usage.  
- **df**: system Disk usage or **df -h** (easy human friendly command) - **dmesg**: output of system like messages.  
- **iostat 1**:   input and output stats (disk info) with 1 it will refresh it  
- **netstat:** Displays network connections, routing tables, and interface statistics  
- **free**     Memory usage and system performance monitoring.  
- **cat/proc/cpuinfo**  Read files of CPU info  
- **cat/proc/meminfo** Memory info

### System Log Monitoring:

=> Log Directory = /var/log    
- boot - when your system reboot    
- chronyd = NTP (**Network Time Protocol**)    
- cron - schedule job log activity    
- maillog - email comes in activity recorded    
- secure - records login logout activity    
- messages - imp log to monitor system activities    
- httpd - application log  
1. go in /var/log directory    
2. view list by type ll

==tail -f file-name== (will get new log at the bottom)

### System Maintenance Commands:

- shutdown  
- init 0-6  (0 to shutdown , 6 to reboot  )
- reboot  
- halt - shutdown right away

### Changing Hostname:

To see the file which contains the host-name we use the following command:

```
cat /etc/hostname  
```

For changing the host-name we use the following command:

```
hostnamectl  set-hostname New-hostname  
```

Then after this reboot the system the host-name will be changed.

### Finding System Information:

- To check the version of the operating system we use the following command

```
cat   /etc/redhat-release  
```

- To check a little detail about the operating system we use the following command:

```
uname -a  
```

- ==dmidecode== provides valuable information about the system's hardware, such as the CPU, memory, motherboard, BIOS, and other system components. ==dmidecode | more==

### System Architecture:

- **32-bit:** May struggle with large data operations.
- **64-bit:** More efficient, capable of handling larger operations and better multitasking. To check the architecture of system we us the following command in Linux:

```
arch  
```

this command is long than arch both are used to check how many bits of system is

```
uname -a  
```

### Terminal Control Key:

1. clear
2. exit
3. script :store terminal activities
4. **CTRL-u** --> erase everything you typed on command line  
5. **CTRL-c** --> stop/kill command  
6. **CTRL-z** --> suspend a command  
7. **CTRL-d -**-> exit from interactive program

# Recover Root Password:

### For Linux:

1. **Reboot the system.**
2. **Access the Boot Loader Menu:**
    - For GRUB: Press `Esc` or hold `Shift` while the system is booting.
3. **Edit the Boot Options:**
    - Highlight the default boot entry and press `e` to edit.
    - Find the line starting with `linux` or `linux16`.
    - At the end of this line, append `single` or `init=/bin/bash`.
4. **Boot into Single-User Mode:** - Press `Ctrl + X` or `F10` to boot. - The system will boot into a root shell.
5. **Reset the Password:** passwd
    - - Enter and confirm the new root password.  
        6 **Reboot:** reboot

# sos report:

its diagnostic tool in system This report is often requested by Red Hat Technical Support to help analyze and resolve issues reported in support cases The `sosreport` command is often used when a user needs to provide troubleshooting information to support teams or when they need to analyze system problems.

To generate a report use the following command:

```
sudo sosreport  
```

# Environment Variables :

set defined path Environment variables are essential for configuring the operating system and applications.

### **Common Environment Variables:**

- `HOME`**:** The current user's home directory.
- `PATH`**:** The directories to search for executable files.
- `USER`**:** The username of the current user.
- `SHELL`**:** The path to the current user's shell.
- `LANG`**:** The language and locale settings.

to view all environment variables printevn OR env it will list every directory where path is defined ==echo $path== ==echo $MAIL== ==echo $MAIL== ......and so on

for change directory ==cd $HOME==

**Setting (temporary):**

```
export VAR_NAME=value

Like  export TEST=1 can check by 
echo $TEST
```

**Adding to Profile (permanent):** Edit `/.bashrc` or `/.bash_profile`:

```
export VAR_NAME=value
```

# Special Permissions:

3 permissions in linux these are not actual commands 1. setuid 2. setgid 3. seticky bit (t or T)

- to assign special permissions at the user level

```
         chmog    u+s   xyz.sh
```

- to assign special permissions at the group level

```
         chmog   g+s   xyz.sh
```

- to remove special permissions at the group level

```
         chmog   u-s   xyz.sh
         chmog   g-s   xyz.sh
```

To find all execute-able in linux with setuid and setgid permission

```
find / -perm   /600   -type  f
```

`-type f`**:** only searches regular files

give all permisiions to this directory chmod 777 /allinone ==rm -rf folder-name==

###### seticky bit (t or T)

```
   chmod    +t   /foldername
```

to usnig this +t you have no permission to remove this file