+++
date = '2025-03-02T13:23:55+11:00'
draft = false
title = 'Specialer PicoCTF'
+++
# Specialer

Medium | General Skills | picoCTF 2023 | bash | ssh

## Author: LT 'syreal' Jones, et al.

Reception of Special has been cool to say the least. That's why we made an
exclusive version of Special, called Secure Comprehensive Interface for
Affecting Linux Empirically Rad, or just 'Specialer'. With Specialer, we really
tried to remove the distractions from using a shell. Yes, we took out spell
checker because of everybody's complaining. But we think you will be excited
about our new, reduced feature set for keeping you focused on what needs it the
most.  Please start an instance to test your very own copy of Specialer.
`ssh -p 51238 ctf-player@saturn.picoctf.net`. The password is
`af86add3`

## Solution

After connecting via SSH to this challenge, we are presented with a command line.

My first thought was to gain an idea of the environment through the files and folders available. 

> *ls*

This returned the error *-bash: ls: command not found*

This prompted me to try figure out what commands were available.

> *help*

I was now presented with a list of available commands that were applicable for this environment.

Going through these, “cd” immediately appeared as a viable option to explore the files available to me. 

As well as “cd”, using “pwd” allowed me to see the current directory.

> */home/ctf-player*

I proceeded to check out the surrounding files using *cd* and tab.

Now I could see:

> *.hushlogin .profile abra/ ala/ sim/*

I decided to check out the first directory - *abra/*

In here, I found a text file *cadabra.txt.*

Now it was time to figure out how to read the contents of this file.

Without the option to use *cat*, I had to turn to revisit the *help* page.

Here I found the *echo* command. This led me to using the command:

> *echo $(<cadabra.txt)*

This allowed me to read the contents of this file:

> *Nothing up my sleeve!*

Now that I had a way to read the contents of the available files, I thought I’d get a good idea of what was in the files that were easily found.

Next I tried the following directory, named *ala/*, alluding to another “magic word”.

In this directory I found:

> *kazam.txt mode.txt*

Using the same command as earlier to read the contents of *kazam.txt*, I was surprised to find the flag!

> *return 0 picoCTF{y0u_d0n7_…}*

I redacted the rest of the flag in an effort to allow others to find this “magic” for themselves.

## Conclusion

Overall, this challenge felt like a straightforward task with the opportunity to find a workaround for missing commands, namely *ls* and *cat*. Definitely a fun task to work on finding other ways to carry out otherwise regular operations from the CLI.
