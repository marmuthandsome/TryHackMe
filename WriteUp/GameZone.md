## Game Zone | TryHackMe

This is the link for the room [Game Zone](https://tryhackme.com/room/gamezone)

<img src="https://tryhackme-images.s3.amazonaws.com/room-icons/f840de8ced2851ef65e39bf9d809751e.jpeg" width="150px" align="center">

---
This room will cover SQLi (exploiting this vulnerability manually and via SQLMap), cracking a users hashed password, using SSH tunnels to reveal a hidden service and using a metasploit payload to gain root privileges. 

Lets do this!

Access the website first.

<img src="https://user-images.githubusercontent.com/67650329/193772171-4ff48976-c2f4-4a2a-84f2-b6c72eeb795b.png" width="350px" align="center">

**What is the name of the large cartoon avatar holding a sniper on the forum?**

**Answer: Agent 47**

You can test the sql injection on login bar.

`' or 1=1 -- -`

<img src="https://user-images.githubusercontent.com/67650329/193772613-7cd528ac-0dc3-4181-a846-1b6e2e9f3653.png" width="350px" align="center">

And the website bring you to the another page.

<img src="https://user-images.githubusercontent.com/67650329/193772909-e4c82163-6c55-410c-ac0f-136dd52d88c3.png" width="450px" align="center">

**When you've logged in, what page do you get redirected to?**

**Answer: portal.php**

We're going to use SQLMap to dump the entire database for GameZone.

Using the page we logged into earlier, we're going point SQLMap to the game review search feature.

First we need to intercept a request made to the search feature using `BurpSuite`.

<img src="https://user-images.githubusercontent.com/67650329/193774256-04fca068-ec79-4925-a456-66dfba4e58c2.png" width="450px" align="center">

Save this request into a text file. We can then pass this into SQLMap to use our authenticated user session.

<img src="https://user-images.githubusercontent.com/67650329/193774689-c2d679bd-2e07-49b7-82ce-a4287d522c9b.png" width="450px" align="center">

`sqlmap -r {file_name} --dbms=mysql --dump`

-r = uses the intercepted request you saved earlier.

--dbms = tells SQLMap what type of database management system it is.

--dump = attempts to outputs the entire database.

SQLMap will now try different methods and identify the one thats vulnerable. Eventually, it will output the database.

<img src="https://user-images.githubusercontent.com/67650329/193774925-156fabc3-de04-472b-af10-0b0da7276ff8.png" width="450px" align="center">

**What was the username associated with the hashed password?**

**Answer: agent47**

<img src="https://user-images.githubusercontent.com/67650329/193775509-687fe690-7b59-4ec0-a4e4-dad4498d8267.png" width="500px" align="center">

Now we cracking the password hash using `JohnTheRipper`.

`john hash.txt --wordlist=rockyou.txt --format=raw-SHA256`

hash.txt = contains a list of your hashes (in your case its just 1 hash).

--wordlist = is the wordlist you're using to find the dehashed value.

--format = is the hashing algorithm used. In our case its hashed using SHA256.

<img src="https://user-images.githubusercontent.com/67650329/193775742-1a401043-e780-4d4e-bf0c-38e3a613892d.png" width="500px" align="center">

Now you have a password and username. Try SSH'ing onto the machine.

<img src="https://user-images.githubusercontent.com/67650329/193777587-0874a9fd-6476-47ff-9712-5d9f0ff29dff.png" width="500px" align="center">

We will use a tool called ss to investigate sockets running on a host.

If we run `ss -tulpn` it will tell us what socket connections are running

-t	= Display TCP sockets

-u	= Display UDP sockets

-l	= Displays only listening sockets

-p	= Shows the process using the socket

-n	= Doesn't resolve service names

<img src="https://user-images.githubusercontent.com/67650329/193777950-18e0d481-771a-4dc6-9361-f0288c1b8de6.png" width="500px" align="center">

**How many TCP sockets are running?**

**Answer: 5**

We can see that a service running on port 10000 is blocked via a firewall rule from the outside (we can see this from the IPtable list). However, Using an SSH Tunnel we can expose the port to us (locally)!

From our local machine, `run ssh -L 10000:localhost:10000 <username>@<ip>`

<img src="https://user-images.githubusercontent.com/67650329/193778189-3214e218-36f5-4a52-8d67-5b551738e93e.png" width="500px" align="center">

Once complete, in your browser type "localhost:10000" and you can access the newly-exposed webserver.

<img src="https://user-images.githubusercontent.com/67650329/193778378-828c01b7-95ce-4e5f-932e-031aea0d3977.png" width="400px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193778474-cbc954cd-4787-46ec-9253-87a13baa0801.png" width="400px" align="center">

**What is the name of the exposed CMS?**

**Answer: Webmin**

**What is the CMS version?**

**Answer: 1.580**

We got the CMS version we can search the vulnerability.

Using the CMS dashboard version, use Metasploit to find a payload to execute against the machine.

<img src="https://user-images.githubusercontent.com/67650329/193779039-96f8bf2c-a289-46d2-abcf-d7ae2338b019.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193779174-1332216a-28b8-4391-85ae-1a7deef6c574.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193779311-dc61d7a5-abc1-4a26-8099-ac14f42227d1.png" width="500px" align="center">

<img src="https://user-images.githubusercontent.com/67650329/193779402-8170da58-e2ca-48ef-a339-8dca3c0c355f.png" width="500px" align="center">

---
