# Hidden in Plainsight (Forensics)

Grab the log file as shown below using `wget` command

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/hidden_in_plainsight]
└─$ wget https://challenge-files.picoctf.net/c_amiable_citadel/a9f79ebd7dfa722721b5cbdd12a5059e9404c28c90b9b0bf9e307015f8c1c265/img.jpg   
--2026-01-26 13:20:39--  https://challenge-files.picoctf.net/c_amiable_citadel/a9f79ebd7dfa722721b5cbdd12a5059e9404c28c90b9b0bf9e307015f8c1c265/img.jpg
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 108.158.61.37, 108.158.61.119, 108.158.61.97, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|108.158.61.37|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 73517 (72K) [application/octet-stream]
Saving to: ‘img.jpg’

img.jpg                                      100%[============================================================================================>]  71.79K   200KB/s    in 0.4s    

2026-01-26 13:20:40 (200 KB/s) - ‘img.jpg’ saved [73517/73517]
```

By checking the metadata of this image we can see that `Comment` is encoded in `base64` format so we will decode it using `cyberchef`

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/hidden_in_plainsight]
└─$ exiftool img.jpg

ExifTool Version Number         : 13.36
File Name                       : img.jpg
Directory                       : .
File Size                       : 74 kB
File Modification Date/Time     : 2025:11:08 00:47:39+05:30
File Access Date/Time           : 2026:01:26 13:22:20+05:30
File Inode Change Date/Time     : 2026:01:26 13:20:40+05:30
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9
Image Width                     : 640
Image Height                    : 640
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 640x640
Megapixels                      : 0.410
```

When we decode it first time we get `steghide:cEF6endvcmQ=` . From this output we get to know that we have to extract the data with the help of `steghide` tool, but key is encoded.

So now we will decode the key `cEF6endvcmQ=`using same `base64` decode and we will get `pAzzword` 

So when we will extract this `img.jpg` using `steghide` we will get a file named `flag.txt` 

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/hidden_in_plainsight]
└─$ steghide extract -sf img.jpg -p pAzzword

wrote extracted data to "flag.txt".
                                                                                                                                                                                  
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/hidden_in_plainsight]
└─$ ls
flag.txt  img.jpg
                                                                                                                                                                                  
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/hidden_in_plainsight]
└─$ cat flag.txt 
picoCTF{h1dd3n_1n_1m4g3_e7f5b969}
```

FInal flag: `picoCTF{h1dd3n_1n_1m4g3_e7f5b969}`