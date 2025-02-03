- ctrl+c to get prompt back (if you are unable to get prompt use ctrl+c)
- whoami = display loggedin user
- hostname = display hostname
- pwd (print working directory, shows current working directory)
-  to check library behind commands 'strace -e open pwd'
- ls, ls -l, ls -a, ls lt, ls ltr, ls -R, ls -al/-la (list commands)
- cd, cd .., cd foldername, cd ~/Downloads
- mkdir (to create on or many directories) mkrdir file1 file2 (created two files)
- rmdir, rm (to remove directory use rmdir, rm for removing file)
- cp (copy command) , cp file1.txt /path/to/destination/ (copying file1.txt to destination) (more to discover)
- mv oldname newname (to rename a file or directory), mv /path/to/file /new/path (movefile to new location)
- touch newfile (creates an empty file)
- echo "well hello" > newfile (creates a file, where well hello is written)
- cat > filename (to create a file and write in it), cat filename (to display the file), cat file1 file2 > file3 (joins two file into a new file) ("Press ctrl+d to finish writing in cat mode and save file")
- vi
	- echo -e "First line\nSecond line"
	- shift+zz in normal mode to save n exit
- sudo (superuser do, allow regular users to run programs as superuser or root)
- man (manual used for what command does, e.g. man ls)
- history (gives a list of all past commands typed in the current terminal session)
- sudo su root, sudo su 'user'
- command to become **Root User** 'su -'
- **find** command: 
	- find . -name "filename"  
	- to use find in heirarchical way: find / -name "apturl.js"
	- find / -type d -name "directory_name" to ==find directory==
	- find / -type f -name "directory_name" to ==find files==
- **locate** command: locate "filename"
- `setfacl`, `getfacl` (access control list) (setfacl to set the permission, getfacl to display the permissions)

`uname -a` = displays information about OS
`arch` = shows if cpu is 32bit or 64bit 

- sed
	- syntax = `sed 's/keyword/replaceWith/g' filename` = s for substitute, keyword the word that will replace, replaceWith is the word to replace, g for global
	- `sed -i 's/keyword/replaceWith/g' filename` = i is used to make change in the file
	- `sed '/keyword/d' filename` find and deletes a line
- Useradd Commands
	- `-g` (Primary Group) Specifies the primary group for the new user. If the group doesn't exist, you need to create it first using the `groupadd` command.
	- `-s` (Login Shell) Specifies the login shell for the new user. This is the program that runs when the user logs in.
	- `-m` (Create Home Directory) Creates a home directory for the new user. If this option is not specified, the home directory is not created by default.
	- `-d` (Home Directory) Specifies a custom home directory for the new user. If this option is not specified, the default is `/home/username`.
	- `sudo useradd -g developers -s /bin/bash -m -d /custom/home/dir username` This command creates a new user with:
		- Primary group: `developers`
		- Login shell: `/bin/bash`
		- Home directory created: `/custom/home/dir`
- To change date 
	- `sudo date --set="YYYY-MM-DD HH:MM:SS"`
- To change hostname
	- `hostnamectl set-hostname new-hostname`

==To Find IP of domain==
```
host -t a www.facebook.com = find IP address
```

### Key combinations
- ctrl+u = erase everything typed on the command line
- ctrl+c = stop/kill a command
- ctrl+z = suspend a command
- ctrl+d = exit from an interactive program (signals end of data)
#### Hiding file
- use " . " at the start while naming to hide a file e.g. filename = ".folder"

# Recover Root Password
- Restart computer
- Edit grub
	- press e instead of enter to edit when selecting the OS
	- then search for ro
	- remove ro and type there `rw init=/sysroot/bin/sh` > ctrl+x > it will start the computer in single mode user
	- then type `chroot /sysroot` press enter and then type `passwd root` to change root password, enter then type `touch /.autorelabel` to update selinux information, then type `exit` to exit out of sysroot > then type `reboot` to reboot the system
- Change password
- Reboot



### To Check OS and other System Details
- `hostnamectl`