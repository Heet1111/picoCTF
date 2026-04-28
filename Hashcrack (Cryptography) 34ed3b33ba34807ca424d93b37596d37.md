# Hashcrack (Cryptography)

In this challenge we do not get any of the files that we have to download. In this task we have to connect it remotely through `nc`  command which will be provided while launching the instance.

```jsx
┌──(parallels㉿kali-linux-2024-2)-[~/ctf/picoctf/cryptography/hashcrack]
└─$ nc verbal-sleep.picoctf.net 56046~
Welcome!! Looking For the Secret?

We have identified a hash: 482c811da5d5b4bc6d497ffa98491e38
Enter the password for identified hash: password123
Correct! You've cracked the MD5 hash with no secret found!

Flag is yet to be revealed!! Crack this hash: b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
Enter the password for the identified hash: letmein
Correct! You've cracked the SHA-1 hash with no secret found!

Almost there!! Crack this hash: 916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745
Enter the password for the identified hash: qwerty098
Correct! You've cracked the SHA-256 hash with a secret found. 
The flag is: picoCTF{UseStr0nG_h@shEs_&PaSswDs!_6965e43b}
```

In this challenge we have to decode the provided encoded value and get to the flag. As you can see above, they provided the hash we have to find which type of hash is this and then decode it.

| Encoded | Type | Decoded |
| --- | --- | --- |
| 482c811da5d5b4bc6d497ffa98491e38 | md5 | password123 |
| b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3 | sha1 | letmein |
| 916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745 | sha256 | qwerty098 |

Final Flag: `picoCTF{UseStr0nG_h@shEs_&PaSswDs!_6965e43b}`