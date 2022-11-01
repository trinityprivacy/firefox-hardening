# Firefox Hardening: Make your browser safe

This guide is about how to install Firefox on Linux and harden it to make it as safe as possible

## Menu

* [Install Firefox as DEB package](#install-firefox-as-deb-package)
    - [Remove Firefox from Snap](#remove-firefox-from-snap)
    - [Add Mozilla Team Repository](#add-mozilla-team-repository)
    - [Set the deb version as preferred](#set-the-deb-version-as-preferred)
    - [Set automatic Updates](#set-automatic-updates)
    - [Install the package via apt](#install-the-package-via-apt)
* [User Configuration File](#user-configuration-file)
    - [Download Link](#download-link)
    - [Extract the files](#extract-the-files)
* [Recommended Extensions](#recommended-extensions)
    - [uBlock Origin](#ublock-origin)
    - [BitWarden Password Manager](#bitwarden-password-manager)
    - [Skip Redirect](#skip-redirect)
    - [LocalCDN](#localcdn)
    - [Multi Account Containers](#multi-account-containers)

## Install Firefox as DEB package

### Remove Firefox from Snap

On your computer open a terminal and type:
```bash
sudo snap remove firefox
```

### Add Mozilla Team Repository

Run the following command in the same Terminal window:
```bash
sudo add-apt-repository ppa:mozillateam/ppa
```

## Set the deb version as preferred

We will alter the Firefox package priority to ensure the PPA/deb/apt version of Firefox is preferred
```bash
echo '
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
' | sudo tee /etc/apt/preferences.d/mozilla-firefox
```

## Set automatic Updates

To have future Firefox upgrades to be installed automatically type:
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

## Install the package via apt
```bash
sudo apt install firefox
```

## User Configuration File

### Download Link

The file user.js-xxx.zip can be downloaded from this repository: [https://github.com/arkenfox/user.js](https://github.com/arkenfox/user.js)

### Extract the files

In your Firefox browser tab type:
```bash
about:profiles
```

Copy the profile root directory you want to add the user.js file into
```bash
Example: /home/user/.mozilla/firefox/abcded.profile-name
```

Extract the files from the .zip file:
```bash
unzip -q user.js-xxx.zip
```

Go into the extracted folder:
```bash
cd user.js-xxx/
```
Copy the content of the folder into the profile root directory
```bash
cp *.* /home/user/.mozilla/firefox/abcded.profile-name
```
Now, if you re-open your browser and everything has gone fine, you should see something like a windows opened in a window, this is because the resolution has been spoofed and the reason is to prevent canvas fingerprinter.


## Recommended Extensions

### uBlock Origin

Link: [click](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)

### BitWarden Password Manager

aaa

### Skip Redirect

aaa

### LocalCDN

aaa

### Multi Account Container

aaa
