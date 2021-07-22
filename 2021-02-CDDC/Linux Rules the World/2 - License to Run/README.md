# License to Run

- Category: Linux
- Points: 100
- Captures: 39
- Challenge Helpers: [@XeniaFiorenza](https://github.com/xeniafiorenza/CTF-Writeups/tree/main/CDDC%202021)

## Challenge Description:
```
Glad to hear that you are in. bot2 has been sent to release some malicious files in a few days. Can you find and check it?
```
## Solution:

Following the instructions in the Note, specifically the following:
> 2. Each one of the flags is the password for the next user. Your main goal is to access the last user account.

We use the previous flag as the password for the second account, `bot2`

![](bot2-logon.png)

As we can see, there is a hidden executable file named `.#flag$!!1` in the home directory. Running this program gives us the next flag:

![](bot2-flag.png)
## Flag:
```
CDDC21{TH4nKsF0R_p3RM}
```