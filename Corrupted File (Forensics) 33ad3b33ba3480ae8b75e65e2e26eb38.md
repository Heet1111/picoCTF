# Corrupted File (Forensics)

Grab the file as shown below using `wget` command 

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/corrupted_file]
└─$ wget https://challenge-files.picoctf.net/c_amiable_citadel/9371995b0773e9fee9af0d339adebcfa3f05ce79b0a30220449982ea9d9f2c1b/file
--2026-01-31 21:33:22--  https://challenge-files.picoctf.net/c_amiable_citadel/9371995b0773e9fee9af0d339adebcfa3f05ce79b0a30220449982ea9d9f2c1b/file
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 108.158.61.37, 108.158.61.94, 108.158.61.97, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|108.158.61.37|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8759 (8.6K) [application/octet-stream]
Saving to: ‘file’

file                      100%[===================================>]   8.55K  --.-KB/s    in 0s      

2026-01-31 21:33:28 (356 MB/s) - ‘file’ saved [8759/8759]
```

Here this file is corrupted but by seeing the hex of this file we can get that it is an `jpeg` file.

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/corrupted_file]
└─$ hexdump -C file | head
00000000  5c 78 ff e0 00 10 4a 46  49 46 00 01 01 00 00 01  |\x....JFIF......|
00000010  00 01 00 00 ff db 00 43  00 08 06 06 07 06 05 08  |.......C........|
00000020  07 07 07 09 09 08 0a 0c  14 0d 0c 0b 0b 0c 19 12  |................|
00000030  13 0f 14 1d 1a 1f 1e 1d  1a 1c 1c 20 24 2e 27 20  |........... $.' |
00000040  22 2c 23 1c 1c 28 37 29  2c 30 31 34 34 34 1f 27  |",#..(7),01444.'|
00000050  39 3d 38 32 3c 2e 33 34  32 ff db 00 43 01 09 09  |9=82<.342...C...|
00000060  09 0c 0b 0c 18 0d 0d 18  32 21 1c 21 32 32 32 32  |........2!.!2222|
00000070  32 32 32 32 32 32 32 32  32 32 32 32 32 32 32 32  |2222222222222222|
*
00000090  32 32 32 32 32 32 32 32  32 32 32 32 32 32 ff c0  |22222222222222..|
```

In this file the digital signature bytes are not true so we cannot open this file and get the output so we will change its digital signature. 

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/corrupted_file]
└─$ printf '\xFF\xD8\xFF' | dd of=file bs=1 seek=0 count=3 conv=notrunc

3+0 records in
3+0 records out
3 bytes copied, 7.2044e-05 s, 41.6 kB/s

┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/corrupted_file]
└─$ mv file file.jpeg
```

`printf '\xFF\xD8\xFF' | dd of=file bs=1 seek=0 count=3 conv=notrunc` 

`printf '\xFF\xD8\xFF'` : change the first bytes of file.

`dd of=file` : specify the file name

`bs-1` : block size 1 byte

`seek=0` : start writing at byte offset 0 (starting)

`count=3` : write 3 exactly bits

`conv=notrunc` : do not truncate file after transferring

Now we will have to add an extension to a file `.jpeg` to view the image 

```bash
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/corrupted_file]
└─$ mv file file.jpeg 
```

After fixing the file we can see the changes in hex / digital signature of file

```bash
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/forensics/corrupted_file]
└─$ hexdump -C file.jpeg | head
00000000  ff d8 ff e0 00 10 4a 46  49 46 00 01 01 00 00 01  |......JFIF......|
00000010  00 01 00 00 ff db 00 43  00 08 06 06 07 06 05 08  |.......C........|
00000020  07 07 07 09 09 08 0a 0c  14 0d 0c 0b 0b 0c 19 12  |................|
00000030  13 0f 14 1d 1a 1f 1e 1d  1a 1c 1c 20 24 2e 27 20  |........... $.' |
00000040  22 2c 23 1c 1c 28 37 29  2c 30 31 34 34 34 1f 27  |",#..(7),01444.'|
00000050  39 3d 38 32 3c 2e 33 34  32 ff db 00 43 01 09 09  |9=82<.342...C...|
00000060  09 0c 0b 0c 18 0d 0d 18  32 21 1c 21 32 32 32 32  |........2!.!2222|
00000070  32 32 32 32 32 32 32 32  32 32 32 32 32 32 32 32  |2222222222222222|
*
00000090  32 32 32 32 32 32 32 32  32 32 32 32 32 32 ff c0  |22222222222222..|
                                                                                
```

Now open the image and we can see the flag 

Final flag: `picoCTF{r3st0r1ng_th3_by73s_2326ca93}`