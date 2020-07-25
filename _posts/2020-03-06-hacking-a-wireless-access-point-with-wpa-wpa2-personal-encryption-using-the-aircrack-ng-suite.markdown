---
layout: post
title: Hacking a Wireless Access Point (Router) with WPA/WPA2 Personal Encryption
  using the Aircrack-ng Suite
featured: true
date: '2020-03-06 03:00:11'
tags:
- hacking
- penetration-testing
- kali-linux
- linux
- wifi
- wifi-hacking
- wireless
- wireless-hacking
---

## Introduction
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### WPA

After WEP encryption was introduced with the ratification of the IEEE 802.11 standard in 1997, it was quickly discovered to be vulnerable to a myriad of exploits. As such, the Wi-Fi Alliance, in conjunction with the IEEE, adopted a quick fix for this increasingly risky encryption mechanism - WPA (Wi-Fi Protected Access) - in 2003. WPA sought to implement fixes for major flaws that were exposed in WEP with the most important change being the adoption of the new security protocol, TKIP (Temporal Key Integrity Protocol). TKIP introduced a few major improvements over WEP, including:

- Implementation of a packet sequencer so out-of-order packets are rejected
- Mixes root keys with IVs on a key-by-key basis instead of appending root key with IV
- Stronger data assurance than the Cyclic Redundancy Check (CRC) from WEP with the introduction of a 64-bit MIC (Message Integrity Check)

TKIP provided much needed security for an increasingly vulnerable wireless world back in those days. [Hacking WEP encryption](/hacking-a-wep-encrypted-wireless-access-point-using-the-aircrack-ng-suite/) was becoming tooled, weaponized, and unfortunately, trivial before WPA replaced it. However, since WPA was a temporary solution, it still used WEP's RC4 stream cipher. The Wi-Fi Alliance quickly enhanced WPA a year after it's public reveal with the introduction of WPA2 to combat additional possible vulnerabilities, but it wasn't enough.

#### WPA2

The Wi-Fi Alliance quickly pushed out WPA to quickly fix the vulnerabilities of WEP, but the Wi-Fi Alliance had a true Wi-Fi security standard in the works. In 2004, the Wi-Fi Alliance and IEEE released the 802.11i standard. So, WPA was a quick fix to WEP that essentially introduced TKIP overlayed onto RC4. WPA2's most important features are:

- Introduction of AES encryption opposed to the RC4 cipher
- Introduction of the CCM mode Protocol (CCMP) to replace TKIP (allows for TKIP for backward compatibility)
- Most importantly, it uses a 4-way handshake for authentication

##### The WPA2 4-Way Handshake

The two figures below were taken from the [Clear To Send Podcast](cleartosend.net) and describe the 4-way handshake:

![4-way-1](/content/images/2020/03/4-way-1.png)

![4-way-2](/content/images/2020/03/4-way-2.png)

Lastly, there are two main modes of WPA/WPA2 - Personal and Enterprise. Personal is the typical hexadecimal or alphanumeric passphrase. Enterprise uses the router as an authenticating controller in front of an authenticating server, usually a RADIUS server; but Enterprise is out of scope for this post. This post will cover how to crack WPA/WPA2 personal encrypted Wi-Fi networks. To do this, we will capture the 4-way handshake with Aircrack-ng and brute force the passphrase by presenting the 4-way handshake for each passphrase attempt. Let's get started with the proof of concept. It is far simpler than WEP, thankfully.

Note: As of this writing, some access points offer the WPA/WPA2 TKIP/AES "mixed-mode" option. This allows for Wi-Fi devices to be backwards compatible and interoperable without extra hardware.

<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->

_Disclaimer: This post is meant for educational purposes only and any information obtained sholuld not be used for malicious purposes. I will not be responsible for any damage, harm, or legal action derived from any information within this post._

<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->
## Proof of Concept
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

_If you need help with a Wi-Fi penetration testing Setup for these attacks, I've written a short post about that [HERE](/setting-up-a-new-wi-fi-hacking-setup/)_

_These attacks use the Aircrack-ng suite_

For this proof-of-concept, I am using the following software/hardware:

- Laptop running Windows 10
- Alfa AWUS036NHA Wireless Adapter
- D-Link DIR-615 Wireless N 300 Router
- Virtualbox Version 6.1.4
- Kali Linux 2020.1
- Aircrack-ng 1.5.2 (comes with Kali Linux)
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
### The Attack
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

As of this writing, there has been quite a few vulnerabilities discovered from WPA/WPA2 networks. The typical deauth attack still exists; the [KRACK attack](https://www.krackattacks.com/) was discovered in 2017; [Bettercap](https://www.bettercap.org/) assisted with the [PMKID attack](https://www.evilsocket.net/2019/02/13/Pwning-WiFi-networks-with-bettercap-and-the-PMKID-client-less-attack/) beginning around early 2019; packets can be spoofed; and finally, weak passphrases can be implemented by admins which brings us to the attack in this post: a password brute-force attack. In this attack I use the Aircrack-ng suite with a Kali Linux VM to capture the 4-way handshake of a router I own. Then, Aircrack-ng is able to present the handshake and attempt a password try, multiple times a second. If the password is weak on the router, we are able to crack it with Aircrack-ng and be provided access to the network. Depending on if they have brute-force security measures and/or proper network segmentation. This proof of concept was done in my SOHO with my own router and devices, as listed above.

The first step of the attack is to first choose or be given an access point with WPA/WPA2 encryption to exploit. You can find this information with 'airodump-ng'. A small guide on how to do that is here: [https://ryandinho.me/hacking-a-wep-encrypted-wireless-access-point-using-the-aircrack-ng-suite/#discoveringvictimroutereasily](/hacking-a-wep-encrypted-wireless-access-point-using-the-aircrack-ng-suite/#discoveringvictimroutereasily). The attack also assumes your wireless adapter is capable of packet injection and promiscuous mode. Another guide on how to do that is here: [https://ryandinho.me/hacking-a-wep-encrypted-wireless-access-point-using-the-aircrack-ng-suite/#injectiontest](/hacking-a-wep-encrypted-wireless-access-point-using-the-aircrack-ng-suite/#injectiontest)

**START**

- 

Find out the name of your wireless card interface using airmon-ng:

`airmon-ng`

![final-wpa-1](/content/images/2020/03/final-wpa-1.png)

The interface name is "wlan0"

- 

Put your wireless card in monitor mode ON THE SAME CHANNEL AS THE VICTIM AP (THIS IS A MUST):

'airmon-ng start wlan0 11'

![final-wpa-2](/content/images/2020/03/final-wpa-2.png)

The channel number goes at the end of the command, highlighted above.

- 

Use airmon-ng again to ensure the interface name has been changed:

`airmon-ng`

![final-wpa-3](/content/images/2020/03/final-wpa-3.png)

It is "wlan0mon".

- 

Perform a packet capture of the victim router and output it to a file using airodump-ng:

`airodump-ng -c 11 -d 00:18:E7:EA:28:87 -w WPA-WPA2-Output wlan0mon`

![wpa-2](/content/images/2020/03/wpa-2.png)

    -c: The channel to filter on (11)
    -d: The MAC address of the victim router (00:18:E7:EA:28:87)
    -w: the filename to output the pcap to (WPA-WPA2-Output)

The following window should appear but with your specifications:

![wpa-3](/content/images/2020/03/wpa-3.png)

**KEEP THIS WINDOW RUNNING TO WAIT FOR THE 4-WAY HANDSHAKE!!!**

- 

The first step is to capture the 4-way handshake. To do this we will deauthenticate a client using the [deauthentication attack](/hacking-a-wep-encrypted-wireless-access-point-using-the-aircrack-ng-suite/#deauthentication) and capture the handshake when they reauthenticate:

`aireplay -0 1 -a 00:18:E7:EA:28:87 -c 00:04:4B:59:10:88 wlan0mon`

![wpa-4](/content/images/2020/03/wpa-4.png)

Pictured above is the output of a successful deauthentication attack against the victim router, of a victim client. The client I deauthenticated was an Android tablet I had. The picture below shows the output of the airodump-ng menu when the client is deauthenticated and the 4-way handshake is subsuqeuently captured. The highlighted box shows the output of a successful handshake capture.

![final-wpa-7](/content/images/2020/03/final-wpa-7.png)

Once the handshake is captured we can begin the brute force attack. For this attack we will use a wordlist that comes with Kali Linux on the cap file.

- 

This final step uses aircrack-ng to brute force the password on the router:

`aircrack-ng -w ../usr/share/wordlists/rockyou.txt WPA-WPA2-Output-01.cap`

![wpa-6](/content/images/2020/03/wpa-6.png)

    -w: the wordlist file path (../usr/share/wordlists/rockyou.txt) or (path/to/file)

- Finally, below is the output of a successful key capture on the cap file

![final-wpa-9](/content/images/2020/03/final-wpa-9.png)

Notice that the attack took 48 minutes and 54 seconds. This isn't particularly unusual so be prepared for that. However, this depends on your machine and wordlist file size you use. I am on a VM itterating through a massive text file.

If there are any questions, concerns, or errors in the post feel free to contact me through email or in the comments below. Thanks!

<!--kg-card-end: markdown-->