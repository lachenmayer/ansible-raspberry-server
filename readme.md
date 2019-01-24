# 1. Follow official instructions for getting Raspbian onto your SD card.

Using NOOBS:

- https://www.raspberrypi.org/documentation/installation/noobs.md

Manually:

- https://www.raspberrypi.org/documentation/installation/installing-images/mac.md

# 2. Enable SSH

```
touch /Volumes/boot/ssh
```

# 2. Edit wi-fi settings

([source](https://www.raspberrypi-spy.co.uk/2017/04/manually-setting-up-pi-wifi-using-wpa_supplicant-conf/))

Change your wifi name & wifi password in `wpa_supplicant.conf`.

Once you've done that, copy it onto the SD card:

```
cp ./wpa_supplicant.conf /Volumes/boot/
```

# 3. Put the SD card in the Pi & start it up

# 4. Find the Pi on the network

```
nmap -sn 192.168.0.1/24
```

# 5. Try logging in to the Pi

```
ssh pi@<the IP address you just found>
```

The default password is `raspberry`.

If you're able to log in, note down the IP address.