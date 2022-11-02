## Epoch | TryHackMe

This is the link for the room [Epoch](https://tryhackme.com/room/epoch)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/1f93210b470f836c38121fc3f65c0807.png" width="150px" align="center">

**Red Team Lab**

Be honest, you have always wanted an online tool that could help you convert UNIX dates and timestamps… and this new online date converter tool is totally secure...right?! In this challenge, you must figure out how the web application works, convert UNIX dates, and exploit the web application to find the flags!

---

This it's page for this machine.

<img src="https://user-images.githubusercontent.com/67650329/199459196-54186917-773b-4e17-95eb-4e808f208b26.png" width="500px" align="center">

We can test with [epochconverter](https://www.epochconverter.com/)

And it's the result for the epoch test.

<img src="https://user-images.githubusercontent.com/67650329/199459592-0c3f9a28-3ea5-4cd7-bd22-5bf53cba5950.png" width="500px" align="center">

So... We can see the hint for search the flag.

Hint: The developer likes to store data in `environment variables`, can you find anything of interest there?.

We can use the command `;printenv`.

Why printenv: The printenv command in Linux provides you with the ability to view all or a part of the environment.

<img src="https://user-images.githubusercontent.com/67650329/199459872-bd6443f7-56c8-452f-a2c2-57646204a92e.png" width="500px" align="center">

Thank you for reading 👋👋👋

---
