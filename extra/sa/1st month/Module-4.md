### Tee Command :

will show out put on screen as well stored data in file

> [!NOTE] echo "its my internship month" | tee file-name echo "its my internship month" | tee -a file-name
> 
> When you use the `tee -a` command, it appends new content to the end of the existing file without overwriting the old content.

to see how many characters are in file , we use command ==wc -c file name== this command use to see all list of directory ==ls -l | tee listdir==

## Pipes:

with help of pipe we can run 2 commands in same time by using | pipe

**more** command is used to see results on 1 screen/page **tail -l** command will show last line of output

```
-ltr |  more

(command 1  arguments  |  command 2  arguments)

```

## File maintenance Commands:

- cp (copy)
- rm (remove)
- mv (move)
- mkdir (create folder)
- rmdir or rm -r (remove a directory)
- chgrp (chnage group)
- chown (change ownership)

```
mv  file-name  new file-name( it will rename 1 file with other name )

mv file-name /foledername (this will use to change location)
```

#### File Display Commands :

- cat (read what inside file)
- more (you can see content at a time on 1 screen)
- less (will show content line by line) ==ls -lts | less== ==less file-name==
- head command will show first 2 line of output ==head -2 filename==
- tail (command will show last 2 line of output ) ==tail -2 filename==

## Filters / Text Processors Commands:

1. cut
2. awk
3. grep and egrep
4. sort
5. uniq
6. wc

**CUT:** cut --version , cut --help , man cut these above commands are used for getting details of cut command

1. ==cut -c1 file-name== this command will help to show first letter of all lines in file
2. ==cut -c1,3,5== this command will help to show 1,3 and 4 letter of all lines in file
3. ==cut -c1-4== this command will help to show 1-4 letter of all lines in file
    1. ==ls -l | cut -c2-4== Only prints user permissions of file/directory

**awk** awk is used for data extraction

1 . ==awk '{print $2}' file-name== by $1 it will show you first column of file

1. ==ls -l | awk '{print $2 , $4}' file-name== by $1 it will show you first column of file

3 . ==awk '/sania/ {print}' file-name== use to search specific word

4 . ==cat file-name | awk '{$2="sania"; print $0}' == ==
        $2 will use to replace 2nd column with sania

5 . ==awk 'length ($0) > 15' file-name== get line that have more than 15 bytes size

1. ==ls -l | awk '{print NF}' == its will show how many columns are in total

**grep and egrep** it allows us to search specific key-word that you are looking for

1. ==grep keyword file-name== we can find specific word or line using keyword -> from file
    
2. ==grep -c keyword file-name== we can find specific word how many times used-> from file
    
3. ==grep -i keyword file-name== we can find specific word if its in small letter or capital letter -> from file
    
4. ==grep -n keyword file-name== we can find specific word and number of line -> from file
    
5. ==grep -v keyword file-name== we can find all other words excluded specific keyword -> from file
    
6. ==ls -l | grep example== filters the results to show only the lines that contain the word "example".
    
7. ==grep -i "keyword|2nd-keyword" file-name== we can find 2 words by using specific keywords -> from file
    

**sort**

> [!NOTE] it is used to sort all columns alphabetically

1. sort file
2. ls -l | sort
    
3. sort -r file will sort file in reverse order
    
4. sort -k2 file will sort 2nd column **uniq**
    

> [!NOTE] will remove duplicates texts

1. uniq filename
2. sort file-name | uniq
3. sort file-name | uniq -c --->(list count) means howmany times duplicate showed up
4. sort file-name | uniq-d (only show repeated lines)

**wc (word count)** - wc --help - wc file (will show what exactly in file) - wc -l file-name (get numbers of lines inside file) - wc -w file-name (number of words in the file ) - wc -b or -c filename ( will show bytes in file) - ls -l | wc -l (list of files)

### Compare files (diff & cmp):

- **diff** command is used to differentiate 2 files line by line **diff first-file 2nd file**
- **cmp** command used to compare 2 files byte by byte **cmp fist-file 2nd file**

Compress & un-Compress Files: tar :

> [!NOTE] tar -cvf archive_name.tar directory_to_compress

gzip :The `gzip` command is used to compress files, reducing their size. gzip -d gunzip :The `gzip -d` and `gunzip` commands are used to decompress files that were compressed with `gzip`.

if your system crash and you cannot resolve issue than we can use it

### Truncate File Size:

this command is used to shrink or extend file size

# truncate -s 10(file size) filename

### Combining & Splitting Files:

- multiple files can be combined into one
- single file can be split into multiple files

==split -l 3 filename new file-name== (in which we are going to split files )

#### Commands ,option & arguments:

1. ls -l file name (command , option ,argument )will show only specific file
2. rm -f directory name(will remove directory without asking or option )
3. rm -r folder name (it will give option to remove)
4. man ls (manual command )(to check command manually)

#### File Permissions :

3 Types of permissions - r: read - w: write - x: execute (running a program)

Each permission (rwx) can be controlled at 3 levels

**u= user (you)** first 3 for user **g= group (people in same group)** 2nd 3 for group **o= other (everyone on the system)** last 3 for others

- chmod (command change permission) with chmod command you can give permission to the users
    
- ==chmod g-w filename== (it will remove write permissions from group )
    
- ==chmod a-r filename== (it will removal all read permissions from file )
- ==chmod u-w file name== (you have no permission to delete file or remove it )
- and if you use + you will get all permissions get back so you can read & write the file

**command #cat is used to read what inside the file**

##### change mode calculator

|0|no permission|chmod 000 filename|it means we are not giving any permission to user group and other to do anything no read , write or executeable|
|---|---|---|---|
|1|execute|chmod 101 file name|user can execute group have no permission and other can execute|
|2|write|chmod 120 filename|-|
|3|execute+write|chmod 321 file name|user can do xw- group can do -w- and other can do --x|
|4|read|-|-|
|5|read+execute|-|--|
|6|read + write|-|-|
|7|read+write+execute|-|-|

**File Ownership:** _User level_ *group level & group level ##### Commands

# chown & #chgrp

---->in these 2 **commands** we can change group and user of the file

#### ACL (Access Control List ):

```
getfacl filename
```

This command displays the ACLs set on the specified file or directory.

```
setfacl -m u:username:permissions(rwx) filename
setfacl -m test:rw /temp/tex
```

This command modifies the ACL to add a user-specific entry. Replace `username` with the user's name and `permissions` with the desired permissions (e.g., `rwx` for read, write, execute).

```
setfacl -m g:group:permissions(rwx) filename
```

To add permissions for group.

**to Remove all entries for all users**

```
setfacl -b  path to filename(test/tex)
```

**to remove a specific entry for a specific user**

```
setfacl -x u:username path to filename(test/tex)
```

### Help Command :

- whatis (write command like #whatis cd or #whatis ls)
- --help ( #ls --help)
- man (man ls)

### Adding Text to file:

1. vi (text editor )to quit from this ---> qw!
2. Redirect command output > or >>
3. echo > or >> (these 2 >> is used for add 2nd lines in the file avoid to overwrite)

```
echo "text enter like my nameis sania" >  BSSE (filename in which you are adding text )
```

**Input & Output :** 1. Standard input (stdin) default file descriptor 0 (cat < filnename) 2. Standard Output(stdout) default file descriptor 1 (ls > filename) 3. Standard Error ( stderr) default file descriptor 2