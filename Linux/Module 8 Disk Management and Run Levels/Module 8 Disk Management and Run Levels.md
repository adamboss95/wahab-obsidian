

### System Run Level 

• System Run Levels 

Main Run level

| 0   | Shut Down (or Halt) the system            |
| --- | ----------------------------------------- |
| 1   | Single-user mode; usually aliased as s or |
| 6   | Reboot the system                         |

| 2   | Multiuser mode without networking |
| --- | --------------------------------- |
| 3   | Multiuser mode with networking    |
| 5   | Multiuser mode with networking    |
Please note run level 4 is undefined or not used/User-definable

Commands: 

For Shutdown 
```
init 0 
```

For Single User mode 
```
init 1 
```

For Multiuser mode without networking 
```
init 2 
```

For Multiuser mode with networking 
```
init 3 
```

For Multiuser mode with networking and GUI 
```
init 5 
```

For Reboot the system 
```
init 6 
```

For checking which run level you are in 
```
who -r
```


### Computer Boot Process


![[Pasted image 20250128172248.png]]


### Linux Boot Process

![[Pasted image 20250128172354.png]]


### Linux Boot Process (Newer Version) 
    
• The boot sequence changes in CentOS/Redhat 7 and above 

• systemd is the new service manager in CentOS/RHEL 7 that manages the boot sequence 

• It is backward compatible with SysV init scripts used by previous versions of RedHat Linux including RHEL 6 

• Every system administrator needs to understand the boot process of an OS in order to troubleshoot effectively 

**BIOS** = Basic Input and Output Setting (firmware interface) 

**POST** = Power-On Self-Test started 

**MBR** = Master Boot Record 

Information saved in the first sector of a hard disk that indicates where the GRUB2 is located so it can be loaded in computer RAM 

**GRUB2** = Grand Unified Boot Loader v2 

**Loads Linux kernel** 

/boot/grub2/grub.cfg 

**Kernel = Core of Operating System** 

Loads required drivers from initrd.img 

Starts the first OS process (systemd) 

**Systemd = System Daemon (PID # 1)** 

It then starts all the required processes 

Reads = /etc/systemd/system/default.target to bring the system to the 

run-level 

Total of 7 run-levels (0 thru 6)


### Message of the Day 
    
• Message of the day file location 

 /etc/motd 

Commands: 

1. Edit the motd
```
vi /etc/motd 
```

2. Type your message 
    
3. Save and exit 
    
4. cat /etc/motd


### Customize Message of the Day 
    

• Once again, message of the day is the first message users will see when they login to the Linux machine 

Steps: 

• Create a new file in /etc/profile.d/motd.sh 

• Add desired commands in motd.sh file 

• Modify the /etc/ssh/sshd_config file to edit 
	#PrintMotd yes to PrintMotd no 

• Restart sshd service 
```
systemctl restart sshd.service 
```

You can also check by run the file 
```
./motd.sh
```


### Computer Storage 
    
There are 4 type of local storage in your PC 

1. **Local Storage** e.g: RAM,HDD,SSD,etc 
    
2. **DAS** (Direct Attached Storage) e.g: CD/DVD, USB flash drive, external disk directly attached with USB or other cables 
    
3. **SAN** (Storage Area Network) 

-  Storage attached through iSCSI or fiber cable 


4. **NAS** (Network Attached Storage) 

- Storage attached over network (TCP/IP) 
    
- E.g: Samba, NFS etc 
    

### Disk Partition 
    

 Commands for disk partition: 

```
df –h
```
 -h for human readable format

Created alias for df –h = dinfo 

• fdisk 

### Adding Disk and Creating Partition 
    
• Purpose?  

 Out of Space, Additional Apps etc. 

• Commands for disk partition 

df 

fdisk 

### LVM – Logical Volume Management 

- **LVM** allows disks to be combined together

- Imagine you have three 100 GB hard drives. Using LVM, you combine them into a single 300 GB storage pool. You create three logical volumes: 50 GB for your OS, 100 GB for your games, and 150 GB for your files. If your game volume fills up, you can resize it without any hassle, adding more space from the 300 GB pool.

- **Simple Analogy**: 

###### Imagine a Bookshelf System

Think of your computer's storage as a collection of bookshelves:

1. **Physical Volumes (PVs):** These are your actual bookshelves (hard drives, SSDs). Imagine you have three bookshelves.
    
2. **Volume Groups (VGs):** You can combine these bookshelves into one large library. This large library is called a Volume Group. Now, you have all your book space (storage space) in one place, making it easier to manage.
    
3. **Logical Volumes (LVs):** Inside this large library, you can create smaller sections (logical volumes) to organize your books. You can create a section for fiction, another for non-fiction, and another for reference books. These sections act like virtual partitions that you can easily resize or rearrange without needing a new bookshelf.

![[Pasted image 20250129095642.png]]

### LVM Configuration During Install 
    

• Install Linux CentOS with LVM configuration 

STEPS: 

- Open VM 
    
- Click new 
    
- Give name LVM-LinuxOS 
    
- Create VM 
    
- When reached on Setup click on Installation destination 
    
- Click on hard disk and on partitioning click on I will configure partitioning and done 
    
- LVM is selected and + Add  
    
- It will ask you mount point select /home and desired capacity type 2g 
    
- File system type xfs 
    
- You can select another partitioning as well 
    
- And click on done 
    
- And when your setup is done go in terminal and `df –h` now you can see the disk info


### Add Disk and Create LVM Partition

![[Pasted image 20250129095854.png]]



**Commands:**

- Display detailed information about the partitions on all available storage devices 
```
fdisk –l
```
 
- Create disk partition Practical Work 
    
1. fdisk /dev/sdc[diskname] 
    
2. Hit enter 
    
3. Press `n` for new partition 
    
4. Press `p` for primary 
    
5. By default partition number is 1 
    
6. By Default sector is 2048 
    
7. Size of sector by default 2097151 
    
8. Everything is done now hit p and now you will see the disk partition is created 
    
9. As you are doing LVM press t for change partition system id 
    
10. Press `L` and Now a list will appear and LVM is associated with 8e 
    
11. Type `8e` and hit enter 
    
12. To check system is Linux LVM press `p` 
    
13. And to write to it press `w` 
    
14. Now we have to create a physical volume 
    
15. To create a physical volume type `pvcreate /dev/sdc1[name and partition number 1]` 
    
16. Hit enter and it will be successfully created  
    
17. To check `pvdisplay` and it will tell you everything about that physical volume 
    
18. To create a volume group `vgcreate linux_vg[name] /dev/sdc1[assigning to]` and hit enter 
    
19. Volume group is created now to verify it `vgdisplay linux_vg` 
    
20. Now to create a logical volume `lvcreate –n[new] linux_lv –size 1G linux_vg` 
    
21. For verify `lvdisplay` 
    
22. Assign file system `[makefilesystem]mkfs.xfs /dev/linux_vg/linux_lv` 
    
23. Create directory for mount logical volume `mkdir /linux` 
    
24. For Mount logical volume `mount /dev/linux_vg/linux_lv /linux` 
    
25. And verify it by `df -h`


> [!NOTE]
> If you want to mount this partition at boot time then edit the /etc/fstab file and add the following line 
> 
> `/dev/linux_vg/linux_lv /linux xfs defaults 0 0`

### Add and Extend disk using LVM 
    
/oracle = 1.0G 

/oracle = Full 

Few Options: 

• Delete older files to free up disk space 

• Add new physical disk mount to /oracle2 

• Create a new virtual disk and mount to /oracle2 

• Or extend /oracle through LVM. 

Practical Work: 

1.  Become root 
    
2. View details about disk by `fdisk –l | more` 
    
3. Partition disk by `fdisk /dev/sdd[diskname]` 
    
4. For new disk hit `n` 
    
5. For Primary disk hit `p` 
    
6. For default partition number hit enter 
    
7. For first sector hit enter 
    
8. For last sector hit enter 
    
9. For checking disk hit `p` 
    
10. Hit `t` for assigning system 
    
11. For list hit `L` 
    
12. For LVM hit `8e` 
    
13. Hit `p` for checking system type Linux LVM 
    
14. For write and create partition hit `w` 
    
15. Reboot the system for updated partition 
    
16. After system is reboot become root again 
    
17. Type `pvdisplay` or `pvs` to check which disk is associated with which disk 
    
18. For display of VG Size and much more information of our disk type `vgdisplay linux_vg` 
    
19. To create physical volume `pvcreate /dev/sdd1` and hit enter 
    
20. To extend group `vgextend linux_vg /dev/sdd1` and hit enter 
    
21. To extend logical volume `lvextend –L+1024M [path from df –h filesystem] /dev/mapper/linux vg-linux_lv` 
    
22. To extend file system `xfs_growfs [path from df –h filesystem] /dev/mapper/linux vg-linux_lv` 
    
23. Now again `df –h` to see your size is extended from 1gig to 2gig


### Add/Extend Swap Space 
    

- What is swap? – CentOS.org 

- **Swap** in Linux is like an extension of your computer's memory (RAM). Think of it as a backup memory area that your computer can use when it runs out of actual RAM.

- **Swap** space is used when your RAM is full. It provides extra memory space by using a portion of your hard drive.

- **Swap space** in Linux is used when the amount of physical memory (RAM) is full. If the system needs more memory resources and the RAM is full, inactive pages in memory are moved to the swap space. While swap space can help machines with a small amount of RAM, it should not be considered a replacement for more RAM. Swap space is located on hard drives, which have a slower access time than physical memory. 

- Recommended swap size = Twice the size of RAM 

	M = Amount of RAM in GB, and S = Amount of swap in GB, then 
	
	If M < 2 
	
	Then S = M *2 
	
	Else S=M+2 

- Commands 
```
dd
```

```
mkswap
```

```
swapon or swapoff
```
 
- To check free memory 
```
Free –m
```
 
- Create a file with command to give memory 
```
dd if=/dev/zero of=/newswap[filename] bs=1M count=1024
```


> [!NOTE]
> you can also create a file by touch command but touch command create a empty file and by this you give memory  
> 

- Assign permissions to file 
```
chmod go-r newswap ls –ltr
```
 
- Make swap 
```
Mkswap /newswap
``` 

- Add swap and total memory increase 
```
swapon /newswap
```

- To delete swap 
```
swapoff /newswap
```

- 
```
rm /newswap
```



### Advance Storage Management with Stratis

**Stratis** is like a smart library system for your computer's storage. It helps you organize and manage your data more efficiently by grouping storage devices into pools and creating flexible filesystems within those pools.

**Simple Analogy**

###### Imagine a Library System

Think of your computer's storage as a library system:

1. **Books (Data):** Your files and data are like books in the library.
    
2. **Shelves (Physical Volumes):** The physical storage devices (like hard drives or SSDs) are like shelves where you keep the books.
    
3. **Library Sections (Pools):** Stratis allows you to group multiple shelves together into sections (pools). This makes it easier to manage all your books in one place.
    
4. **Book Sections (Filesystems):** Inside each section, you can create smaller areas (filesystems) to organize your books by genre, author, etc.


![[Pasted image 20250129143038.png]]

1. Install Statris package 
```
yum/dnf install stratis-cli stratisd
```
 
2. Enable and start Statris service 
```
systemctl enable|start stratisd
```
 
3. Add 2 x 5G new disks from virtualization software and verify at the OS level 

4. Oracle virtualbox storage setting 
```
lsblk 
```

5. Create a new stratis pool and verify 
```
stratis pool create pool1 /dev/sdb
```

```
stratis pool list
```
 
6. Extend the pool 
```
stratis pool add-data pool1 /dev/sdc
```
 
```
stratis pool list
```
 
7. Create a new filesystem using stratis 
```
stratis filesystem create pool1 fs1
```
 
```
stratis filesystem list
```
Filesystem will start with 546 MB 

8. Create a directory for mount point and mount filesystem 
```
mkdir /bigdata
```

```
mount /dev/stratis/pool1/fs1 /bigdata 
```

```
lsblk
```

9. Create a snapshot of your filesystem 

```
startis filesystem snapshot pool1 fs1 fs1-snap 
```

```
stratis filesystem list 
```

10. Add the entry to /etc/fstab to mount at boot 
```
UUID=“asf-0887afgdja-” /bigdata xfs defaults,x- systemd.requires=stratisd.service 0 0

```

### RAID

**RAID** stands for **Redundant Array of Independent Disks**. It's a way to combine multiple physical hard drives into a single logical unit to improve performance, increase storage capacity, or provide redundancy (data protection).

**RAID** in Linux (and other operating systems) allows you to combine multiple hard drives to achieve better performance, redundancy, or both. It's like having a team of chefs working together to ensure your pizzas are delivered quickly and reliably, even if one chef makes a mistake.

Raid is used for if one disk die you use another disk 
    
Raid is  configured on physical disk whereas LVM is configured on virtual disk 
    
- Types of RAID 
    

 **RAID0** – you add 2 disk and if data is loss no backup 

**RAID1** – you mirror both disk data and is slow 

**RAID5** – you have 3 or more disk you don’t add you copy everything

![[Pasted image 20250129144117.png]]



**Simple Analogy**

Imagine you have a pizza delivery business. You want to ensure that pizza deliveries are fast, reliable, and can handle large orders without any delays. Here are some ways RAID can help, using a pizza analogy:

###### RAID Levels Explained:

1. **RAID 0 (Striping):**
    
    - **How it works:** You split the ingredients across multiple chefs. Each chef works on a part of the pizza, making the overall process faster.
        
    - **Benefit:** Improved performance (speed).
        
    - **Drawback:** If one chef makes a mistake, the entire pizza is ruined (no redundancy).
        
2. **RAID 1 (Mirroring):**
    
    - **How it works:** You have two chefs making identical pizzas. If one pizza is ruined, you still have the other.
        
    - **Benefit:** Redundancy (data protection).
        
    - **Drawback:** You need twice the ingredients (storage space).
        
3. **RAID 5 (Striping with Parity):**
    
    - **How it works:** You have three or more chefs. Each chef works on a part of the pizza, and one chef keeps track of a backup recipe (parity) for any mistakes.
        
    - **Benefit:** Balance of performance and redundancy.
        
    - **Drawback:** Requires at least three chefs (disks), and rebuilding a ruined pizza takes time.
        
4. **RAID 10 (Combining RAID 1 and RAID 0):**
    
    - **How it works:** You have four chefs. Two chefs make identical pizzas (mirroring), and the other two split the ingredients (striping) to make it faster.
        
    - **Benefit:** High performance and redundancy.
        
    - **Drawback:** Requires at least four chefs (disks).


























