## PrintNightmare, again! | TryHackMe

This is the link for the room [PrintNightmare, again!](https://tryhackme.com/room/printnightmarec2bn7l)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/80976dc5f46f5d2f78a99c2c8e2bc4a9.png" width="150px" align="center">

**Blue Team Lab**

In the weekly internal security meeting, it was reported that an employee overheard two co-workers discussing the PrintNightmare exploit, and how they can use the exploits to elevate their privileges on their local computers. Inspect the artefacts on the endpoint to detect the exploit they used!

---

**Tools**

- ProcDOT
- FullEventLogView

**Note: Use the `FullEventLogView tool`. Go to `Options > Advanced Options` and `set Show events from all times`**

**1. The user downloaded a zip file. What was the zip file saved as?** 

Hint: You can try using ProcDOT or FullEventLogView.

Answer: levelup.zip

<img src="https://user-images.githubusercontent.com/67650329/199449689-85b2e587-6c74-4789-9e5b-58955b8a1f64.png" width="500px" align="center">

**2. What is the full path to the exploit the user executed?** 

Answer: C:\Users\bmurphy\Downloads\CVE-2021-1675-main\CVE-2021-1675.ps1

<img src="https://user-images.githubusercontent.com/67650329/199450457-0fb616c8-6b62-48df-b263-856448c439e9.png" width="500px" align="center">

**3. What was the temp location the malicious DLL was saved to?** 

Answer: C:\Users\bmurphy\AppData\Local\Temp\3\nightmare.dll

<img src="https://user-images.githubusercontent.com/67650329/199450901-b0e5164a-61be-4855-b57d-389898367ae0.png" width="500px" align="center">

**4. What was the full location the DLL loads from?** 

Answer: C:\Windows\system32\spool\DRIVERS\x64\3\nightmare.dll

<img src="https://user-images.githubusercontent.com/67650329/199451758-430e4d6d-ab51-4360-8e1c-badcc3fba305.png" width="500px" align="center">

**5. What is the primary registry path associated with this attack?** 

Answer: HKLM\System\CurrentControlSet\Control\Print\Environments\Windows x64\Drivers\Version-3\THMPrinter\

**6. What was the PID for the process that would have been blocked from loading a non-Microsoft-signed binary?**

Answer: 2600

<img src="https://user-images.githubusercontent.com/67650329/199452335-ba076db7-6921-46b9-b721-3cf881f9eb25.png" width="650px" align="center">

**7. What is the username of the newly created local administrator account?**

Answer: backup

<img src="https://user-images.githubusercontent.com/67650329/199452846-cf979e81-dd98-43a7-baa7-c4034274d7b4.png" width="500px" align="center">

**8. What is the password for this user?**

Answer: ucGGDMyFHkqMRWwHtQ

Step:

- [Powershell History File](https://0xdf.gitlab.io/2018/11/08/powershell-history-file.html).
- First, Open the powershell and Write the command `Set-PSReadlineOption`.
- After you run the command, Run another command `Get-PSReadlineOption`.
- And you can see `HistorySaveFile`.

<img src="https://user-images.githubusercontent.com/67650329/199454205-41006d77-6e86-4010-8029-40b74484aabe.png" width="750px" align="center">

- Change the directory to `C:\Users\bmurphy\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine`.
- And you can see the `ConsoleHost_history.txt` and Open it.

**9. What two commands did the user execute to cover their tracks? (no space after the comma)**

Answer: rmdir .\CVE-2021-1675-main\, del .\levelup.zip

<img src="https://user-images.githubusercontent.com/67650329/199455299-b9cb2d9b-bacb-4237-bd83-b49eb66bedc2.png" width="550px" align="center">

---
