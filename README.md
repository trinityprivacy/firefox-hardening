# <img src="https://user-images.githubusercontent.com/114076168/199189876-ff5f49f8-975d-43fd-b040-9bee0b25f323.png" width="33" height="35"> Firefox Hardening Guide [![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fp4privacy%2Ffirefox-hardening&count_bg=%230000ff&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

This guide is about how to install Firefox on Linux via APT package manager and harden it to make your browsing as safe as possible

## Menu

* [Install Firefox via APT as DEB package](#install-firefox-via-apt-as-deb-package)
* [First Method: User Configuration File](#first-method-user-configuration-file)
* [Second Method: Firefox Profile Maker](#second-method-firefox-profile-maker)
* [Recommended Extensions](#recommended-extensions)

## Install Firefox via APT as DEB package

#### Remove Firefox from Snap

This is an optional step, but as lot of people do not like snap package manager, I thought to add this step as well in case you want to make a fresh install

On your computer open a terminal and type:
```bash
sudo snap remove firefox
```

#### Add Mozilla Team Repository

Run the following command in the same Terminal window:
```bash
sudo add-apt-repository ppa:mozillateam/ppa
```

#### Set the deb version as preferred

We will alter the Firefox package priority to ensure the PPA/deb/apt version of Firefox is preferred
```bash
echo '
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
' | sudo tee /etc/apt/preferences.d/mozilla-firefox
```

#### Set automatic Updates

To have future Firefox upgrades to be installed automatically type:
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

#### Install the package via apt
```bash
sudo apt install firefox
```

## First Method: User Configuration File

The [arkenfox/user.js](https://github.com/arkenfox/user.js) is a configuration file which aims to provide as much privacy and enhanced security as possible, and to reduce tracking and fingerprinting as much as possible - while minimizing any loss of functionality and breakage.

#### Download Link

The file user.js-xxx.zip can be downloaded from the repository [release page](https://github.com/arkenfox/user.js/releases)
Be aware that before proceeding with this methos, a read to the [wiki](https://github.com/arkenfox/user.js/wiki) is highly recommended!

#### Extract the files

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


## Second Method: Firefox Profile Maker

This is an online tool that will help you to create a Firefox profile with the defaults you like.
You select which features you want to enable and disable and in the end you get a download link for a zip-file with your profile template

### Installation

- First step is going to the website [https://ffprofile.com](https://ffprofile.com) and foolow the steps.
The process is pretty straightforward and you can also select the addons/extensions which will be automatically installed.
I have listed anyway some recommended extensions at the end of this guide.
At the end of the step by step process you will have 4 download options, but we will go with the complete one and download he file profile.zip

- Optional: add a new profile to keep the old one
  - Run on a terminal:
  ```bash
  firefox -no-remote -ProfileManager
  ```
  - Create a new profile
- Type about:support into the firefox url bar.
- Press the open profile folder button.
- Quit Firefox.
- Delete everything from the new profile (you will lose all existing data from the profile).
- Unzip the profile.zip archive into the folder.
- If Existent: Unzip the enterprise_policy.zip archive to Firefox installation directory.
- Start Firefox again. If you made a new profile, you can use it with firefox -no-remote -P profilename.
- Open the addon manager and update the extensions.


## Recommended Extensions

- <img src="https://user-images.githubusercontent.com/114076168/199192811-6b6bed17-2af7-49ea-9cad-0e49dfafeaae.png" width="20" height="20"> [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search). After installing the extension go to Preferences -> Filter Lists and:
  - Enable "AdGuard Tracking Protection" on Privacy section
  - Import [Actually Legitimate URL Shortener Tool](https://raw.githubusercontent.com/DandelionSprout/adfilt/master/LegitimateURLShortener.txt) on Import -> Custom, paste the link and click on Apply
- <img src="https://user-images.githubusercontent.com/114076168/199192844-f0a42bbd-8d9a-47fc-9f8f-8cc0cc111db4.png" width="20" height="20"> [BitWarden Password Manager](https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager/)
- <img src="https://user-images.githubusercontent.com/114076168/199192916-00b00905-273c-4d4c-bfa6-e20bd38929fc.png" width="20" height="20"> [Skip Redirect](https://addons.mozilla.org/en-US/firefox/addon/skip-redirect/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)
- <img src="https://user-images.githubusercontent.com/114076168/199192958-a7f47ee3-96e0-48ca-b18a-1cbe52f0e1cb.png" width="20" height="20"> [LocalCDN](https://addons.mozilla.org/en-US/firefox/addon/localcdn-fork-of-decentraleyes/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)
- <img src="https://user-images.githubusercontent.com/114076168/199193068-5af38361-5d44-496e-94a2-3c88603c54f1.png" width="20" height="20"> [Firefox Multi-Account Container](https://addons.mozilla.org/en-US/firefox/addon/localcdn-fork-of-decentraleyes/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)
