# Riddle Registry (Forensics)

This challenge is related to forensics, so we need to investigate to solve this puzzle. 

Here we are given a PDF file which we have to grab it, since i am using Kali Linux so i will copy the link address and in terminal i will run

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/riddle_registery]
└─$ wget https://challenge-files.picoctf.net/c_amiable_citadel/5da2648ffaf783a1015aec626491641b7907e0991c16cb6c771aaaea387c18f6/confidential.pdf
--2026-01-26 12:38:48--  https://challenge-files.picoctf.net/c_amiable_citadel/5da2648ffaf783a1015aec626491641b7907e0991c16cb6c771aaaea387c18f6/confidential.pdf
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 108.158.61.97, 108.158.61.94, 108.158.61.37, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|108.158.61.97|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 182705 (178K) [application/octet-stream]
Saving to: ‘confidential.pdf.1’

confidential.pdf.1            100%[================================================>] 178.42K  --.-KB/s    in 0.1s    

2026-01-26 12:38:49 (1.32 MB/s) - ‘confidential.pdf.1’ saved [182705/182705]
```

When we open a PDF and read it we did not find anything useful. So we try to see metadata of this PDF.

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/riddle_registery]
└─$ exiftool confidential.pdf       
ExifTool Version Number         : 13.36
File Name                       : confidential.pdf
Directory                       : .
File Size                       : 183 kB
File Modification Date/Time     : 2025:11:08 00:47:36+05:30
File Access Date/Time           : 2026:01:31 21:29:34+05:30
File Inode Change Date/Time     : 2026:01:26 12:24:51+05:30
File Permissions                : -rw-rw-r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 1
Producer                        : PyPDF2
Author                          : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV8zNTc4NzM5YX0=
```

While seeing metadata of this we get that Author name is encrypted in `base64` format by decoding it we get our final flag.

Final flag: `picoCTF{puzzl3d_m3tadata_f0und!_3578739a}`