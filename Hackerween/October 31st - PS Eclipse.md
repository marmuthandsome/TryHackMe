## PS Eclipse | TryHackMe

This is the link for the room [PS Eclipse](https://tryhackme.com/room/posheclipse)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/0a0c0c0df8c70f64451e32a563216f39.png" width="150px" align="center">

**Medium, Blue Team**

Scenario: You are a SOC Analyst for an MSSP (Managed Security Service Provider) company called TryNotHackMe.

A customer sent an email asking for an analyst to investigate the events that occurred on Keegan's machine on Monday, May 16th, 2022. The client noted that the machine is operational, but some files have a weird file extension. The client is worried that there was a ransomware attempt on Keegan's device. 

Your manager has tasked you to check the events in Splunk to determine what occurred in Keegan's device. 

Happy Hunting!

---

**Tools**

- Splunk
- [Virus Total](https://www.virustotal.com/gui/home/search)
- [Cyberchef](https://icyberchef.com/)

**1. A suspicious binary was downloaded to the endpoint. What was the name of the binary?**

Answer: OUTSTANDING_GUTTER.exe

<img src="https://user-images.githubusercontent.com/67650329/200800716-ff63effe-9d59-418a-a044-8f0b4b407796.png" width="600px" align="center">

**2. What is the address the binary was downloaded from? Add http:// to your answer & defang the URL.**

Answer: hxxp[://]886e-181-215-214-32[.]ngrok[.]io

<img src="https://user-images.githubusercontent.com/67650329/200832991-0a140ff3-b2ca-4ea6-ba69-2b25d04e5f6e.png" width="600px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/200833192-1a0c91f1-c790-4e56-b5f0-378a2f1ad9db.png" width="500px" align="center">

**3. What Windows executable was used to download the suspicious binary? Enter full path.**

Answer: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

<img src="https://user-images.githubusercontent.com/67650329/200833815-e9f5d809-7030-4096-862a-dd58cb624730.png" width="600px" align="center">

**4. What command was executed to configure the suspicious binary to run with elevated privileges?**

Answer: "C:\Windows\system32\schtasks.exe" /Create /TN OUTSTANDING_GUTTER.exe /TR C:\Windows\Temp\COUTSTANDING_GUTTER.exe /SC ONEVENT /EC Application /MO *[System/EventID=777] /RU SYSTEM /f

<img src="https://user-images.githubusercontent.com/67650329/200834220-0493dc59-1d4a-4ad8-95d0-957b86568e29.png" width="600px" align="center">

**5. What permissions will the suspicious binary run as? What was the command to run the binary with elevated privileges? (Format: User + ; + CommandLine)**

Answer: NT AUTHORITY\SYSTEM;"C:\Windows\system32\schtasks.exe" /Run /TN OUTSTANDING_GUTTER.exe

<img src="https://user-images.githubusercontent.com/67650329/200835932-23f575a7-c31e-443d-9a5b-7c4f85c9c034.png" width="600px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/200836053-15b34bdb-690e-436f-a5fd-b77e768e19b2.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/200837144-3ddaa6b9-c2e4-42fa-b319-ced32fb19894.png" width="600px" align="center">

**6. The suspicious binary connected to a remote server. What address did it connect to? Add http:// to your answer & defang the URL.**

Answer: hxxp[://]9030-181-215-214-32[.]ngrok[.]io

<img src="https://user-images.githubusercontent.com/67650329/200837984-47a48c7a-2da4-4c0c-a165-45f5d2253c61.png" width="600px" align="center">

**7. A PowerShell script was downloaded to the same location as the suspicious binary. What was the name of the file?**

Answer: script.ps1

<img src="https://user-images.githubusercontent.com/67650329/200838326-ec99705a-885d-428b-ba54-973ded877583.png" width="400px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/200838569-80d9d666-894a-470e-a51a-20cac5815c9e.png" width="600px" align="center">

**8. The malicious script was flagged as malicious. What do you think was the actual name of the malicious script?**

Answer: BlackSun.ps1

<img src="https://user-images.githubusercontent.com/67650329/200839113-30e08463-f17c-433d-8777-9ff0986e4691.png" width="600px" align="center">

**9. A ransomware note was saved to disk, which can serve as an IOC. What is the full path to which the ransom note was saved?**

Answer: C:\Users\keegan\Downloads\vasg6b0wmw029hd\BlackSun_README.txt

<img src="https://user-images.githubusercontent.com/67650329/200839661-1c4f5c99-6354-4a6e-aa9a-06661837d74b.png" width="600px" align="center">

**10. The script saved an image file to disk to replace the user's desktop wallpaper, which can also serve as an IOC. What is the full path of the image?**

Answer: C:\Users\Public\Pictures\blacksun.jpg

<img src="https://user-images.githubusercontent.com/67650329/200839898-c1ef82dd-3e7b-4fb8-99d5-b14f5a93f56b.png" width="600px" align="center">

---
