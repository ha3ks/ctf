# HackTheBox - Blue Walkthrough
-------------------

<p align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/room-icons/7717bbc69c486931e503a74f3192a4d8.gif" style="height: 300px; width:300px;"/>
</p>


The following are the answers and rough guide to the Blue Box.

```bash 
export IP=10.10.156.177
```

## Task 1 - Recon

> How many ports are open with a port number under 1000?

```
3
```

--- Usual nmap run.

> What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)

```
ms17-010
```

--- Ran another nmap scan to look for vulns: *nmap -sS -sV --script=vuln 10.10.156.177 -oN nmap_vuln_scan.txt*


## Task 2 - Gain Access

> Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)


```
exploit/windows/smb/ms17_010_eternalblue
```

--- Search in Metasploit to the rescue.

> Show options and set the one required value. What is the name of this value? (All caps for submission)


```
RHOSTS
```

--- show options when using the exploit.


## Task 3 - Escalate

> If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use?

```
/post/multi/manage/shell_to_meterpreter
```

--- Search to the rescue again here.

> Select this (use MODULE_PATH). Show options, what option are we required to change?

```
session
```

--- Needed to set session to session 1 what we had backgrounded.


## Task 4 - Cracking

> Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 

```
Jon
```

--- Got the name in the inital nmap scan Jon-PC *wink*

> Copy this password hash to a file and research how to crack it. What is the cracked password?

```
alqfna22
```

--- Cracked skulls, I mean hashes via hashcat after hashdumping in windows.


## Task 5 - Find flags!

> Flag1? This flag can be found at the system root. 

```
flag{access_the_machine}
```

--- Cough (search -f flag(star).txt) this told me the location of each flag and i just cat them all. shhh

> Flag2? This flag can be found at the location where passwords are stored within Windows.

```
flag{sam_database_elevated_access}
```

> flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved. 


```
flag{admin_documents_can_be_valuable}
```


Great Box, I remember most of this from Heath Adams (TCM) course I picked up long ago on Udemy, now you can get it direct from TCM Academy!