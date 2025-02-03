##### Jan 10, 2025
# SOC Analyst Training
## Linux Training

### Module 4
1. **Linux Command Syntax**
	- Command Option(s) Argument(s)
	![[Pasted image 20250110093130.png]]
	- ls is command, -l is option, straw* is argument

2. **File Permissions**
	- Two types
		- Symbolic Mode
		- Absolute Numeric Mode
	- Giving or removing permission/access to user, to protect from or make file or directory accessible.
3. **Symbolic Mode Permissions**
	- 3 types of permissions
		-  r = read
		-  w = write
		-  x = execute = running a program
	- Permissions can be controlled on three levels:
		- u = user = yourself
		- g = group
		- o = other = everyone
		- a = all
	- Permissions can be displayed by running ls -l command
		- -rwxrw-r--
	- Command to change permission 
		- chmod
```
chmod g-r+w-x file1
```
```
chmod u+x file1
```
```
chmod o+r-w file1
```
```
chmod a+r+w-x file1
```
```
chmod a-w+x file1
```
```
chmod o-wx file1
```
![[Pasted image 20250110094636.png]]
![[Pasted image 20250110101620.png]]
![[Pasted image 20250110101737.png]]
![[Pasted image 20250110101859.png]]
![[Pasted image 20250110101954.png]]
![[Pasted image 20250110102231.png]]
- looking at the terminal, here - means no access, r means read access only, w means write (read, edit, renaming) access, x means execute access
- in -rw-rw-r-- the first three characters after initial - are user/owner permission/access, the middle three characters -rw is for group permission/access, the last three characters r-- is for permission/access for the others/everyone.

4. **Absolute Numeric Mode Permissions**
![[Pasted image 20250110103557.png]]
![[Pasted image 20250110102837.png]]
```
chmod 000 file1
```
```
chmod 764 file1
```
![[Pasted image 20250108150127.png]]
- ==Alternate way to get numeric codes is to search chmod calculator on browser to get the numeric code==

5. **File Ownership**
- Two Owners of file
	- User
	- Group
- Command to change ownership
	- chown = changes ownership of file
	- chgrp = changes group ownership of file
- to  change ownership to root or from root we need to either be the root account or use superuser sudo
```
sudo chown root file2
```
![[Pasted image 20250110111507.png]]
```
sudo chgrp root file2
```
![[Pasted image 20250110111612.png]]

6. **Access Control List (ACL)**
- ACLs allows to set specific permissions for individual users or groups, beyond the traditional owner/group/other permissions


- `getfacl`: Retrieves and displays ACLs.
```
getfacl roger
```
![[Pasted image 20250110115512.png]]
- - `setfacl`: Sets or modifies ACLs.
```
sudo setfacl -m u:abdulwahab:rw roger
```
![[Pasted image 20250110115716.png]]
```
sudo setfacl -m g:test:rw roger
```
![[Pasted image 20250110115954.png]]
```
sudo setfacl -m g:test:r-- roger
```
==to remove access from a user we use -==
![[Pasted image 20250110120253.png]]
```
sudo setfacl -x g:test roger
```
==to remove full access of group test==
![[Pasted image 20250110120523.png]]
```
sudo setfacl -b roger
```
==to remove all permissions and return back to its original form==
![[Pasted image 20250110120752.png]]
==only the owner of the file can remove a file not those that has permissions to rwx==

7. **Help Commands**
- 3 types
	- `whatis` command (`whatis ls`,`whatis setfacl`)
		- ![[Pasted image 20250110121819.png]]
	- command `--help` (`touch --help`)
		- ![[Pasted image 20250110121908.png]]
	- `man` command (`man touch`)
		- ![[Pasted image 20250110122036.png]]
 8. **Tab completion and Up Arrow Keys**
 - Hitting Tab key after a certain command or name completes the available commands, files or directories
	 - if i write `ls -l str` and press tab it will show me complete the str, if i press tab again it will show me all the available files which start with str
		 - ![[Pasted image 20250110122810.png]]
			- here i wrote `ls -l str` then pressed tab and it completed the file name starting with "str"
		- ![[Pasted image 20250110122937.png]]
			- here i pressed tab twice and it showed me all file names having "strawhats"
- Hitting up arrow key returns the last command ran.
9. **Adding Text to Files (Redirects)**
- 3 ways to add test to a file
	- vi
		- shift zz in normal mode to save n exit
	- Redirect command output > or >>
	- echo > or >>
```
echo "add text" > pirateking
```
```
echo "add text without removing whats already in the file using >>" >> pirateking
```
![[Pasted image 20250110125559.png]]
==`echo "add text" > pirateking` will overwrite the file==
10.  **input and output redirects**
- stdout = standard output
- `stdout` **(Standard Output)**: This is the output stream where a program writes its output data. By default, `stdout` is the terminal display, but it can be redirected to files or other output streams. For example, you might use `echo "Hello, World!" > output.txt` to write "Hello, World!" to `output.txt`.
```
ls -ltr > filename
```
![[Pasted image 20250110145522.png]]
```
pwd > filename
```
![[Pasted image 20250110145540.png]]
```
ls -ls >> filename
```
![[Pasted image 20250110145641.png]]
- stdin = standard input
- `stdin` **(Standard Input)**: This is the input stream where data is sent to and read by a program. By default, `stdin` is the keyboard input, but it can also be redirected from files or other input sources. For example, you might use `cat < myfile.txt` to read the contents of `myfile.txt`.
```
cat < filename
```
==if we type `cat filename` it would display the same==
![[Pasted image 20250110153935.png]]
- to copy the error of a command to a specific file
```
ls -et 2> filename
```
![[Pasted image 20250110160134.png]]

11. **Standard Output to a File (tee)**
- tee is used to create and display a file simultaneously
 ```
 echo "add text" | tee filename
```
![[Pasted image 20250110162348.png]]
- to append text to a file using tee
```
echo "add text" | tee -a filename
```
![[Pasted image 20250110162625.png]]
- another way to use tee command
```
ls -ltr | tee filename
```
![[Pasted image 20250110162927.png]]

12. **Pipes**
- A pipe (`|`) in the Linux terminal allows you to take the output of one command and use it as the input for another, enabling you to chain commands together efficiently.
```
ls -ltr | more
```
![[Pasted image 20250110165517.png]]
- this command shows the list page by page. (press space to continue to view next, press q to quit)
```
ls -ltr | tail -1
```
![[Pasted image 20250110170239.png]]

13. **File Maintenance Commands**
- cp = to copy a file or directory
![[Pasted image 20250110175550.png]]
![[Pasted image 20250110175836.png]]
- rm = to remove a file
![[Pasted image 20250110180024.png]]
- mv = to move or rename a file or directory

- mkdir = to create directory
- rmdir or rm -r = to remove directory
- chgrp = to change group ownership
- chown = to change user ownerhsip

14. **File Display Commands**
- cat = displays the contents of file 
- more = one page at a time of file `q` to quit
	- Forward-only navigation.
	- limited search capability
	- - **Scroll Down**: Press `Spacebar` or `Page Down`.
	- **Exit**: Press `q`
```
more filename
```
- less = advanced version, Bidirectional navigation (forward and backward).
	- **Scroll Down**: Press `Spacebar` or `Page Down`.
	- **Scroll Up**: Press `b` or `Page Up`.
	- **Search**: Type `/search_term` and press `Enter` to search forward.
	- **Exit**: Press `q`
```
less filename
```
- head = shows the beginning of a file.
	- `head -5 filename` Displays the last 5 lines of `filename`
	- `head -c 1000 filename` Displays the last 1000 bytes of `filename`.
	- `head -n 10 filename` displays first 10lines
- tail = shows the end of a file.
	- `tail -5 filename` Displays the last 5 lines of `filename`
	- `tail -c 1000 filename` Displays the last 1000 bytes of `filename`.
	- `tail -n 20 filename` displays the last 20lines
	- `-f` Continuously monitors `filename` for new lines added to the file. Particularly useful for watching log files.
```
tail -5 filename
```
```
tail -c 1000 filename
```
```
tail -f filename
```

15. **Filters / Text Processors Commands**
- cut
- awk
- grep and egrep
- sort
- uniq
- wc

16. **cut Text Processors Commands**
- cut
	- cut filename = doesnt work
	- `cut -c1 filename` = List one character
	- `cut -c1,3,5,6 filename` = pick and choose character
	- `cut -c1-5 filename` = list range of characters
	- `cut -c1-6,10-15 filename` = list specific range of characters
	- `cut -b1-3 filename` = displays 3 bytes information = list by byte size
	- `cut -d: -f 6 /etc/passwd` = list first 6th column separated by :
	- `cut -d: -f 6-7 /etc/passwd `= list first 6 and 7th column seperated by :
	- `ls -l | cut -c2-4` = Only print user permissions of files/dir
17. **awk Text Processors Commands**
- awk = 
	- `awk '{print $1}' filename` = displays first column of filename
	- `ls -l | awk '{print $1,$3}'` = list 1 and 3rd column of ls -l output
	- `ls -l | awk '{print $NF}'` = last field of output
	- `awk '/monkey/ {print}' filename` = searches word luffy in file and displays the line where luffy is
	- `awk -F: '{print $1}' /etc/passwd` = output only 1st field/column of /etc/passwd
	- `echo "Hello Garp" | awk '{$2="Adam"; print $0}'` = replace words 2nd column/field words
	- `cat filename | awk '{$2="pirate"; print $0}' ` = replace words field words
	- `awk  'length($0) > 10' filename`= get lines that have more than 10 byte size
	- `ls -l | awk '{if($9 == strawhats) print $0;}'` = get the field matching strawhats in current directory
	- `ls -l | awk '{print NF}'` = displays number of fields
![[Pasted image 20250113104752.png]]
![[Pasted image 20250113105017.png]]
![[Pasted image 20250113105731.png]]
![[Pasted image 20250113105958.png]]
![[Pasted image 20250113110335.png]]
![[Pasted image 20250113111055.png]]
![[Pasted image 20250113111512.png]]
![[Pasted image 20250113111750.png]]
![[Pasted image 20250113112853.png]]
![[Pasted image 20250113113141.png]]

18. **grep/egrep Text Processors Commands**
- grep
	- stands for "global regular expression print." processess text line by line and prints any lines which match a specified pattern
	- `grep` used for simpler pattern matching with basic regular expressions.
	- `grep monkey strawhats` = searches and displays the line having monkey in it in the file strawhats
	- `grep abdulwahab /etc/passwd` = displays the line that has abdulwahab in it
	- `grep -c keyword filename` = displays the count of lines having the specific word
	- `grep -i keyword filename` = search for a keyword ignoring case-sensitive
	- `grep -n keyword filename` = display the matched lines and their line numbers
	- `grep -v keyword filename` = display everything but keyword
	- `grep -vi keyword filename | awk '{print $1,$2}'` = displays 1 and 2nd field (i in the -vi is for ignoring case-sensitive)
	- `grep -vi keyword filename | awk '{print $1,$2}' | cut -c1-4`
![[Pasted image 20250113115000.png]]
![[Pasted image 20250113115512.png]]
![[Pasted image 20250113115551.png]]
![[Pasted image 20250113115753.png]]
![[Pasted image 20250113115900.png]]
![[Pasted image 20250113120048.png]]
![[Pasted image 20250113120604.png]]
![[Pasted image 20250113120850.png]]
- egrep
	- `egrep` (or `grep -E`) used for more complex pattern matching with extended regular expressions, which offer greater flexibility and power.
	- `grep -i "keyword|keyword" filename'
	- `egrep "m(onkey|onet)" filename`
![[Pasted image 20250113122800.png]]
![[Pasted image 20250113123337.png]]

19. **sort/uniq Text Processors Commands**
- Sort and uniq commands
	- Sort Command sorts in alphabetic order
	- Uniq command filters out the repeated or duplicate lines
	- `sort filename` = sorts file in aphabetic order
	- `sort -r filename` = sorts file in reverse aphabetic order
	- `sort -k2 file` = sort by field number
	- `ls -l | sort -k9` = sort ls -l from field 9
	- uniq filename = the contents must be sorted first for uniq to work properly
	- `sort filename | uniq`
	- `sort filename | uniq -c` = display uniq with count
	- `sort filename | uniq -d` = only display repeated lines
	- ls -l | sort | uniq 
![[Pasted image 20250113123843.png]]
![[Pasted image 20250113124038.png]]![[Pasted image 20250113124717.png]]
![[Pasted image 20250113125050.png]]
![[Pasted image 20250113130334.png]]
![[Pasted image 20250113141356.png]]
![[Pasted image 20250113141619.png]]

20. **wc Text Processors Commands**
- wc = word counter, displays line, words and bytes of a file
	- `wc filename` = display line, words, bytes
	- `wc -l filename` = display number of lines only
	- `wc -w filename` = display number of words only
	- `wc -c filename` = display number of bytes
	- `ls -l | grep ^d | wc -l` = display all  that have d at the start, this command is to show how many directories we have
	- `grep akainu marines | wc -l` = to show count of akainu in file
![[Pasted image 20250113142801.png]]
![[Pasted image 20250113143813.png]]

21. **Compare Files**
- diff = shows the differences in a unified format, highlighting lines that need to be changed.
	- `diff admirals admirals2`
![[Pasted image 20250113145443.png]]
- cmp = shows the differences in a unified format, highlighting lines that need to be changed.
	- `cmp admirals admirals2`
![[Pasted image 20250113145541.png]]

22. **Compress and un-Compress Files**
- tar 
	- tar cvf filename . = create tar of the current directory
	- tar xvf filename = un tar in the current directory
![[Pasted image 20250113152942.png]]
- `gzip filename` = zip a file
![[Pasted image 20250113153007.png]]
- gzip -d or `gunzip filename` = unzip file
![[Pasted image 20250113153038.png]]
23. **Truncate File Size**
- command used to shrink or extrend size of file to specified size
	- `truncate -s 150 filename` 
		- reducing the size of file will remove contents of the file with it and increasing the size with truncate wont bring back the lost contents of the file
![[Pasted image 20250113154432.png]]
![[Pasted image 20250113154554.png]]

24. **Combining and Splitting Files**
- Multiple files can be combined into one
- One file can be split into multiples files
	- `cat file1 file2 file3 > file4`
	- `split -l 2 file4` = split 2 lines per file 
![[Pasted image 20250113155758.png]]
![[Pasted image 20250113155700.png]]

25. **Linux vs Windows Commands**
- ![[Pasted image 20250113160122.png]]