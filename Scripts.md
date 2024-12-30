Normalizing a shell
	`python3 -c 'import pty;pty.spawn("/bin/bash")'`
	`export TERM=xterm`
	`CTRL + Z`
	`stty raw -echo && fg`

RDP with xfreerdp
	`xfreerdp /u:[USERNAME] /p:[PASSWORD] /v:[IP_ADDRESS]`
