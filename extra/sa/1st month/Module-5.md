## Intro to vi Editor: (text editor)

- inserting & deleting text
- Replacing Text
- Moving around the files
- Finding & substituting strings
- Cutting & pasting text ==vi file name== (to use follow commands)

## Most common Keys :

- i - insert
- Esc - Escape out of any mode
- r ----> replace
- d ----> delete (if you click dd twice it will remove line)
- :q! ----> quit without saving
- :wq! ----> quit and save
- shift+zz ----> (will save file )
- shift+g ----> to go at the end
- u ----> undo
- o ----> insert mode and will create new line
- x ----> will use to remove as well
- a ----> will use to add space between

### sed Command :

- Replace a string in a file with new string or word
- Find & delete a line
- Remove empty line
- To replace tabs with spaces
- show defined line from a file
- Substitute within vi editor

**Common `sed` commands:**  
Most commonly we use sed for substituting text:

```
sed 's/pattern/replacement/' file  
```

```
sed 's/old/new/g' file  
```

The `g` flag tells `sed` to replace **all** occurrences in a line, not just the first one.

```
sed 's/old/new/g' file  
```

To make the changes directly in the file (in-place editing), use the `-i` option:

```
sed -i 's/old/new/g' file  
```

You can use `sed` to delete specific lines or patterns of lines:

```
sed '3d' file

```

You can for deleting a line matching a pattern

```
sed '/pattern/d' file  
```

You can use for deleting a range of lines:

```
sed '2,5d' file  
```

The `-n` option prevents `sed` from printing all lines, and `p` prints the specified line.

```
sed -n '3p' file

```

for removing empty lines in a file we use following command:

```
sed -i  '/^$/d'  
```

substitute/replace within vi    
- replace word  

```
    
:%s/Khan/Khans/ + enter
```

### User Account Management:

- useradd : is used to create a user ==useradd -m (username to create)==
- groupadd ==cat /etc/group== (used to check where is group)

#### Why We Use These Commands

- **groupadd**: To create new groups for managing user permissions and access to resources.
- **cat /etc/group**: To check and verify the existing groups and their details, including which users belong to which groups.
- userdel ==userdel -r (name of user)==
- groupdel ==groupdel (group-name)==
- usermod : The `usermod` command is used to modify or change user account information in Linux. ==usermod -l newname oldname==

Files: - /etc/passwd - /etc/group - /etc/shadow

```
useradd -g superheros -s /bin/bash -c "user description" -m -d /home/spiderman  spiderman
```