# Flag in Flame (Forensics)

Grab the log file as shown below using `wget` command

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/flag_in_flame]
└─$ wget https://challenge-files.picoctf.net/c_amiable_citadel/53216672a2c2381d0ed77a981fbf595657b3a8be3f0e0edff71b33c1baa6c9d6/logs.txt
--2026-01-26 14:55:07--  https://challenge-files.picoctf.net/c_amiable_citadel/53216672a2c2381d0ed77a981fbf595657b3a8be3f0e0edff71b33c1baa6c9d6/logs.txt
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 108.158.61.119, 108.158.61.94, 108.158.61.37, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|108.158.61.119|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1592268 (1.5M) [application/octet-stream]
Saving to: ‘logs.txt’

logs.txt                      100%[================================================>]   1.52M  1.27MB/s    in 1.2s    

2026-01-26 14:55:09 (1.27 MB/s) - ‘logs.txt’ saved [1592268/1592268]
```

Here  we have to decode this log file using `base64` and we will save the output on another file, because the `logs.txt` contains a big base64 encoded text 

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/flag_in_flame]
└─$ base64 -d logs.txt >> op        
                                                                                                      
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/flag_in_flame]
└─$ ls
logs.txt  op
```

Here we decoded `logs.txt` and saved its result in `op` file.

Now by seeing the metadata of this output file we can get that it is an `.png` image. Using `mv` command we will rename the file and add extension `.png` .

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/flag_in_flame]
└─$ exiftool op 
ExifTool Version Number         : 13.36
File Name                       : op.out
......
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
.....

┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/flag_in_flame]
└─$ mv op op.png
```

When we open this image we can see some `hex` in the image when we decode it using any online decoding tools such as `cyberchef` , the recipe will be `From Hex` we get out final flag

![image.png](image.png)

HEX:`7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35636363376362307D`

Final flag: `picoCTF{forensics_analysis_is_amazing_5ccc7cb0}`