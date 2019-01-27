# 0. Install ansible & passlib

```
pip install ansible passlib
```

- [Ansible](https://docs.ansible.com/ansible/latest/index.html) automates the setup of the Pi once Raspbian is installed on it.
- Passlib is needed to generate the user password.

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

# 4. Try logging in to the Pi

```
ssh pi@raspberrypi.local
```

The default password is `raspberry`.

If you're able to log in, you're all good :)

# 5. Add your SSH key & change your password

```
ansible-playbook 01-auth.yml
```

This will prompt you for the location of your SSH public key and a password for the `pi` user.

In most cases, you should be fine with the default value for the SSH key, ie. if you don't know what you should input there, keep the default by pressing enter.

The output of this step is saved in `vars/auth.yml`.
