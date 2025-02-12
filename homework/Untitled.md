Privilege escalation
	potato attak
CVE-2019-1388
Escalation path DLL Hijacking
LDAP and difference between active directory idm winbind openldap etc
DHCP  
DNS


- Fat NTFS ReFS (data limits)

| File System | Maximum Volume Size | Maximum File Size |
| ----------- | ------------------- | ----------------- |
| FAT32       | 2 TB                | 4 GB              |
| NTFS        | 16 exabytes (EB)    | 16 exabytes (EB)  |
| ReFS        | 1 Yottabyte (YB)    | 16 Exabytes (16)  |
**FAT32:** Suitable for smaller volumes and files, but limited to 4 GB per file
**NTFS:** Ideal for most users with large volume and file size support
**ReFS:** Designed for high resiliency and large-scale data storage, supporting even larger volumes and files


- Syslogs in windows
- Event Viewers (logs), Event IDs
- sysmon
- registry

- **Hypervisor** and its types
A **hypervisor** is software that allows multiple virtual machines (VMs) to run on a single physical computer. Think of it as a manager that divides and allocates resources (like CPU, memory, and storage) to each VM so they can operate independently, as if they were separate computers.

### Types of Hypervisors:

1. **Type 1 Hypervisor (Bare-Metal):**
    
    - Runs directly on the physical hardware.
        
    - Provides better performance and efficiency.
        
    - Examples: VMware ESXi, Microsoft Hyper-V, Xen.
        
2. **Type 2 Hypervisor (Hosted):**
    
    - Runs on top of an existing operating system.
        
    - Easier to set up but less efficient than Type 1.
        
    - Examples: VMware Workstation, Oracle VM VirtualBox, Parallels Desktop.
