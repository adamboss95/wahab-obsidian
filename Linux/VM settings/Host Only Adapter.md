We can create a Host-Only Adapter using the command line interface (CLI).

### Step-by-Step Guide:

1. **Open Command Prompt/Terminal:** On your host machine (the one running VirtualBox), open a Command Prompt or Terminal.
    
2. **Create a Host-Only Network:** Use the following command to create a new Host-Only Adapter:
    
    bash
```
VBoxManage hostonlyif create
```
This command should output something like "Interface 'vboxnet0' was successfully created".
    
3.  **Configure the Host-Only Network:** Set the IP address for the Host-Only Adapter:
```
VBoxManage hostonlyif ipconfig vboxnet0 --ip 192.168.56.150 --netmask 255.255.255.0
```

4. **Assign the Host-Only Adapter to VMs:** Go to VirtualBox, and for each VM:

- Open the settings of the VM.
    
- Go to the `Network` tab.
    
- Enable Adapter 2 and set it to "Host-Only Adapter".
    
- Choose the newly created adapter (e.g., `vboxnet0`).

### Step 2: Configure IP Addresses on VMs

1. **Edit Network Configuration Files:**
```
sudo vim /etc/NetworkManager/system-connections/enp0s8.nmconnection
```

Add the command to create ip for enp0s8 (for VM1):
```
sudo nmcli con add type ethernet ifname enp0s8 con-name enp0s8 ipv4.method manual ipv4.addresses 192.168.56.101/24 ipv4.gateway 192.168.56.1 ipv6.method ignore
```



Add the following (for VM2):
```
sudo nmcli con add type ethernet ifname enp0s8 con-name enp0s8 ipv4.method manual ipv4.addresses 192.168.56.102/24 ipv4.gateway 192.168.56.1 ipv6.method ignore
```


- sudo systemctl restart NetworkManager

- sudo nmcli con up enp0s8
- it should connect to each other if you ping 192.168.56.102 from the machine having 192.168.56.101 or vice versa



 issue ; where the root password was not working for   
```  
ssh localhost   
```  
to fix this issue :   
Ensure that public key is correctly added :

```  
sudo chmod 700 ~/.ssh  
sudo chmod 600 ~/.ssh/authorized_keys  
```  
if the 2nd command does not run, make a new file as :   
```  
touch ~/.ssh/authorized_keys  
```  
and give these permissions :   
```  
chmod 600 ~/.ssh/authorized_keys  
```  
edit this file using nano :

```  
sudo nano /etc/ssh/sshd_config  
```

  uncomment the following lines and set them as :   
```  
PermitRootLogin yes  
PubkeyAuthentication yes  
PasswordAuthentication yes  
```  
Save the nano file with Ctrl O and quit by Ctrl x

Restart the ssh service :  
```  
sudo systemctl restart sshd  
```  
for a detailed output :   
```  
ssh -v localhost  
```