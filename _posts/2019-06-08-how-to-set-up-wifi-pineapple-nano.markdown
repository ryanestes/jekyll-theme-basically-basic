---
layout: post
title: How To Set Up A WiFi Pineapple Nano
featured: true
date: '2019-06-08 17:34:00'
tags:
- wifi
- hacking
- wifi-hacking
- wireless
- wireless-hacking
- how-to
- windows
- mac
- linux
- wifi-pineapple
- android
---

The WiFi Pineapple has become ubiquitous within the cyber security community and network industry professionals alike. The low price tag, easy to use PineAP GUI, and mobility have shown that [Hak5](https://shop.hak5.org/) have made a product to genuinely assist with wireless security assessments. This post was originally used to reference the setup process or for those who have a dusty WiFi Pineapple sitting around, or anyone looking for help.



<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->

[WiFi Pineapple Nano Setup for Windows](#wifipineapplenanosetupforwindows)  
[WiFi Pineapple Nano Setup for macOS](#wifipineapplenanosetupformacos)  
[WiFi Pineapple Nano Setup for Linux](#wifipineapplenanosetupforlinux)  
[WiFi Pineapple Nano Setup for Android](#wifipineapplenanosetupforandroid)

<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->  


## WiFi Pineapple Nano Setup for Windows

_This proof of concept was created using Windows 10_


<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Straight To It

1. Plug in the WiFi Pineapple into an available USB slot using the supplied USB Y Cable or any USB that meets the [WiFi Pineapple power specifications](https://docs.hak5.org/hc/en-us/articles/360011238494-Specifications-and-Power-Considerations)
2. Navigate to **Control Panel -\> Network and Internet -\> Network and Sharing Center -\> Change adapter settings**
3. Highlight the WiFi Pineapple Adapter and press **F2** to change it to a name you can recognize _(e.g. Pineapple)_

_Note: The WiFi Pineapple Nano Adapter will have an **ASIX AX88772A USB2.0 to Fast Ethernet Adapter** chipset description_

1. **Right-click** the WiFi Pineapple adapter and select **Properties**
2. In the _This connection uses the following items:_ scroll-menu, highlight the **Internet Protocol Version 4 (TCP/IPv4)** and press the Properties button
3. Set a static IP address for the WiFi Pineapple by selecting the _Use the following IP address_ radio button
4. Set the IP address to **172.16.42.42** or any address that fits your network
5. If you don't know networking concepts comfortably, leave the _Subnet mask:_ and _Default gateway:_ fields alone; the default values are **255.255.255.0** for the _Subnet mask:_ and leave _Default gateway:_ blank. Click **OK -\> Close**
6. Next, **right-click** the adapter which currently has Internet access and select **Properties**. This will be the adapter you are using to bridge to your WiFi Pineapple, providing it with Internet access
7. In the top of the modal the pops up, select the **Sharing** tab
8. Checkmark the _Allow other network users to connect through this computer's Internet connection_
9. Select the adapter from the drop-down list which you named in step 3 and hit **OK**
10. Navigate to **172.16.42.42:1471** or whatever IP address maps to the IP address you set in step 7, ensure the port is 1471
11. Use the on-screen instructions to set up the WiFi Pineapple
12. Click the **Load Bulletins from WiFiPineapple.com** button on the Dashboard, if bulletins successfully load you're all ready to go!



#### Visual Guide

1. Plug in the WiFi Pineapple into an available USB slot using the supplied USB Y Cable or any USB that meets the [WiFi Pineapple power specifications](https://docs.hak5.org/hc/en-us/articles/360011238494-Specifications-and-Power-Considerations)

![IMG_3443](/assets/images/06/IMG_3443.jpg)






1. In the bottom left of the Desktop, click the _Type here to search_ text field and navigate to the Control Panel by searching for it.

![ControlPanelSearch-2](/assets/images/06/ControlPanelSearch-2.png)






1. Navigate to **Network and Internet -\> Network and Sharing Center -\> Change adapter settings**

![NetworkandInternetPicture-2](/assets/images/06/NetworkandInternetPicture-2.png)

![NetworkandSharingCenterPicture-2](/assets/images/06/NetworkandSharingCenterPicture-2.png)

![changeadaptersettings_censored](/assets/images/06/changeadaptersettings_censored.png)






1. Highlight the WiFi Pineapple Adapter and press **F2** to change it to a name you can recognize and press **Enter** _(e.g. Pineapple)_

_Note: The WiFi Pineapple Nano Adapter will have an **ASIX AX88772A USB2.0 to Fast Ethernet Adapter chipset description** _

![Ethernet3_censored](/assets/images/06/Ethernet3_censored.png)

![f2changename_censored](/assets/images/06/f2changename_censored.png)






1. **Right-click** the same Pineapple adapter and select **Properties** from the drop-down menu

![pineappleproperties_censored](/assets/images/06/pineappleproperties_censored.png)






1. In the _This connection uses the following items:_ scroll-menu, highlight the **Internet Protocol Version 4 (TCP/IPv4)** and press the **Properties** button

![pineapplepropertiesipv4change-2](/assets/images/06/pineapplepropertiesipv4change-2.png)






1. Set a static IP address for the WiFi Pineapple by selecting the _Use the following IP address:_ radio button. Set the IP address to **172.16.42.42** (or any address that fits your network). If you don't know networking concepts comfortably, leave the _Subnet mask:_ and _Default gateway:_ fields alone; the default values are **255.255.255.0** for the Subnet mask: and leave Default gateway: blank. Click **OK -\> Close**

![172164242-2](/assets/images/06/172164242-2.png)  
 ![close-2](/assets/images/06/close-2.png)






1. Now, **right-click** the adapter which powers your power supply and select **Properties**. In my case it is my WiFi internal WiFi adapter connected to my home WiFi. I'm going to bridge that connection to my Pineapple

![ezgif.com-gif-maker](/assets/images/06/ezgif.com-gif-maker.png)






1. In the top of the modal that appears, select the **Sharing** tab

![sharingtab-2](/assets/images/06/sharingtab-2.png)






1. Checkmark the _Allow other network users to connect through this computer's Internet connection_ checkbox

![AllowOtherNetworksToShare-2](/assets/images/06/AllowOtherNetworksToShare-2.png)






1. Select the drop-down menu under _Home networking connection:_ and select the name of the adapter that is tied to your pineapple. See step 4 for reference. In my case it is **Pineapple**. Select **OK**

![EnsureLabelSelected-2](/assets/images/06/EnsureLabelSelected-2.png)






1. Open a browser and navigate to **172.16.42.1:1471** (or whichever IP address fits your network) to navigate to the administrative login on your Pineapple.

![172navigateurl-2](/assets/images/06/172navigateurl-2.png)






1. A Welcome modal should appear in the browser. Press the **Get Started** button

![getstarted-2](/assets/images/06/getstarted-2.png)






1. Upon setup, when this screen appears just tap the reset button on the bottom of your WiFi Pineapple to continue with WiFi disabled

![securesetup-2](/assets/images/06/securesetup-2.png)






1. After successful setup, the main dashboard should appear similar to below

![dashboard_loadbulletins-2](/assets/images/06/dashboard_loadbulletins-2.png)






1. Click the **Load Bulletins from WiFiPineapple.com** button on the Dashboard, if bulletins successfully load you're all ready to go!

![loaded_bulletins_complete-2](/assets/images/06/loaded_bulletins_complete-2.png)






#### [Try a simple MITM attack to get things started](https://ryanestes.ghost.io/checking-wips-wids-detection-with-the-wifi-pineapple/)

##### If you aren't seeing bulletins:

- Ensure you performed all steps correctly
- Use a search engine to find others with similar problems as yours
- [Contact](https://ryanestes.ghost.io/contact/) me via email with any concerns
<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->  


## WiFi Pineapple Nano Setup for macOS

_This proof of concept was created using macOS Mojave version 10.14.5_


<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Straight To It

1. Plug in the WiFi Pineapple into an available USB slot using the supplied USB Y Cable or any USB that meets the [WiFi Pineapple power specifications](https://docs.hak5.org/hc/en-us/articles/360011238494-Specifications-and-Power-Considerations)
2. Navigate to **(Apple Menu) -\> System Preferences -\> Network**
3. Ensure the WiFi Pineapple is connected and DHCP has assigned the **172.16.42.x** subnet by highlighting the adapter in the menu on the left-side of the menu. The IP Address should be **172.16.42.127** (or any number higher than 100) and the Router should have the default **172.16.42.1**

_Note: The WiFi Pineapple Nano Adapter will have an **AX88x72A** chipset description_

1. In order to allow for communication with the Wi-Fi Pineapple we must change the hardcoded DCHP subnet of the MAC to match the Wi-Fi Pineapple, or vice versa. To do this, open a Terminal window and ssh into the Wi-Fi Pineapple by typing:


`ssh root@172.16.42.1`



1. An RSA fingerprint prompt should appear if this is the first connection, type **yes** and then enter your root password (The one that logs you into the Wi-Fi Pineapple in the Web GUI)
2. To change the Wi-Fi Pineapple's default IP address and gateway type the following commands in the Terminal:


`uci set network.lan.ipaddr='192.168.2.10'`  
`uci set network.lan.gateway='192.168.2.1'`  
`uci commit && reboot`



_Kudos to the user audibleblink in the Hak5 forums_



1. The Wi-Fi Pineapple will reboot and you can now check the IP address and gateway were successfully changed in the **Network** menu again. If it's the 192.168.2.x values, you should be able to continue to the Internet connection sharing portion
2. Now, return to the **System Preferences** menu and select **Sharing**
3. Highlight the **Internet Sharing** checkbox in the left menu and Internet sharing information should display to the right
4. Select the **Share your connection from:** dropdown menu and select the adapter that is providing Internet access. In my case, **Wi-Fi**
5. From the **To computers using:** menu, select the WiFi Pineapple adapter. In my case the adapter is named **AX88x72A**
6. Select the checkbox next to Internet Sharing in the left menu and select **Start**
7. Navigate to **192.168.2.10:1471** or whatever IP address maps to the IP address you set in _step 6_, ensure the port is **1471**
8. Use the on-screen instructions to set up the WiFi Pineapple
9. Click the **Load Bulletins from WiFiPineapple.com** button on the Dashboard, if bulletins successfully load you're all ready to go!



#### Visual Guide

1. Plug in the WiFi Pineapple into an available USB slot using the supplied USB Y Cable or any USB that meets the [WiFi Pineapple power specifications](https://docs.hak5.org/hc/en-us/articles/360011238494-Specifications-and-Power-Considerations)

![IMG_3626](/content/images/2019/07/IMG_3626.jpg)






1. Navigate to **(Apple Menu) -\> System Preferences -\> Network**

![1](/content/images/2019/07/1.JPG)  
 ![2](/content/images/2019/07/2.JPG)






1. Ensure the WiFi Pineapple is connected and DHCP has assigned the **172.16.42.x** subnet by highlighting the adapter in the menu on the left-side of the menu. The IP Address should be **172.16.42.127** (or any number higher than 100) and the Router should have the default **172.16.42.1**

_Note: The WiFi Pineapple Nano Adapter will have an **AX88x72A** chipset description_

![3](/content/images/2019/07/3.JPG)






1. In order to allow for communication with the Wi-Fi Pineapple we must change the hardcoded DCHP subnet of the MAC to match the Wi-Fi Pineapple, or vice versa. However, changing the WiFi Pineapple instead of the Apple device is the easier and preferred method. To do this, open a Terminal window and ssh into the Wi-Fi Pineapple by typing:


`ssh root@172.16.42.1`



![censor1](/content/images/2019/07/censor1.jpg)



_Note: An RSA fingerprint prompt should appear if this is the first connection, type **yes** and then enter your root password (The one that logs you into the Wi-Fi Pineapple in the Web GUI)_






1. To change the Wi-Fi Pineapple's default IP address and gateway type the following commands in the Terminal:


`uci set network.lan.ipaddr='192.168.2.10'`  
`uci set network.lan.gateway='192.168.2.1'`  
`uci commit && reboot`



_Kudos to the user audibleblink in the Hak5 forums_



![censor2](/content/images/2019/07/censor2.jpg)






1. The Wi-Fi Pineapple will reboot and you can now check the IP address and gateway were successfully changed in the **Network** menu again. If it's the 192.168.2.x values, you should be able to continue to the Internet connection sharing portion

![11-pre](/content/images/2019/07/11-pre.JPG)






1. Now, return to the **System Preferences** menu and select **Sharing**

![4](/content/images/2019/07/4.JPG)






1. Highlight the **Internet Sharing** checkbox in the left menu and Internet sharing information should display to the right. Select the **Share your connection from:** dropdown menu and select the adapter that is providing Internet access. In my case, **Wi-Fi**. From the **To computers using:** menu, select the WiFi Pineapple adapter. In my case the adapter is named **AX88x72A**

![5-censored](/content/images/2019/07/5-censored.jpg)






1. Select the checkbox next to Internet Sharing in the left menu and select **Start** and ensure it remains checked after clicking **Start**.

![7](/content/images/2019/07/7.JPG)  
 ![6](/content/images/2019/07/6.JPG)






1. Navigate to **192.168.2.10:1471** or whatever IP address maps to the IP address you set in _step 6_, ensure the port is **1471** and you will be met with the Welcome screen. Use the on-screen instructions to set up the WiFi Pineapple

![8-pre](/content/images/2019/07/8-pre.JPG)






1. Click the **Load Bulletins from WiFiPineapple.com** button on the Dashboard, if bulletins successfully load you're all ready to go!

![13](/content/images/2019/07/13.JPG)






#### [Try a simple MITM attack to get things started](https://ryanestes.ghost.io/checking-wips-wids-detection-with-the-wifi-pineapple/)

##### If you aren't seeing bulletins:

- Ensure you performed all steps correctly
- Use a search engine to find others with similar problems as yours
- [Contact](https://ryanestes.ghost.io/contact/) me via email with any concerns
<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->
## WiFi Pineapple Nano Setup for Linux
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

under construction

<!--kg-card-end: markdown-->
* * *
<!--kg-card-begin: markdown-->
## WiFi Pineapple Nano Setup for Android

_This proof of concept was created using a Nokia 6.1 running Android 9 "Pie" (Android One)_

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Straight To It

1. Connect the charging cord to your Android device and plug the USB end into the female USB insertion on the WiFi Pineapple. Then, Plug the female USB of the y-cord into the WiFi Pineapple and plug either male USB into a power source such as a computer, battery, or wall outlet
2. On your Android device, go the **Play Store**
3. Search for WiFi Pineapple and download the **WiFi Pineapple Connector** App
4. Open the **WiFi Pineapple Connector** App and a modal should appear prompting for _USB Tethering Required_. Click **No** \*, that you don't have it required (If you do already click **Yes** )
5. The **Tethering & portable hotspot** menu should appear. Click the slider on the right next to the **USB tethering** option to enable USB tethering to the WiFi Pineapple
6. Click the _Back_ button on the Android device to return to the **WiFi Pineapple Connector** App. Now click **Yes** that you have now enabled USB tethering
7. After a few seconds of detecting the WiFi Pineapple, the app should open a web browser and navigate to whatever IP address the DHCP provided on your internal network with the port of **1471**. In my case this was **192.168.42.235:1471**
8. Follow the on screen instructions to set up the WiFi Pineapple completely, otherwise, login!
9. If your android device is connected to the Internet you should be able to immediately load bulletins and be ready to go



#### Visual Guide

1. Plug in the WiFi Pineapple into an available USB slot using the supplied USB Y Cable or any USB that meets the [WiFi Pineapple power specifications](https://docs.hak5.org/hc/en-us/articles/360011238494-Specifications-and-Power-Considerations). Connect the charging cord to your Android device and plug the USB end into the female USB insertion on the WiFi Pineapple

![android-wifi-0](/content/images/2019/08/android-wifi-0.jpeg)






1. On your Android device, go the **Play Store** and search for _WiFi Pineapple Connector_ and download the **WiFi Pineapple Connector** App

![android-wifi-1](/content/images/2019/08/android-wifi-1.png)  
 ![android-wifi-2](/content/images/2019/08/android-wifi-2.png)






1. Open the **WiFi Pineapple Connector** App and a modal should appear prompting for _USB Tethering Required_. Click **No** , that you don't have it enabled (If you do already click **Yes** )

![android-wifi-3](/content/images/2019/08/android-wifi-3.png)






1. The **Tethering & portable hotspot** menu should appear. Click the slider on the right, next to the **USB tethering** option to enable USB tethering to the WiFi Pineapple

![android-wifi-4](/content/images/2019/08/android-wifi-4.png)  
 ![android-wifi-5](/content/images/2019/08/android-wifi-5.png)






1. Click the _Back_ button on the Android device to return to the **WiFi Pineapple Connector** App. Now click **Yes** that you have now enabled USB tethering

![android-wifi-v2-1-1](/content/images/2019/08/android-wifi-v2-1-1.png)






1. After a few seconds of detecting the WiFi Pineapple, the app should open a web browser and navigate to whatever IP address the DHCP provided on your internal network with the port of **1471**. In my case this was **192.168.42.235:1471**. Follow the on screen instructions to set up the WiFi Pineapple completely, otherwise, login!

![android-wifi-6](/content/images/2019/08/android-wifi-6.png)






1. If your android device is connected to the Internet you should be able to immediately load bulletins and be ready to go

![android-wifi-7](/content/images/2019/08/android-wifi-7.png)






#### [Try a simple MITM attack to get things started](https://ryanestes.ghost.io/checking-wips-wids-detection-with-the-wifi-pineapple/)

##### If you aren't seeing bulletins:

- Ensure you performed all steps correctly
- Use a search engine to find others with similar problems as yours
- [Contact](https://ryanestes.ghost.io/contact/) me via email with any concerns
<!--kg-card-end: markdown-->
* * *

* * *
