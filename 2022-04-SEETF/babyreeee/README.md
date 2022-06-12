# babyreeee 

- Category: Reverse Engineering
- Points: 100/? 
- Captures: 189

## Challenge Description:
You've never seen a flagchecker this helpful.

For beginners:
https://ctf101.org/reverse-engineering/what-are-decompilers/


## Files Attached:
babyre (ELF binary)

## Solution:

### Tools used:
- [Cutter](https://cutter.re)
- [Pwntools](https://docs.pwntools.com/en/stable/install.html)

If we inspect the binary with cutter, we can use the decompiler to have a look at the main function:

![](cutter-main.png)
_I have scrolled down to the relevant section for getting more information_

We can see that the program takes in standard input (as seen in `fgets(str.HOI._0_8_, acStack344, 0x80, _stdin);`), then goes on to check the length of the string that we input if it is of length `0x35`, which in binary is **53** characters long, inclusive of the terminating null byte.

This means that our flag that we have to guess has to be **52** characters, since the terminating byte is automatically inserted when we enter our guessed flag (usually a `"\n"`). We can test this by sending a 52 character string into the binary, which reports that we have the right length flag but not the right first character as seen below.

![](test-length.png)

At this point, since we know from other challenges that most of the flags have a flag format of `SEE{<flag content>}`, we can try and check if this is also the case for this program:

![](test-format.png)

We test this by sending in `"SEE{"` followed by just a string of 'a's to pad the string and make it 52 characters long. As we can see, the flag check failed at index 4, and since the counting is zero-indexed, this means that the fifth character is wrong.

We can then write a Python script making use of `pwntools` to interact with the binary and brute force the flag, such as the one below:

```python
from pwn import process

foundFlag = False
SEED = "SEE{"
LENGTH = 52
POS = len(SEED)

while foundFlag != True:
    for i in range(32, 127):
        genstr = SEED + chr(i) + "a"*int(LENGTH-POS-1)
        p = process('./chall')
        a = p.recv()
        p.sendline(genstr.encode())
        a = p.recv()
        if "champ" in a.decode():
            foundFlag = True
            print("FLAG FOUNDDDDD")
            print(genstr)
            break
        else:
            try:
                numindex = a.decode().find("index: ")
                lookingPos = int(a[numindex+7:])
                if lookingPos > POS:
                    POS += 1
                    SEED = SEED + chr(i)
                    print(genstr)
            except:
                print(a)
        p.close()
```

Running the script will guess each printable ASCII character against the binary, eventually leading us to the flag!

![](flag-found.png)

## Flag:
```
SEE{0n3_5m411_573p_81d215e8b81ae10f1c08168207fba396}
```