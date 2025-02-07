Network Monitoring & Log Analysis  
Objective: Monitor network traffic and analyze logs for suspicious activity.  
Tasks:

- Use tcpdump to capture 100 packets on interface eth0 and save to capture.pcap

```
sudo tcpdump -i eno1 -c 100 -w capture.pcap
```

to verify
```
tcpdump -r capture.pcap
```



- Install iftop to monitor real-time bandwidth usage.

```
sudo apt install iftop
```



- Write a script (scan-logs.sh) to search /var/log/auth.log for "Failed password" attempts and save results to failed-logins.txt.

```
vim scan-logs.sh
```

add these lines for configuration

logfiles1