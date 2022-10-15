## Brooklyn Nine Nine | TryHackMe

This is the link for the room [Brooklyn Nine Nine](https://tryhackme.com/room/brooklynninenine)

<img src="https://user-images.githubusercontent.com/67650329/195988223-40728ede-cd8d-403a-801c-0aa2d239a6c9.jpeg" width="200px" align="center">

This room is aimed for beginner level hackers but anyone can try to hack this box. There are two main intended ways to root the box.

---
Let's go!

We can enumeration use `nmap`

`nmap -sC -sV -p- -T4 [TARGET_IP]`

- sC = Run the default script.
- sV = Version of services.
- -p- = Checking for all port.
- T4 = Scanning speed.

<img src="https://user-images.githubusercontent.com/67650329/195988298-6b0e1b9c-dd65-4065-9502-9aaab17e1115.png" width="500px" align="center">

Port open:

- 21 = FTP.
- 22 = SSH.
- 80 = HTTP.

FTP port it's open we can open the FTP to search what it's on the FTP.

`ftp [TARGET_IP] [PORT]`

<img src="https://user-images.githubusercontent.com/67650329/195988421-a1b9021f-8c63-42ef-a0c5-b40cf4b46a7f.png" width="500px" align="center">

We got `note_to_jake.txt` on FTP.

`From Amy,

Jake please change your password. It is too weak and holt will be mad if someone hacks into the nine nine`

After open the txt we find the clue `It is too weak`.

We can use hydra to bruteforce the password and use rockyou wordlist.

`hydra -l [USER] -P [WORDLIST] [TARGET_IP] ssh`

- -l = User on the machine.
- -P = Wordlist to use bruteforce.

<img src="https://user-images.githubusercontent.com/67650329/195988642-00794d02-90e6-41a8-acf7-8ac82901ff3e.png" width="500px" align="center">

Take a few minute and we got the password of jake ssh.

<img src="https://user-images.githubusercontent.com/67650329/195988711-7b6f8d74-d126-4881-a922-4a8e6a925ce9.png" width="250px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195988758-662c3949-a1df-4d79-8df9-c3d84b42d9e3.png" width="300px" align="center">

We got the `user.txt on /home/holt`.

<img src="https://user-images.githubusercontent.com/67650329/195988815-aecfffd5-1bc3-4f4c-b402-99706c52d653.png" width="500px" align="center">

We search script on https://gtfobins.github.io

`sudo less /etc/profile`

`!/bin/sh`

<img src="https://user-images.githubusercontent.com/67650329/195988886-58b84728-8b81-4e2b-8264-e4aecbd03895.png" width="300px" align="center">

---
