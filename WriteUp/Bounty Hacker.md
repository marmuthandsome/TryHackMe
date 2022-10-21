## Bounty Hacker | TryHackMe

This is the link for the room [Bounty Hacker](https://tryhackme.com/room/cowboyhacker)

<img src="https://user-images.githubusercontent.com/67650329/197123226-d78798c1-d4e0-41bb-a86c-c11f107fa318.jpeg" width="250px" align="center">

---
You talked a big game about being the most elite hacker in the solar system. Prove it and claim your right to the status of Elite Bounty Hacker!

Let's go!

`nmap -sC -sV -p- -T4 {IP}`

- -sC = Run the default script.

- -sV = Version of services.

- -p- = Checking for all port.

- -T4 = Scanning speed.

This is the result for the scanning with nmap tools.

<img src="https://user-images.githubusercontent.com/67650329/197123353-92419044-e220-4dc2-a0b6-4b5f47ef748d.png" width="500px" align="center">

Port open:

- 21 = FTP.
- 22 = SSH.
- 80 = HTTP.

FTP port it's open we can open the FTP to search what it's on the FTP.

`ftp [TARGET_IP]`

<img src="https://user-images.githubusercontent.com/67650329/197123723-aad4edee-7e57-4a33-8050-53f906838cca.png" width="500px" align="center">

We got `locks.txt` and `taks.txt` on FTP.

Download it and Open the files.

<img src="https://user-images.githubusercontent.com/67650329/197123856-a7be43e6-25f7-4ed5-ae71-5569cfb1ceab.png" width="250px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/197123887-237ce0b1-fc4a-4790-93d3-01de90367e54.png" width="200px" align="center">

We got the lin username. We can use it bruteforce to find the password of user lin.

`hydra -l [USER] -P [WORDLIST] [TARGET_IP] ssh`

- -l = Username user to bruteforce.
- -P = Wordlist to bruteforce.

<img src="https://user-images.githubusercontent.com/67650329/197124351-ff20ae7f-09d2-4516-a192-41fbab10fc62.png" width="500px" align="center">

After we got the user lin password.

We can use to login the ssh.

<img src="https://user-images.githubusercontent.com/67650329/197124666-d6f51ef1-5837-4523-8f53-4f4ca362d0a5.png" width="250px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/197124753-e51abf08-03f6-4391-bb03-851819861e27.png" width="600px" align="center">

[gtfobins.github.io](https://gtfobins.github.io/)

<img src="https://user-images.githubusercontent.com/67650329/197124893-5815b2e3-b636-45b8-8b72-14b430809e66.png" width="600px" align="center">

---
