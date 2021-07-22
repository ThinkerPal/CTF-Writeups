# Lock and Key 

- Category: Linux
- Points: 100
- Captures: 42
- Challenge Helpers: [@XeniaFiorenza](https://github.com/xeniafiorenza/CTF-Writeups/tree/main/CDDC%202021)

## Challenge Description:
```
One of TheKeepers has successfully obtained what seems to be one of the GDC private servers. He has sent me the image and another file, but unfortunately, I’m not great with Linux. I think you’re the one for this mission.
```
A zip file and an IP address was given for us to access the server
## Solution:

In the zip file, there are two files:
- `cybot01_bot1.key`, the ssh key used for logging into the server
- `Note.txt`, which gives us the following message:
```
Notice


1. As part of the ZIP file, you will find a text file that can be used to connect to the target machine. 

2. Each one of the flags is the password for the next user. Your main goal is to access the last user account.

3. The flags are located in the user home folders.
```
After connecting to the remote server via `ssh`, we can simply do an `ls`, which shows that there is a flag file called `flag.txt` in the home folder, which we can simply read!

![](bot1-flag.png)

## Flag:
```
CDDC21{b0t_eNtR3nC3}
```