+++
date = '2025-04-12T11:30:14+10:00'
draft = true
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
To start off, I conducted an nmap service scan to find the available services found on the most common TCP ports.

> *nmap -sV target1.ine.local*

![alt](/public/images/Picture1.png)


