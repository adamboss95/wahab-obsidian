# Linux Kernel:

interface between hardware & software (its program) 
![[Pasted image 20250115173934.png]]

# Shell :

interface between user and kernel echo $0 (to find your shell)

### Types of shell :

1. Bash (Bourne Again Shell)
2. sh (old version of bash)
3. Csh (C Shell):
4. ksh cat/etc/shells (to see list of all shells)

### Shell scripting:

- shell scripting is a executable file containing multiple shells
- always have to explain absolute path for shell scripting
- (/home/userdir/script.bash) 0r ./filen-name
- it should have executable (x) permissions
- #!/bin/bash (for writing script we have to write this in file must )

### Shell Script -Basic Scripts:

- make a folder
- write script #!/bin/bash ==using nano== filename or ==vi file-name==
- give all to executeable permissions with ==chmode a+x filename==
- to display script we can use ==./output-screen==(its filename) or by absolute path

# Input / Output:

1. read (output)
2. echo (input) ![[Pasted image 20250116121543.png]] it will display on screen after giving x permissions to all must mention with $ to get correct output

# if-then scripts:

---> `fi` is opposite to if , that means you can exit outonce work is done --->`-e` is used to check the option that file exists or not ![[Pasted image 20250116123842.png]] # For Loop Scripts: #!/bin/bash

for i in 1 2 3 4 5 do echo "Welcome $i Times" done

# do-while Scripts:

e.g : run a script until 2pm

while [ condition ] do command1 command1 command3 done

**Save and Exit:** Save the file and exit the text editor (in nano, press `Ctrl + X`, then `Y`, and `Enter`).

# !/bin/bash

# this script is created by sania

count=0 num=10 # Do-while loop:

GNU nano 6.2 do-while

# !/bin/bash

# this script is created by sania

count=0 num=10 # Do-while loop

```
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

![[Pasted image 20250116140029(1).png]]
result: 
![[Pasted image 20250116140141(1).png]]

# Case Statement Scripts :

- **Prompt User Input:** The script asks the user to enter a number.
- **Read Input:** The user’s input is read and stored in the variable `num`.
- **Case Statement:**
    - `1)`: If the user enters `1`, the script prints "You entered One."
    - `2)`: If the user enters `2`, the script prints "You entered Two."
    - `3)`: If the user enters `3`, the script prints "You entered Three."
    - `*)`: If the input doesn’t match any of the specified patterns (1, 2, 3), the script prints "Invalid input, please enter a number between 1 and 3." esac ---> used for end task

```
     #!/bin/bash
#this is my script
echo please chosse 1 option
echo
echo 'a = Display Date & TIme '
echo 'b = List of files and direc '
echo 'c = List of users '
echo 'd = Check System up-time '
echo

  read choices
  case $choices in

a) date;;
b) ls;;
c) uptime;;
*) echo invalid choice -Bye

esac
```
![[Pasted image 20250116142127(3) 1.png]]
- output of case script

![[Pasted image 20250116142100(1).png]]



# check other servers connectivity:

A script to check the status of remote hosts checks the connectivity to a list of servers using the `ping` command.

# Aliases:

is used to cut-down on lengthy & repetitive commands ---> If you want to run multiple commands and give them a single nickname, you can use an alias. - alias ls ="ls -al" 
- alias ps ="pwd;
- ls" - alias tell="whoami; hostname; pwd - alias rm= 'rm -i' (This makes `rm` prompt for confirmation before deleting each file.) 
- alias dir="ls -l | grep ^d
- ==grep ^d :== This filters the output of `ls -l` to show only lines that start with the letter `d`. In the long listing format of `ls -l`, directories are indicated by a `d` at the beginning of the line.

- In Linux, an alias is a shortcut or a custom command that allows you to define a simpler or more convenient command for one or more existing commands. Aliases are typically used to simplify repetitive or complex commands.

**Commands:**  
```  
alias ls = "ls -al"  
```

```  
alias pl="pwd; ls"  

```  
To unalias we use following command  use to remove alias commands

```  
unalias pl  
```

# Creating User or Global Aliases :

- **User Aliases:** Limited to the user who defined them.
- **Global Aliases:** Available to all users on the system.

### - **Configuration Location:**

- **User Aliases:** Defined in the user's home directory configuration files (e.g., `/home/user/.bashrc`).
- **Global Aliases:** Defined in system-wide configuration files (e.g., `/etc/bashrc`).

# Shell History:

will show all history you searched or run on terminal history if you got list/history of all commands choose number and type `!number(!86)` it will run that command and give you output