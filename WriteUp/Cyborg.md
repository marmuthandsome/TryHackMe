## Cyborg CTF | TryHackMe

This is the link for the room [Cyborg](https://tryhackme.com/room/cyborgt8)

<img src="https://user-images.githubusercontent.com/67650329/195512816-9ac77bb0-3c7d-4c3e-8665-8a3434876933.jpeg" width="200px" align="center">

---
Let's go!

A box involving encrypted archives, source code analysis and more.

Access the website first. for this website it's Apache default page.

<img src="https://user-images.githubusercontent.com/67650329/195513132-1c066956-e1a9-4781-ad0f-287ad8b7601b.png" width="500px" align="center">

We can enumeration use `nmap`

`nmap -sC -sV -p- -T4 [TARGET_IP]`

- sC = Run the default script.
- sV = Version of services.
- -p- = Checking for all port.
- T4 = Scanning speed.

<img src="https://user-images.githubusercontent.com/67650329/195513422-057e5fae-5fde-4899-ab3c-69545d5b4bdc.png" width="500px" align="center">

Port open:

- 22 = SSH.
- 80 = HTTP.

We can use `gobuster` for search the subdomain.

`gobuster dir -u [TARGET_IP] -w [WORDLIST] -f -n`

- u = Url/Link Target.
- w = Wordlist to use.
- f = Nospam.
- n = No Status just result (Nospam).

<img src="https://user-images.githubusercontent.com/67650329/195513931-2a2b367a-6888-4cd0-b4ae-5ed3a9e6a1b1.png" width="500px" align="center">

We Found the subdomain:

- /icons/
- /admin/
- /etc/

This is `/admin/` page.

<img src="https://user-images.githubusercontent.com/67650329/195514204-ddfdea54-a850-449d-8fa6-b37292d8fc8e.png" width="500px" align="center">

We can download the file `archive.tar` on /admin/ page.

<img src="https://user-images.githubusercontent.com/67650329/195514332-43928544-a275-430f-b087-e56e2c1789c4.png" width="500px" align="center">

I found another page on `/etc/squid/passwd`

<img src="https://user-images.githubusercontent.com/67650329/195514435-4fdd1dd0-f577-4cae-95f0-aed7908023fe.png" width="500px" align="center">

Now we must cracked the hash. Use `hashcat` tools.

`hashcat -m [NUMBER_HASH] [HASH_FILE] [WORDLIST]`

- m = Use hashcat --help to know the number of hash.

<img src="https://user-images.githubusercontent.com/67650329/195514932-41ea0343-9660-46b3-b4b7-e063eb59d4fc.png" width="300px" align="center">

On the read me file. You can see on Downloaded file before.

<img src="https://user-images.githubusercontent.com/67650329/195515197-70071bf8-4537-4d17-840d-60be4e947f33.png" width="300px" align="center">

Use `borg` tools to get into the machine target. [borg installer](https://linoxide.com/borg-backup-linux-tool/)

`borg list [DIRECTORY]`

- list = To search hidden file on target directory.

`borg extract [DIRECTORY]`

And you can insert the password of hash.

<img src="https://user-images.githubusercontent.com/67650329/195516598-098931fe-312e-4a21-95bd-71b12185e1a5.png" width="500px" align="center">

And back to the downloaded directory you can find another directory `alex`

<img src="https://user-images.githubusercontent.com/67650329/195517133-4bac9ce9-cd2f-4960-bf0c-7687a3d6c17f.png" width="300px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195517253-18eb549b-7b53-4197-b15b-71c3f8db4546.png" width="500px" align="center">

Use ssh to get into the machine target.

<img src="https://user-images.githubusercontent.com/67650329/195517582-127722a1-378a-4ba7-8150-dfdc7928b948.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195517646-14a40997-efe3-423b-8024-acd326843868.png" width="500px" align="center">

We found the credential on `/etc/mp3backups/backup.sh`

<img src="https://user-images.githubusercontent.com/67650329/195517764-883cf1a6-a8a1-4869-8dbe-bb93408e2621.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/195518047-22262316-865f-4b87-ba73-36bb15904d14.png" width="500px" align="center">

---
