
User Management & Security Hardening  
Objective: Secure user accounts and audit system permissions.  
Tasks:

- Create two users: dev1 and dev2 with home directories

```
sudo adduser dev1
```

```
sudo adduser dev2
```

to verify if users are created
```
cat /etc/passwd
```

- Force both users to reset passwords on first login.

```
sudo passwd --expire dev1
```

```
sudo passwd --expire dev2
```


- Create a group developers and add both users to it.

```
sudo addgroup developers
```

```
sudo usermod developers dev1
```

```
sudo usermod developers dev1
```

to verify this
```
cat /etc/group
```


```
sudo find / -perm -4000 -type > suid-report.txt
```