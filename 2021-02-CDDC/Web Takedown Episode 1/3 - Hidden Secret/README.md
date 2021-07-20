# Hidden Secret

- Category: Web
- Points: 200
- Captures: 55
- Challenge Helpers: [@Isacara](https://github.com/Iscaraca)

## Challenge Description:
```
This server looks promising. Can you find the secret?

Target URL: <removed>
```
## Solution:
### Tools used:
- [CyberChef](https://gchq.github.io/CyberChef/)


```js
var pass = unescape("unescape%28%22String.fromCharCode%252867%252C68%252C68%252C67%252C50%252C49%252C123%252C95%252C32%252C68%252C101%252C48%252C98%252C102%252C117%252C36%252C99%252C97%252C116%252C101%252C100%252C45%252C70%252C33%252C97%252C71%252C95%252C125%2529%22%29");
```
![Decoding the Command](./urlDecode.png)
![Evaluating the CharCode](./evaluated.png)

## Flag:
```
CDDC21{_ De0bfu$cated-F!aG_}
```