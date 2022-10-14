## Wgel CTF | TryHackMe

This is the link for the room [Wgel CTF](https://tryhackme.com/room/wgelctf)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/8116d1d52d3a63dd1e7c2e7ddce8a0d5.png" width="200px" align="center">

---
Let's go!

Can you exfiltrate the root flag?

Access the website first. for this website it's Apache default page.

<img src="https://user-images.githubusercontent.com/67650329/195776828-54c2c39a-d9a7-4de8-b232-9fd0567f0c3d.png" width="500px" align="center">

We can try to search anything important on source page.

<img src="https://user-images.githubusercontent.com/67650329/195776922-f00e38eb-0f3f-4204-a300-543245f1cb9e.png" width="500px" align="center">

I think jessie it's the name we can use on ssh.

We can enumeration use `nmap`

`nmap -sC -sV -p- -T4 [TARGET_IP]`

- sC = Run the default script.
- sV = Version of services.
- -p- = Checking for all port.
- T4 = Scanning speed.

<img src="https://user-images.githubusercontent.com/67650329/195777150-624793a7-ada2-4cbc-947d-a37bd06fd6f9.png" width="500px" align="center">

Port open:

- 22 = SSH.
- 80 = HTTP.

We can use `gobuster` for search the subdomain.

`gobuster dir -u [TARGET_IP] -w [WORDLIST] -f -n`

- u = Url/Link Target.
- w = Wordlist to use.
- f = Nospam.
- n = No Status just result (Nospam).

<img src="https://user-images.githubusercontent.com/67650329/195777395-8b0ec685-5882-4ed3-a3dd-9fdb50bb8a7e.png" width="500px" align="center">

We Found the subdomain:

- /sitemap/
- /icons/

We can acces the `/sitemap/`.

<img src="https://user-images.githubusercontent.com/67650329/195777495-8bf6d85b-9819-4caa-bbae-478ac7c54515.png" width="500px" align="center">

We can search another page on /sitemap/ use gobuster.

<img src="https://user-images.githubusercontent.com/67650329/195777642-b1534b53-78b8-477a-b9a7-71623d59bb1a.png" width="500px" align="center">

We found the `./ssh` page on /sitemap/.

<img src="https://user-images.githubusercontent.com/67650329/195778051-03d1f61a-3fb9-490f-b6a5-d9a1770067b0.png" width="500px" align="center">

Now, we can login into jessie ssh.

`ssh [NAME]@[IP] -i [FILE_RSA]`

- i = To access the file rsa.

<img src="https://user-images.githubusercontent.com/67650329/195778818-12d0f6f3-9b4c-423c-aa2a-08616d9a97f6.png" width="500px" align="center">

We go `user.txt` on /home/jessie/Documents/.

<img src="https://user-images.githubusercontent.com/67650329/195779030-0233ea1b-1115-4793-b068-e60b5e2fba14.png" width="300px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195779172-81ced876-673f-47d1-8478-25ba6d6abdcd.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195779316-53d20c11-09c9-4058-aaa7-dc1f47c8c8a7.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195779797-32812eea-210e-4cc5-8eff-70637ee56af9.png" width="300px" align="center">

---
