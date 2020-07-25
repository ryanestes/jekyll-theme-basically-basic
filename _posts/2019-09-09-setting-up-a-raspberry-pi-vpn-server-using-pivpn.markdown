---
layout: post
title: Setting up SSH, PiVPN, and Pi-Hole on a Raspberry Pi
date: '2019-09-09 03:04:00'
tags:
- raspberry-pi
- how-to
- linux
- web-security
- pivpn
- vpn
- pi-hole
- ssh
---

The Raspberry Pi is a versatile, credit card-sized computer that is used for a [myriad of different projects](https://projects.raspberrypi.org/en/). As a personal project of mine, I've tailored my Raspberry Pi 3 to be a personal VPN, network advertisement blocker, and additionally, a bad domain blocker as well. This post will go over how to perform a similar task at a high-level, specifically:

- Enable SSH on your RPi
- Setup a simple personal VPN using PiVPN
- Setup an adblocker using Pi-Hole
- Add a phishing domain feed to Pi-Hole to kickstart the bad domain blocker
- Edit the pi-hole cron job to update daily instead of weekly
  

_NOTE: This proof-of-concept was created using a Raspberry Pi 3 Model B+ running Raspbian Buster v4.19. As of this writing, the Raspberry Pi 4 is the current model and this is the recommended model for this project (or the most current model)._

<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->

[SSH Setup](#sshsetup)  
[PiVPN Setup](#pivpnsetup)  
[Pi-Hole Setup](#pi-holesetup)  
[Pi-hole Domain Feed Configuration](#pi-holedomainfeedconfiguration)

<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->  

## SSH Setup
  
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Straight To It

_Taken directly from the [Raspberry Pi SSH Documentation](https://www.raspberrypi.org/documentation/remote-access/ssh/)_:

  

As of the November 2016 release, Raspbian has the SSH server disabled by default. It can be enabled manually from the desktop:

1. Launch `Raspberry Pi Configuration` from the `Preferences` menu
2. Navigate to the `Interfaces` tab
3. Select `Enabled` next to `SSH`
4. Click `OK`
  

Alternatively, raspi-config can be used in the terminal:

1. Enter `sudo raspi-config` in a terminal window
2. Select `Interfacing Options`
3. Navigate to and select `SSH`
4. Choose `Yes`
5. Select `Ok`
6. Choose `Finish`
  

Alternatively, use `systemctl` to start the service

`sudo systemctl enable ssh`  
`sudo systemctl start ssh`

  

When enabling SSH on a Pi that may be connected to the internet, you should change its default password to ensure that it remains secure. See the Security page for more details.

  
  
<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->  

## PiVPN Setup
  
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Visual Guide

1. Open a Terminal window

![vpn8-terminalopen](/content/images/2019/10/vpn8-terminalopen.png)

  
  
  
  

1. Enter the following command, per the PiVPN website:

`curl -L https://install.pivpn.io | bash`

  

**Note** : _Piping to bash_ (`| bash`) _will run the install automatically. Simply run the command with it to install download and then run (`curl -L https://install.pivpv.io`)_

![pivpn10-installpivpn](/content/images/2019/10/pivpn10-installpivpn.png)

  
  
  
  

1. If you entered the command above the **PiVPN Automated Installer** modal will appear stating that this installer will turn the RPi into an OpenVPN server. Click `Enter`

![pivpn11-welcomepivpn](/content/images/2019/10/pivpn11-welcomepivpn.png)

  
  
  
  

1. The installer will apply a static IP address to the raspberry pi, this is required. As a safeguard, go into your router's DHCP settings and set your RPi's IP as static

![pivpn12-staticipneeded](/content/images/2019/10/pivpn12-staticipneeded.png)

  
  
  
  

1. This shows your RPi's current IP address and asks if you want to set it as static, hit `Enter`

![pi5-1](/content/images/2019/10/pi5-1.jpg)

  
  
  
  

1. This is a warning indicating what might happen if you don't set the RPi's IP address as static

![pivpn14-ipconflict](/content/images/2019/10/pivpn14-ipconflict.png)

  
  
  
  

1. PiVPN will then ask for a local user to run the ovpn configuration

![pivpn15-localusers](/content/images/2019/10/pivpn15-localusers.png)

  
  
  
  

1. My RPi only has one user for this proof of concept so I will select it and press `Enter`

![pivpn16-chooseauser](/content/images/2019/10/pivpn16-chooseauser.png)

  
  
  
  

1. This modal is important. PiVPN warns about daily updates for the security package updates. Since I am running this RPi headless via SSH, I want me RPi to periodically update, so I recommend this step. Press `Enter`, PiVPN can do this for you as well!

![pivpn17-unattendedupgrades](/content/images/2019/10/pivpn17-unattendedupgrades.png)

  
  
  
  

1. This is the screen that will ask if you want to enable **Unattended Upgrades** , select **Yes** and press `Enter`

![pivpn18-enableunattendedupgrades](/content/images/2019/10/pivpn18-enableunattendedupgrades.png)

  
  
  
  

1. OpenVPN runs via TCP and UDP ports 1194, but usually UDP port 1194. Stick to just UDP port 1194 and go down to **Ok** and click `Enter`

![pivpn19-protocol](/content/images/2019/10/pivpn19-protocol.png)

  
  
  
  

1. Don't change the default port unless there is a specific reason to; hit `Enter`

![pivpn20-dafaultopenvpnport](/content/images/2019/10/pivpn20-dafaultopenvpnport.png)

  
  
  
  

1. Confirm these settings and click `Enter`

![pivpn21-confirmcustomportnumber](/content/images/2019/10/pivpn21-confirmcustomportnumber.png)

  
  
  
  

1. This next screen is all about OpenVPN version compatibility. For best security, select **Yes** to run Elliptic Curve key exchange or **No** to be able to run lower compatible versions. Select **Yes** in most scenarios

![pivpn22-installationmodeEC](/content/images/2019/10/pivpn22-installationmodeEC.png)

  
  
  
  

1. You should not change the ECDSA certifiate bit encryption size. 256-bit is sufficient as of this writing. Press `Enter`

![pivpn23-ecdsacertsize](/content/images/2019/10/pivpn23-ecdsacertsize.png)

  
  
  
  

1. This screen will show your public IP address and ask to use the public DNS or your public IP. Select your public IP because PI-Hole settings will alter these settings

![PiVPN16](/content/images/2019/10/PiVPN16.jpg)

  
  
  
  

1. PiVPN wants to know the public DNS servers to use upstream. Select your preference and hit `Enter` while selecting **Ok**. _Note: I use DNSWatch_

![pivpn25-dnsprovider](/content/images/2019/10/pivpn25-dnsprovider.png)

  
  
  
  

1. This is asking to add your own domain. I have none for this purpose so I select **No**

![pivpn26-customersearchdomain-SWITCHTONO](/content/images/2019/10/pivpn26-customersearchdomain-SWITCHTONO.png)

  
  
  
  

1. Then, PiVPN will give a few tips on how to use PiVPN and add ovpn profiles, press `Enter`

![pivpn27-installcomplete](/content/images/2019/10/pivpn27-installcomplete.png)

  
  
  
  

1. It will ask to reboot. Select **Yes** and click `Enter`. Your RPi will now be boot and have PiVPN installed!

![pivpn28-reboot-SWITCHTOYES](/content/images/2019/10/pivpn28-reboot-SWITCHTOYES.png)

  
  
<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->  

## Pi-Hole Setup
  
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Visual Guide

1. Open a Terminal window

![vpn8-terminalopen](/content/images/2019/10/vpn8-terminalopen.png)

  
  
  
  

1. Enter the following command, per the Pi-Hole website:

`curl -sSL https://install.pi-hole.net | bash`

  

**Note** : _Piping to bash_ (`| bash`) _will run the install automatically. Simply run the command with it to install download and then run (`curl -L https://install.pi-hole.net`)_  
 ![pivpn29-pi-hole](/content/images/2019/10/pivpn29-pi-hole.png)

  
  
  
  

1. The installer starts with a donation page to support the application and author

![pivpn30-donatepihole](/content/images/2019/10/pivpn30-donatepihole.png)

  
  
  
  

1. The installer begins

![pivpn30-piholeinstaller](/content/images/2019/10/pivpn30-piholeinstaller.png)

  
  
  
  

1. As stated in the [SSH Setup](#sshsetup), the PiVPN and Pi-Hole servers need to be set to a static IP to run correctly. The installer will run through this first

![pivpn31-staticip](/content/images/2019/10/pivpn31-staticip.png)

  
  
  
  

1. Select the network interface you want the RPi to run on, if you're hardwired via Ethernet, you'll likely select **eth0**. Mine is on Wi-Fi so I will select **wlan0** and click **Ok**

![pivpn32-interface-SELECTWANFORWIFI](/content/images/2019/10/pivpn32-interface-SELECTWANFORWIFI.png)

  
  
  
  

1. Select the DNS provider you want to use for upstream DNS queries. I use **DNS.WATCH**

![pivpn33-upstreamdns](/content/images/2019/10/pivpn33-upstreamdns.png)

  
  
  
  

8.Pi-Hole uses public domain lists pulled in from various sources in order to block ads and known-bad domains. We will add **Phishing Army** to this later and you can add and remove them at ease. Leave all of them selected and select **Ok**

![pivpn34-3rdpartyadblockers](/content/images/2019/10/pivpn34-3rdpartyadblockers.png)

  
  
  
  

1. Then Pi-Hole wants to know whether to use IPv4 or IPv6. You'll likely want both, leave them selected and click **Ok**

![pivpn35-protocols](/content/images/2019/10/pivpn35-protocols.png)

  
  
  
  

1. The next screen is a warning about IP address conflicts if the RPi is not set to be a static IP, click `Enter`

![pivpn36-ipconflict](/content/images/2019/10/pivpn36-ipconflict.png)

  
  
  
  

1. This is the IPv4 address that Pi-Hole will use as the static IP and the gateway

![pi5](/content/images/2019/10/pi5.jpg)

  
  
  
  

1. Then it will show the IPv6 address it is using

![pi12](/content/images/2019/10/pi12.jpg)

  
  
  
  

1. The web admin interface is extremely useful for analytics on your Pi-Hole, keep this selected to **On** and continue

![pivpn38-webadminint](/content/images/2019/10/pivpn38-webadminint.png)

  
  
  
  

1. This step is a precoursor to the next step and only needs to be enabled if you plan to use the web admin interface. If you don't plan to, select **No** , however it is recommended that you do so

![pivpn39-webserver](/content/images/2019/10/pivpn39-webserver.png)

  
  
  
  

1. Again, for security and analytic purposes, keep log queries **On**

![pivpn40-longqueries](/content/images/2019/10/pivpn40-longqueries.png)

  
  
  
  

1. Pi-Hole uses a 0-4 privacy level ranking system that is used to log specific type of network traffic, information on the privacy levels can be seen [here](https://docs.pi-hole.net/ftldns/privacylevels/). Select your level and continue.

![pivpn41-privacylevel](/content/images/2019/10/pivpn41-privacylevel.png)

  
  
  
  

1. The installation is complete from this stage and it will display your information tthat was set throughout the installer

![pi17](/content/images/2019/10/pi17.jpg)

  
  
  
  

1. Navigate to [pi.hole/admin](pi.hole/admin) to go to the web interface for Pi-Hole. This is only possible if you enabled it in step 13

![pivpn43-pihole-admin](/content/images/2019/10/pivpn43-pihole-admin.png)

  
  
<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->  

## Pi-Hole Domain Feed Configuration
  
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->  

### Adding public lists to Pi-Hole (Phishing Army)
  
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
1. The file containing the block lists that Pi-Hole pulls from is `adlists.list` located at `etc/pihole/adlists.list`. Open that file using your preferred editor

![pivpn46-adlistsupdate](/content/images/2019/10/pivpn46-adlistsupdate.png)

  
  
  
  

1. The list of URLs that contain these third-party lists are revealed. Go to the bottom of the list and add `Phishing Army`'s public extended domain list. The list is located at: `https://phishing.army/download/phishing_army_blocklist_extended.txt`. Save and exit

![pivpn47-adlists-lists](/content/images/2019/10/pivpn47-adlists-lists.png)

  

![pivpn48-updatewithphishingarmy](/content/images/2019/10/pivpn48-updatewithphishingarmy.png)

  
  
  
  

1. To manually pull the domain feeds into Pi-Hole, and with **Phishing Army** freshly added, run the command `pihole -g`

![pivpn49-piholeg](/content/images/2019/10/pivpn49-piholeg.png)

  
  
  
  

1. As you can see above, all of the feeds were pulled in correctly and **Phishing Army** was as well

![pivpn49-phishingarmycheckfinish](/content/images/2019/10/pivpn49-phishingarmycheckfinish.png)

  
  
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->  

### Pi-Hole Cron Job Change (Weekly to Daily)
  
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
1. Using your favorite editor, open the pihole cron job file at `etc/cron.d/pihole`

![pivpn44-updatepiholetoupdatedaily](/content/images/2019/10/pivpn44-updatepiholetoupdatedaily.png)

  
  
  
  

1. The cron job that updates the Pi-Hole feeds weekly is highlighted **AND ALREADY CHANGED TO THE CORRECT SETTING TO UPDATE NIGHTLY AT MIDNIGHT**. Change this cron job to update whenver you please, a cron job calculator is [here](https://crontab.guru)

![pivpn45-conjobpihole](/content/images/2019/10/pivpn45-conjobpihole.png)

  
  
  
  
<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->
# Thank You!
  

I hope this helped solve some issues you were having with setting up SSH, PiVPN, Pi-Hole, and adding lists to Pi-Hole. If you have any questions [Contact](https://ryanestes.ghost.io/contact/) me via email with any concerns.

<!--kg-card-end: markdown-->
* * *
