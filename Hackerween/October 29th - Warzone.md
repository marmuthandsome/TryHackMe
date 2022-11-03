## Warzone | TryHackMe

This is the link for the room [Warzone](https://tryhackme.com/room/warzoneone)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/3d6033aa286ac42fdb793c605ebbf3f0.png" width="150px" align="center">

**Blue Team Lab**

You work as a Tier 1 Security Analyst for a Managed Security Service Provider (MSSP). Today you're tasked with monitoring network alerts. A few minutes into your shift, you get your first network case: Potentially Bad Traffic and Malware Command and Control Activity Detected. Your race against the clock starts. Inspect the PCAP and retrieve the artefacts to confirm this alert is a true positive.

---

Tools:

- Brim.
- Network Miner.
- Wireshark.

**1. What was the alert signature for Malware Command and Control Activity Detected.**

Answer: ET Malware MirrorBlast CnC Activity M3

Put the PCAP into the Brim.

Search on the search bar `Malware Command and Control Activity Detected`.

<img src="https://user-images.githubusercontent.com/67650329/199665386-e683105f-87b6-4656-ab3f-c746faf3d87b.png" width="500px" align="center">

**2. What is the source IP address? Enter your answer in a defanged format?**

Answer: 172[.]16[.]1[.]102

**3. What IP address was the destination IP in the alert? Enter your answer in a defanged format.**

Answer: 169[.]239[.]128[.]11

On the same Log you can see the answer for number 2 and 3.

<img src="https://user-images.githubusercontent.com/67650329/199665543-d48802bc-0f1b-4a4f-aabe-2af91ea0c967.png" width="500px" align="center">

**4. Inspect the IP address in VirsusTotal. Under Relations > Passive DNS Replication, which domain has the most detections? Enter your answer in a defanged format.**

Answer: fidufagios[.]com

<img src="https://user-images.githubusercontent.com/67650329/199666078-911f4422-1202-4dd9-af4a-b942c102b93b.png" width="500px" align="center">

**5. Still in VirusTotal, under Community, what threat group is attributed to this IP address.**

Answer: TA505

**6. What is the malware family.**

Answer: MirrorBlast

<img src="https://user-images.githubusercontent.com/67650329/199666284-e5b320a0-7fe2-424b-bf1a-6403f22f5353.png" width="700px" align="center">

**7. Do a search in VirusTotal for the domain from question 4. What was the majority file type listed under Communicating Files.**

Answer: Windows Installer

<img src="https://user-images.githubusercontent.com/67650329/199667810-ce4335bb-1f5c-4576-9f2c-dc5592bccdae.png" width="700px" align="center">

**8. Inspect the web traffic for the flagged IP address; what is the user-agent in the traffic.**

Answer: REBOL View 2.7.8.3.1

<img src="https://user-images.githubusercontent.com/67650329/199668291-285a4461-a9bb-4e24-82a1-3ea1fb4fecbd.png" width="500px" align="center">

**9. Retrace the attack; there were multiple IP addresses associated with this attack. What were two other IP addresses? Enter the IP addressed defanged and in numerical order. (format: IPADDR,IPADDR).**

Answer: 185[.]10[.]68[.]235,192[.]36[.]27[.]92

<img src="https://user-images.githubusercontent.com/67650329/199669252-9c1f1320-62da-4aed-a67e-efc15596e79f.png" width="500px" align="center">

**10. What were the file names of the downloaded files? Enter the answer in the order to the IP addresses from the previous question. (format: file.xyz,file.xyz).**

Answer: filter.msi,10opd3r_load.msi

<img src="https://user-images.githubusercontent.com/67650329/199669496-5b292639-8323-44c0-9c24-ef6d6d5ad585.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/199669594-fdade3f5-ca55-447f-8761-182514ffdd3a.png" width="500px" align="center">

**11. Inspect the traffic for the first downloaded file from the previous question. Two files will be saved to the same directory. What is the full file path of the directory and the name of the two files? (format: C:\path\file.xyz,C:\path\file.xyz).**

Answer: C:\ProgramData\001\arab.bin,C:\ProgramData\001\arab.exe

We can search on the Wireshark

<img src="https://user-images.githubusercontent.com/67650329/199670079-dfa309c6-8603-410f-b008-477303dedff6.png" width="700px" align="center">

**12. Now do the same and inspect the traffic from the second downloaded file. Two files will be saved to the same directory. What is the full file path of the directory and the name of the two files? (format: C:\path\file.xyz,C:\path\file.xyz).**

Answer: C:\ProgramData\Local\Google\rebol-view-278-3-1.exe,C:\ProgramData\Local\Google\exemple.rb

<img src="https://user-images.githubusercontent.com/67650329/199670677-1eb1b8da-1205-42f7-8ec6-309b010926b1.png" width="700px" align="center">

---
