# Super

- Category: Linux
- Points: 200
- Captures: 22
- Challenge Helpers: [@XeniaFiorenza](https://github.com/xeniafiorenza/CTF-Writeups/tree/main/CDDC%202021)

## Challenge Description:
```
This bot doesn’t look so important, it seems like he can do nothing…figure out how you can move on to the next user.
```
## Solution:

*blah blah login with previous flag*

After logging into this user, we can see that there is a `flag.txt` file in the home directory:

![](bot5-logon.png)

However, things are not as simple as we think, as the file has the permission `-r--------` or `0400`, meaning that it can only be read by its owner, `bot6`.

Because we are not `bot6` but `bot5`, we need to find some way to read this file as `bot6`.

We can check what kind of permissions we have with the sudo command with `sudo -l`

![](bot5-perms.png)

This tells us that we can run the `cat` command in the `/var/log` folder as `bot6` without any password.

However, as the flag is in `bot5`'s home folder, we need to get *slightly* creative with how we access it...

and by that I mean path traversal!

By running `sudo -u bot6 cat /var/log/../../home/bot5/flag.txt`, we can get `bot6` to execute `cat` on the file that is in `bot5`'s home directory, by traversing 2 levels up from `/var/log` and into the root directory, then into `bot5`'s home directory from there:

![](bot5-flag.png)
## Flag:
```
CDDC21{b3w4r3sud03rz}
```