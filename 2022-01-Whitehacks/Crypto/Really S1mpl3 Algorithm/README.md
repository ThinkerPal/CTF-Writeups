# Really S1mp(l3) Algorithm

- Category: Crypto
- Points: 135/1000
- Captures: 72
## Challenge Description:
Rumour has it that this algorithm originated from the Republic of South Africa!

## Files Attached:
[challenge.txt](challenge.txt)
## Solution:

### Tools that would have been helpful:
- [factordb.com](factordb.com)

Taking a look at the file, we see 4 variables `p`, `q`, `e` and `ct` defined, and further taking inspiration from the initals of this challenge, we can infer that this challenge has to deal with RSA (and decrypting the ciphertext).

With some quick googling, I found [this page](https://www.amazingtricks.in/how-to-solve-rsa-crypto-challenges-in-ctfs/) and its accompanying code to decrypt our ciphertext. Since in our case the components of the prime `p` and `q` have been given to us, we do not need to factorsie anything (which the site recommeneded [factordb](factordb.com) for.)

A quick edit to the code later, we end up with this:

```python
#!/usr/bin/python3
from Crypto.Util.number import inverse
p = 89677525768054651799811339393073439598902155753884683756875620558829954902529

q = 84438062750417241222463359000671279258755386034358736244893269480285225711041

e = 65537

ct = 2006481391032768131106572837821981606814991526844317992631122301790966354846642917808142106585149537517169168108747108233658443914026685951141453359021205

phi = (p-1)*(q-1)
d=inverse(e, phi)
m=pow(ct,d,p*q)
print(hex(m)[2:-1])
```

Running the program after that gives us a hexadecimal string, which we can then throw into [CyberChef](gchq.github.io/CyberChef) to convert to our flag.

(Note: I did realise when runnning the python program that there was a little bit of a weird ending to the flag – I'm pretty sure that if I bothered to look at the code more I could have fixed it, but in my case I just removed the trailing period with a closing curly brace)

## Flag:
```
WH2022{1t5_r34lly_s1mpl3_4m_1_r1ght}
```