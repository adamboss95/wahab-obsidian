





- To change date
	- sudo date --set="YYYY-MM-DD HH:MM:SS"
- uptime = for system uptime
- cal YYYY = list the whole year calendar
- uname -a
- df -h > systemdiskinfo
- vim systemdiskinfo , press dd on the first 2 lines, press esc then :wq! to save and quit
- to run dmesg needs root access
	- sudo dmesg 
	- sudo dmesg > dm-file
- vim dm-file , press G to go to the end of the file, remove last 5-7 lines by pressing dd on those lines
- add text at the end by pressing G in the vim editor, enter the text, press esc, :wq!
- init 6 = reboot system