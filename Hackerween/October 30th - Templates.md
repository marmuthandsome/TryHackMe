## Templates | TryHackMe

This is the link for the room [Templates](https://tryhackme.com/room/templates)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/223d78403d08b0560d6ed7104be6aa5d.png" width="150px" align="center">

**Medium, red team**

Pug is our favourite templating engine! We made this super slick application so you can play around with Pug and see how it works. Seriously, you can do so much with it. Try out the Pug templating engine and inject some code to exploit!

---

**Tools**

- [CyberChef](https://cyberchef.org/)
- [SSTI reverse shell to PUG](https://gist.githubusercontent.com/Jasemalsadi/2862619f21453e0a6ba2462f9613b49f/raw/e52a952130d102ef48b5146779249cceb3b5bf28/ssti_rev_shell_pug_node_js)

First step, We must access the website.

<img src="https://user-images.githubusercontent.com/67650329/200494432-f57c8fef-cf57-4138-acfb-37cdda5a336a.png" width="500px" align="center">

Access this github to see the script of reverse shell [SSTI reverse shell to PUG](https://gist.githubusercontent.com/Jasemalsadi/2862619f21453e0a6ba2462f9613b49f/raw/e52a952130d102ef48b5146779249cceb3b5bf28/ssti_rev_shell_pug_node_js)

Copy the Payloads and Paste it on [CyberChef](https://cyberchef.org/)

And then change the IP Address to your IP Address and Change the port to listen with netcat.

After done change all to can change back to the base64.

And copy paste on the website and run the listener.

<img src="https://user-images.githubusercontent.com/67650329/200496633-ef70170b-b46a-4dd0-96c6-07f58978277c.png" width="500px" align="center">

And you got in to the machine.

<img src="https://user-images.githubusercontent.com/67650329/200497842-df09ca18-fadd-4ab6-9aa5-28b335eb04fb.png" width="500px" align="center">

---
