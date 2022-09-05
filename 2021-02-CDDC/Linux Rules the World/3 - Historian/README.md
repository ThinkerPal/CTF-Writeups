# Historian

- Category: Linux
- Points: 200
- Captures: 39
- Challenge Helpers: [@XenosF](https://github.com/XenosF/CTF-Writeups/tree/main/CDDC%202021)

## Challenge Description:
```
Some more intel has been recovered and it hints at new program developments the cyber bots system is running, the code is supposedly used to encrypt secrets.
```
## Solution:

![](bot3-logon.png)

Using the previous flag to log into this user, we can see that there is a new file, `.viminfo` in the home directory that was not in the previous home folders.

![](bot3-flag.png)

Opening it up, we can see that there are "illegal starting characters", mostly pertaining to the file at `/usr/local/share/secret`. Reading that file, we can find the next flag.
## Flag:
```
CDDC21{V1m_th3_s4vior}
```