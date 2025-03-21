##### Jan 09, 2025
# Linux Training

## Module 3
### 1. Access to Linux
	- two types 1. Console, 2. Remote

### 2. Access to Linux via Putty (Putty used for access to Linux using windows)

### 3. Command Prompts and Getting Prompts Back

### 4. Introduction to Linux File System

### 5. File System Structure and its Description
- to check library behind commands 
```
strace -e open pwd
```

**/boot**

Contains file that is used by the boot loader (grub.cfg)

**/root**

root user home directory. It is not same as /

**/dev** 

System devices (e.g. disk, cdrom, speakers, flashdrive, keyboard etc.)

**/etc** 

Configuration files

**/bin → /usr/bin** 

Everyday user commands

**/sbin → /usr/sbin** 

System/filesystem commands

**/opt** 

Optional add-on applications (Not part of OS apps)

**/proc**

Running processes (Only exist in Memory)

**/lib → usr/lib**

C programming library files needed by commands and apps.

Check which libraries the command use

```
strace -e open pwd
```

**/tmp**

Directory for temporary files

**/home**  

Directory for user

**/var**  

System logs

**/run**  

System daemons that start very early (e.g. systemd and udev) to store temporary runtime files like PID files

**/mnt**  

To mount external filesystem. (e.g. NFS)

**/media**  

For cdrom mounts.

**Structure**

![[Linux File System Structure.png]]

### 6. Linux File or Directory Properties

### 7. Linux File Types
- ![[Pasted image 20250109105003.png]]

### 8. What is Root?
**3 types of root on Linux system**

1. *Root account :* most powerful account.

2. *Root as /:*  very first directory in Linux also called root directory

3. *Root home directory:* the root use account home directory

- ![[Pasted image 20250109105730.png]]

### 9. Changing Password in Linux
```
passwd userid
```

- ![[Pasted image 20250109112118.png]]

### 10. File System Path
Two paths
- Absolute Path
- Relative Path

**Absolute Paths**

This indicates that the path starts at the root directory.

*Begins with a '/'.* 

```
cd /var/log/httpd
```

**Relative path**

Identifies the path relative to your current location.

*Not Begins with a '/'.* 

```
cd Desktop
```

### 11. Creating Files and Directories
- ![[Pasted image 20250109113009.png]]
- to create file with touch, and to create file with cp
```
touch filename , cp filename newfilename
```

- ![[Pasted image 20250109113840.png]]
- to create multiple files with touch
```
touch filename1 filename2 filename 3
```

- ![[Pasted image 20250109114557.png]]
- vi (to save and quit editor use command ':wq!' or shift+zz)
```
vi filename
```

- ![[Pasted image 20250109114504.png]]
- mkdir to create directory
```
mkdir directoryName
```
- ![[Pasted image 20250109114838.png]]

### 12. Copying Directories
- copying elders directory into folder5 and naming it as EldersBackup
	- ![[Pasted image 20250109115858.png]]
- using mv command to move single or multiple files to another directory, in this case moving multiple files at once using absolute path
```
mv tom jerry spike /home/abdulwahab/Downloads/folders5/folder9
```
- ![[Pasted image 20250109120922.png]]

### 13. Finding Files and Directories find locate
	- two commands to find file/directories
		1. find
```
find . -name "filename"
```
- ![[Pasted image 20250109122037.png]]
- to use find in hierarchical way
```
find / -name "apturl.js"
```
- ![[Pasted image 20250109124637.png]]
- locate
	- to locate database, needs to be updated
	- to update database, use command 'updatedb'
- had to install a package for locate to work
	- to install the package 
```
sudo apt install plocate
```

- e.g. i want to find where the file named whitebeard is located
```
locate whitebeard
```
- ![[Pasted image 20250109122627.png]]
- Find vs Locate
	- **Find** searches file system while **locate** searches database

### 14. WildCards
- three type  * , ? , [] 
- * = (asterisk)
	- i want to remove the files whos name starts from straw using *
```
rm straw*
```
![[Pasted image 20250109163313.png]]
- heres another example
![[Pasted image 20250109165842.png]]
- ? = (question mark)
	- to check files whos name is straw but i dont remember the whole name
```
ls -l str?aw*
```
- [] = (brackets)
	- if i want to display files in a directory that have rht in it
```
ls -l *[rht]*
```
![[Pasted image 20250109165540.png]]


### 15. Soft and Hard Links
- inode = a number assigned by the computer to a file that we create or is created
- soft link = a link that will be removed if file is removed or renamed
```
ln -s
```

- hard link = removing or moving the file doesn't affect the hard link
```
ln
```

![[Pasted image 20250109171057.png]]

- **Soft Link**: created a file named dragon in folder10 directory, then added a text to the file using echo, then created a link from previous folder5 directory, used cat to display the contents of the file from the created link

![[Pasted image 20250109172634.png]]

```
touch folder10/dragon
```

```
echo "one piece is real" > folder10/dragon
```

```
ln -s folder10/dragon
```

```
cat dragon
```

```
rm folder10/dragon
```
- after removing the soft link gets broken and doesn't display the contents of the removed file
- **Hard Link**: created a file named garp using touch, created a hard link using ln in the same partition but different directory, used echo to add text to the file, using cat to display contents of link showed contents of the garp file that i created earlier
```
touch folder10/garp
```

```
ln folder10/garp
```

```
echo "vice admiral garp" > folder10/garp
```

```
cat garp
```

```
cat folder10/garp
```

```
rm folder10/garp
```

```
cat garp
```

![[Pasted image 20250109175036.png]]
- after removing the garp file in folder10 directory, the hard link still shows the content of removed file


### 16. Navigating File System

Changing Directory

```
cd
```

Print working directory

```
pwd
```

List the content of directory

```
ls
```

### 17. Linux File Types

**File Symbol** ---> *Meaning* 

 **\-** ---> *Regular file*
 **d** ---> *Directory*
 **l** ---> *link*
 **c** ---> *special file or device file*
 **s** ---> *socket*
 **p** ---> *named pipe*
 **b** ---> *block* *device*
