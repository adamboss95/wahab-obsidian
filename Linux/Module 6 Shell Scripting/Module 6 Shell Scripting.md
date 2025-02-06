##### Jan 17, 2025
# SOC Analyst Training
## Linux Training

### Module 6
1. Linux Kernel
- What is a Kernel?
	- Interface between hardware and software
	- ![[Pasted image 20250117094548.png]]

2. What is a Shell?
- What is a Shell?
	- its like a container
	- interface between users and kernel/OS
	- CLI is a Shell
- Find your shell
	- `echo $0`
	- Available Shells `cat /etc/shells`
	- Your Shell? `cat /etc/passwd`

3. Types of Linux Shells
- Gnome = GUI environment in Linux
- KDE = GUI environment
- sh = CLI shell
- bash = stands for born again shell
- csh (cshell) and tcsh (tennex cshell)
- ksh = korn shell

4. Shell Scripting
- What is a Shell Script?
	- A shell script is an executable file containing multiple shell commands that are executed sequentially. The file can contain
		- Shell (#! /bin/bash)
		- Commends (# comments)
		- Commands (echo, cp, grep etc.)
		- Statements (if, while, for etc.)
- Shell script should have executable permissions (e.g. -rwx r-x r-x)
- Shell script has to be called from absolute path (e.g. /home/userdir/script.bash)
- If called from current location then ./script.bash

5. Basic Shell Scripts
- Shell Script-Basic Scripts
	- Output to screen using "echo"
	- Creating tasks
		- Telling your id, current locaion, your files/directories, system info
		- Creating files or directories
		- Output to a file ">"
	- Filers/Text processors through scripts (cut, awk, grep, sort, uniq, wc)
-  ![[Pasted image 20250117103448.png]]
- ![[Pasted image 20250117110114.png]]
- ![[Pasted image 20250117110148.png]]

6. Input and Output of Script
- Input/Output
	- Create script to take input from the user
		- read
		- echo
	- `vim filename` and then put scripts in it
	- ![[Pasted image 20250117112521.png]]
	- ![[Pasted image 20250117112619.png]]

7. if then Scripts
- If then
- ![[Pasted image 20250117120808.png]]
- ![[Pasted image 20250117120849.png]]

8. For Loop Scripts
- For loops keep running until specified number of variable
	- e.g: variable=10 then run the script 10times
	- OR variable = green, blue, red (then run script 3 times for each color)
- For loop script
- ![[Pasted image 20250117121925.png]]
- ![[Pasted image 20250117122227.png]]

9. do-while Scripts
- do while
	- The while statement continually executes a block of statements while a particular condition is true or met
	- e.g: Run a script until 2pm
	- syntax
		- while [ condition ]
		- do
		- command 1
		- command 2
		- commandN
		- done
- ![[Pasted image 20250117124053.png]]
- ![[Pasted image 20250117124150.png]]
- dowhile script 
```
#!/bin/bash
count=0
num=10
while [ $count -lt 10 ]
do
echo
echo $num seconds left to stop this process $1
echo
sleep 1
num=`expr $num - 1`
count=`expr $count + 1`
done
echo
echo $1 process is stopped!!!
echo
```

10. Case Statement Scripts
-  ![[Pasted image 20250117125858.png]]
- Case Statement Syntax
```
#!/bin/bash
echo
echo Please chose one of the options below
echo
echo 'a = Display Date and Time'
echo 'b = List file and directories'
echo 'c = List users logged in'
echo 'd = Check System uptime'
echo
read choice
case $choices in
a) date;;
b) ls;;
c) who;;
d) uptime;;
*) echo Invalid choice - Bye.;;
esac
```
- This script will look at your current day and tell you the state of the backup
```
#!/bin/bash
NOW=$(date +"%a")
case $NOW in
Mon)
echo "Full backup";;
Tue|Wed|Thu|Fri)
echo "Partial backup";;
Sat|Sun)
echo "No backup";;
*) ;;
esac
```

11. Check Remote Servers Connectivity
- Check other servers connectivity
	- A script to check the status of remote hosts
		- ![[Pasted image 20250117173525.png]]
- Syntax 
```
#!/bin/bash

ping -c1 192.168.1.1
        if [ $? -eq 0 ]
        then
        echo OK
        else
        echo NOT OK
        fi
```

- Change ip and check
```
#!/bin/bash

hosts="192.168.1.1"
ping -c1 $hosts &> /dev/null
        if [ $? -eq 0 ]
        then
        echo $hosts OK
        else
        echo $hosts NOT OK
        fi
```
Change the IP to something else and check

- Multiple IPs
```
#!/bin/bash

IPLIST="path_to_the_Ip_list_file"


for ip in $(cat $IPLIST)

do
   ping -c1 $ip &> /dev/null
   if [ $? -eq 0 ]
   then
   echo $ip ping passed
   else
   echo $ip ping failed
   fi
done
```

12. Aliases
- Syntax for creating alias
- alias nick = "command"
	- e.g alias ls="ls -la" , whenever i run ls it will give the output of the ls -la  
- we can create alias for multiple commands too
	- `alias ls="ls -al"`
	- `alias pl=pwd: ls"`
	- `alias tell="whoami; hostname; pwd"`
	- `alias dir="ls -l | grep ^d"`
	- `alias lmar=ls -l | grep Mar"`
	- `alias gwa= "chmod a+w"` (give writing access)
	- `alias gra="chmod a+r"` (give reading access)
	- `alias gxa="chmod a+x"` (give executable access)
	- `alias d="df -h | awk '{print \$6}' | cut -c1-4`
- To Delete Alias, use `unalias commandtodelete`
	- e.g `unalias ls` will delete ls from alias
- To Display Alias,  `alias`

13. Creating User or Global Aliases
- User = Applies only to a specific user profile
	- to set aliases for specific user, need to edit the file with vi or vim and add the alias there
		- User = ==/home/user/.bashrc== is where user alias file is located
- Global = Applies to everyone who has account on the system
- to set aliases for everyone on the system, need to edit the file with vi or vim and add the alias there
	- Global = ==/etc/bashrc== is where global alias file is located

14. Shell History
- All commands are recorded in the history
- history is effective for troubleshooting
- all commands history can be viewed by `history`
- commands can be seen and run again using the number allocated to those commands
- e.g in history the ls -ltr command is on 306 number, the same command can be run by using `!306` , it will run ls -ltr
- The location of file history where shell commands are save = ==/home/username/.bash_history ==
- To view other users history of shell commands
	- Become root `sudo su`
	- `cat /home/users-dir-name/.bash_history`