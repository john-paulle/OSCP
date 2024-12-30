Passive Information Gathering
- whois
- google site:xxx filetype:xxx
- netcraft.com
- github
- shodan.io
- securityheaders.com
Active Information Gathering
- DNS enum
	- `host -t [ns, a, aaaa, mx, ptr, cname, txt] megacorpone.com`
- nmap
	- -sT - TCP connect scan
	- -sS - TCP SYN scan
	- -sU - UDP scan
	- -sn - network sweep
	- -A - version detection, script scanning, and traceroute
	- -O - OS fingerprinting
	- --script
		- http-headers
- SMB enum
	- `nmap -v -p 139,445 -oG smb.txt 192.168.50.1-254`
	- `sudo nbtscan -r 192.168.50.0/24`
	- `net view \\dc01 /all`
- SMTP enum
	- `nc -nv 192.168.50.8 25`
	- `Test-NetConnection -Port 25 192.168.50.8`
	- `python3 smtp.py root 192.168.50.8` (see smtp.py below)
	- `#!/usr/bin/python` 
		`import socket`
		`import sys`
		
		`if len(sys.argv) != 3:`
		        `print("Usage: vrfy.py <username> <target_ip>")`
		        `sys.exit(0)`
		
		`# Create a Socket`
		`s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)`
		
		`# Connect to the Server`
		`ip = sys.argv[2]`
		`connect = s.connect((ip,25))`
		
		`# Receive the banner`
		`banner = s.recv(1024)`
		
		`print(banner)`
		
		`# VRFY a user`
		`user = (sys.argv[1]).encode()`
		`s.send(b'VRFY ' + user + b'\r\n')`
		`result = s.recv(1024)`
		
		`print(result)`
		
		`# Close the socket`
		`s.close()`
		
		


- SNMP enum
  
  
SNMP MIB Values

| 1.3.6.1.2.1.25.1.6.0   | System Processes |
| ---------------------- | ---------------- |
| 1.3.6.1.2.1.25.4.2.1.2 | Running Programs |
| 1.3.6.1.2.1.25.4.2.1.4 | Processes Path   |
| 1.3.6.1.2.1.25.2.3.1.4 | Storage Units    |
| 1.3.6.1.2.1.25.6.3.1.2 | Software Name    |
| 1.3.6.1.4.1.77.1.2.25  | User Accounts    |
| 1.3.6.1.2.1.6.13.1.3   | TCP Local Ports  |

  
	echo public > community
	echo private >> community
	echo manager >> community
	for ip in $(seq 1 254); do echo 192.168.50.$ip; done > ips
	onesixtyone -c community -i ips
	
	snmpwalk -c public -v1 -t 10 192.168.50.151
	snmpwalk -c public -v1 192.168.50.151 1.3.6.1.4.1.77.1.2.25
