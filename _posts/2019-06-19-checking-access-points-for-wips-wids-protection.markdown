---
layout: post
title: Checking Access Points For WIPS/WIDS Protection From Evil Twin Attacks
date: '2019-06-19 09:08:00'
tags:
- hacking
- how-to
- wifi-pineapple
- wifi-hacking
- wireless
- wifi
- wireless-hacking
- twe
- trusted-wireless-environment
---

The premier defense for rogue access points in a wireless network is the implementation of a Wireless Intrusion Prevention System (WIPS) or Wireless Intrusion Detection System (WIDS). A quick WIPS/WIDS implementation check can be performed on any access point with a WiFi Pineapple Nano handy. This proof-of-concept will show how to check open access points for WIPS/WIDS implementation by using a WiFi Pineapple Nano. This check is both safe and legal and is a good starting point to test the WiFi Pineapple functionality and an access point for **ONE** of the **SIX** [Trusted Wireless Environment](https://www.trustedwirelessenvironment.com/) common hacks - "Evil Twin" Access Points

<!--kg-card-begin: markdown-->

_Note: In this tutorial I will filter my MAC address so only my own device can connect with my WiFi Pineapple. This proof-of-concept is performed completely with my own devices. I do not condone using this information as part of any malicious act._

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
### Requirements

- A device capable of browsing the Internet
- A configured WiFi Pineapple ([Configuration Help](/how-to-set-up-wifi-pineapple-nano-on-windows/))
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Straight To It

1. Open your Wi-Fi menu and seek an SSID to spoof. Remember the SSID name must be EXACTLY the same for this test to work
2. Open an Internet browser and browser to your WiFi Pineapple's dashboard; typically [http://172.16.42.1:1471](http://172.16.42.1:1471)
3. Go to the **Filters** tab
4. Ensure that both **Client Filtering** and **SSID Filtering** have the filtering set to **Allow Listed MAC(s)** and **Allow Listed SSID(s)** respectively
5. Type in the MAC address of the device you're going to connect to the WiFi Pineapple; your victim device, and click **Add**. The MAC Address should appear above in the filtering menu
6. Type in the SSID of the AP name you are spoofing EXACTLY as it is written and click **Add**. The SSID should appear above in the filtering menu
7. Go to the **Networking** tab in the left navigation menu
8. Change the **Open SSID** field to the name of the SSID you are spoofing from _Step 1_
9. Uncheck the **Hide Open SSID** checkbox
10. Click the **Update Access Points**. A prompt with green text should appear below saying the update was successful and the radios are going to restart
11. Now, go to your victim device (An Android Phone in my case) and intentionally connect to your WiFi Pineapple. You can check you've connected to the WiFi Pineapple and not the AP by going into the options of your Wi-Fi connection and checking to see if the IP Address is on the same subnet as your WiFi Pineapple ( **172.16.42.x** )
12. If the connection remains for about 1 minute or more you can be pretty certain the AP you are testing doesn't have WIDS/WIPS implementation, or have a misconfigured implementation. You can start a timer when connected to get a better idea

Thats it! See below for a visual guide

#### Visual Guide

1. Open your Wi-Fi menu and seek an SSID to spoof. Remember the SSID name must be EXACTLY the same for this test to work. In my case the SSID is **Test\_Router\_RE**

![1-wipds](/assets/images/07/1-wipds.png)






1. Open an Internet browser and browser to your WiFi Pineapple's dashboard; typically [http://172.16.42.1:1471](http://172.16.42.1:1471)





1. Go to the **Filters** tab

![1-filter](/assets/images/07/1-filter.png)






1. Ensure that both **Client Filtering** and **SSID Filtering** have the filtering set to **Allow Listed MAC(s)** and **Allow Listed SSID(s)** respectively

![2-AllowListed](/assets/images/07/2-AllowListed.png)






1. Type in the MAC address of the device you're going to connect to the WiFi Pineapple; your victim device, and click **Add**. The MAC Address should appear above in the filtering menu

![3-ClientFilter](/assets/images/07/3-ClientFilter.png)






1. Type in the SSID of the AP name you are spoofing EXACTLY as it is written and click **Add**. The SSID should appear above in the filtering menu

![4-SSIDFilter](/assets/images/07/4-SSIDFilter.png)






1. Go to the **Networking** tab in the left navigation menu

![6-Networking](/assets/images/07/6-Networking.png)






1. Change the **Open SSID** field to the name of the SSID you are spoofing from _Step 1_





1. Uncheck the **Hide Open SSID** checkbox





1. Click the **Update Access Points**. A prompt with green text should appear below saying the update was successful and the radios are going to restart

![7-SSIDChangeAndUpdate](/assets/images/07/7-SSIDChangeAndUpdate.png)






1. Now, go to your victim device (An Android Phone in my case) and intentionally connect to your WiFi Pineapple. You can check you've connected to the WiFi Pineapple and not the AP by going into the options of your Wi-Fi connection and checking to see if the IP Address is on the same subnet as your WiFi Pineapple ( **172.16.42.x** )

![Final-WIPDS](/assets/images/07/Final-WIPDS.png)






1. If the connection remains for about 1 minute or more you can be pretty certain the AP you are testing doesn't have WIDS/WIPS implementation, or have a misconfigured implementation. You can start a timer when connected to get a better idea




<!--kg-card-end: markdown-->
