# DISKO 1 (Forensics)

Grab the file as shown below using `wget` command

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/disko_1]
└─$ wget https://artifacts.picoctf.net/c/537/disko-1.dd.gz
--2026-01-31 22:56:02--  https://artifacts.picoctf.net/c/537/disko-1.dd.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.159.61.105, 108.159.61.109, 108.159.61.26, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.159.61.105|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 20484478 (20M) [application/octet-stream]
Saving to: ‘disko-1.dd.gz’

disko-1.dd.gz             100%[===================================>]  19.54M  5.94MB/s    in 3.3s    

2026-01-31 22:56:06 (5.94 MB/s) - ‘disko-1.dd.gz’ saved [20484478/20484478]
```

This file is compressed because it has extension of `.gz` , firstly we have to extract it we will do this with the help of `gunzip` .

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/disko_1]
└─$ gunzip -k disko-1.dd.gz

┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/disko_1]
└─$ ls
disko-1.dd  disko-1.dd.gz
```

Now we will get a file named `disko-1.dd` as shown here.

This is a disk image so we cannot read it with any text viewer, so we will just grab the string s present in this disk image. We will do it with the `strings` . 

When we run the command `strings disko-1.dd` we get too many strings and finding the flag will be too much time consuming but we know that the flag always starts with `picoCTF` so we will just extract the string that starts with `picoCTF` to do that we will pipe the `grep` command

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/disko_1]
└─$ strings disko-1.dd | grep "picoCTF"
picoCTF{1t5_ju5t_4_5tr1n9_be6031da}
```

FInal flag: `picoCTF{1t5_ju5t_4_5tr1n9_be6031da}`