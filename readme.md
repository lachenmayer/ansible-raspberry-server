**Work in progress - this probably will not work for you unless you're happy to mess around.**

# 0. Install ansible & passlib

```
pip install ansible passlib
```

- [Ansible](https://docs.ansible.com/ansible/latest/index.html) automates the setup of the Pi once Raspbian is installed on it.
- Passlib is needed to generate the user password.

# 1. Get Raspbian onto your SD card.

1. Download [Etcher](https://www.balena.io/etcher/)
2. Download [Raspbian Lite](https://www.raspberrypi.org/downloads/raspbian/) (if you want to use the Raspberry Pi with a screen, keyboard & mouse, then download the full Raspbian with desktop & recommended software - we're assuming that you just want to use it as a server.)
3. Open the downloaded image in Etcher, plug in your SD card & flash it. **Make sure you select the right drive if you have an external hard drive attached - flashing will overwrite anything that's on a drive.**
4. Unplug & plug your SD card back into your computer so it mounts again - we need to edit some files on the SD card before we can put it in the Pi.

(If you're allergic to Electron, you can also follow the guide for [manual installation](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md).)

# 2. Enable SSH

Raspberry Pis don't have SSH enabled by default. This is to ensure that you don't accidentally make your Pi accessible to the internet with the default password still set. Otherwise [online weirdos will try to do bad things with your Pi](https://www.zdnet.com/article/linux-malware-enslaves-raspberry-pi-to-mine-cryptocurrency/).

To enable SSH, do the following:

1. If you haven't done so already, insert the mini SD card into an SD adapter & plug it in to your computer (NOT the Raspberry Pi!)
2. Open up your Terminal & run the following:

    ```
    touch /Volumes/boot/ssh
    ```

    (If you get an error that says `No such file or directory`, unplug & plug back in your SD card - you should have a drive called "boot" show up in the Finder.)

# 2. Edit wi-fi settings

*You can skip this step if you only want to use the Pi with an Ethernet cable.*

If you want to use your Raspberry Pi on a wifi network, you need to give it your wifi password.

Change your wifi name & wifi password in the file called `wpa_supplicant.conf` in this repo.

Once you've done that, copy it onto the SD card:

```
cp ./wpa_supplicant.conf /Volumes/boot/
```

([source](https://www.raspberrypi-spy.co.uk/2017/04/manually-setting-up-pi-wifi-using-wpa_supplicant-conf/))

# 3. Put the SD card in the Pi & start it up

The moment you've been waiting for.

# 4. Try logging in to the Pi

```
ssh pi@raspberrypi.local
```

The default password is `raspberry`. (Nothing will show up while typing the password)

If you're able to log in, you're all good :)

# 5. Add your SSH key & change your password

```
ansible-playbook 01-auth.yml
```

This will prompt you for the location of your SSH public key and a password for the `pi` user.

In most cases, you should be fine with the default value for the SSH key, ie. if you don't know what you should input there, keep the default by pressing enter.

The output of this step is saved in `vars/auth.yml`.

# 6. Run the playbook

```
ansible-playbook all.yml --ask-pass
```
