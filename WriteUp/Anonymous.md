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
ftp Anonymous FTP login allowed. So we can use the smbclient with anonymous user.

Use smbclient command:
`


└─$ smbclient -L 10.10.212.113
Password for [WORKGROUP\kali]:

    	Sharename   	Type  	Comment
    	---------   	----  	-------
    	print$      	Disk  	Printer Drivers
    	pics        	Disk  	My SMB Share Directory for Pics
    	IPC$        	IPC   	IPC Service (anonymous server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

    	Server           	Comment
    	---------        	-------

    	Workgroup        	Master
    	---------        	-------
    	WORKGROUP        	ANONYMOUS
