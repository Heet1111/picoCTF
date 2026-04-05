# Log Hunt (General Skills)

Grab the log file as shown below using `wget` command

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/log_hunt]
└─$ wget https://challenge-files.picoctf.net/c_amiable_citadel/49cec6157142f24a599f4164d5b63322c2494f801390d6f22eb91b3aa592bc66/server.log      
--2026-01-26 12:46:22--  https://challenge-files.picoctf.net/c_amiable_citadel/49cec6157142f24a599f4164d5b63322c2494f801390d6f22eb91b3aa592bc66/server.log
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 108.158.61.94, 108.158.61.119, 108.158.61.37, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|108.158.61.94|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 108322 (106K) [application/octet-stream]
Saving to: ‘server.log’

server.log                    100%[================================================>] 105.78K   356KB/s    in 0.3s    

2026-01-26 12:46:24 (356 KB/s) - ‘server.log’ saved [108322/108322]
```

Now as we know the log file is scattered and we have to find the flag

We already know that the flag starts with `picoCTF` so we will find it using command `grep` 

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/log_hunt]
└─$ grep 'picoCTF' server.log                   
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:27] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:29] INFO FLAGPART: picoCTF{us3_
```

Here we only get the first part of our flag, and we can get other parts using filter `FLAGPART` instead of `picoCTF` 

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/log_hunt]
└─$ grep FLAGPART server.log    
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 10:02:55] INFO FLAGPART: y0urlinux_
[1990-08-09 10:05:54] INFO FLAGPART: sk1lls_
[1990-08-09 10:05:55] INFO FLAGPART: sk1lls_
[1990-08-09 10:10:54] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:10:58] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:11:06] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:04:27] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:29] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:04:37] INFO FLAGPART: picoCTF{us3_
[1990-08-09 11:09:16] INFO FLAGPART: y0urlinux_
[1990-08-09 11:09:19] INFO FLAGPART: y0urlinux_
[1990-08-09 11:12:40] INFO FLAGPART: sk1lls_
[1990-08-09 11:12:45] INFO FLAGPART: sk1lls_
[1990-08-09 11:16:58] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:16:59] INFO FLAGPART: cedfa5fb}
[1990-08-09 11:17:00] INFO FLAGPART: cedfa5fb}
```

By connecting all the parts we get our flag.

Final flag: `picoCTF{us3_y0urlinux_cedfa5fb}`