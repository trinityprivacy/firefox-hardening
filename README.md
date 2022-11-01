# <img src="https://user-images.githubusercontent.com/114076168/199189876-ff5f49f8-975d-43fd-b040-9bee0b25f323.png" width="33" height="35"> Firefox Hardening Guide [![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fp4privacy%2Ffirefox-hardening&count_bg=%230000ff&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

This guide is about how to install Firefox on Linux via APT package manager and harden it to make your browsing as safe as possible

## Menu

* [Install Firefox via APT as DEB package](#install-firefox-via-apt-as-deb-package)
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

## Install Firefox via APT as DEB package

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

Finally, an efficient wide-spectrum content blocker. Easy on CPU and memory
Link: [click](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)

### BitWarden Password Manager

A secure and free password manager for all of your devices
Link: [click](https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager/)

### Skip Redirect

Some web pages use intermediary pages before redirecting to a final page. This add-on tries to extract the final url from the intermediary url and goes there straight away if successful.
Link: [click](https://addons.mozilla.org/en-US/firefox/addon/skip-redirect/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)

### LocalCDN

Emulates remote frameworks and delivers them as local resource. Prevents unnecessary 3rd party requests to Google, StackPath, MaxCDN and more.
Link: [click](https://addons.mozilla.org/en-US/firefox/addon/localcdn-fork-of-decentraleyes/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)

### Multi Account Container

It lets you keep parts of your online life separated into color-coded tabs. Cookies are separated by container, allowing you to use the web with multiple accounts
Link: [click](https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)
