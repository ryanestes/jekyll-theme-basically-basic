---
layout: post
title: WiFu and OSWP Certification Review
date: '2019-05-26 17:32:00'
excerpt_separator: <!--more-->
tags:
- certifications
- hacking
- reviews
- wifi
- wifi-hacking
- wireless
- wireless-hacking
---

On May 10th, 2019, I successfully attempted and passed the Offensive Security Wireless Professional (OSWP) exam. In this post I will talk about the preliminary Offensive Security Wireless Attacks with Kali (WiFu) course, as well as my thoughts on the OSWP exam.
<!--more-->
## Who Should Take This Course

According to Offensive Security, the WiFu course and OSWP certification is “designed for information security professionals who want to take a serious and meaningful step into the world of wireless penetration testing.” This includes “Security Professionals & Enthusiasts” and “Network Administrators”, according to Offensive Security.

After completion of the course content and the preceding exam, I agree the exam is directed towards network and security enthusiasts eager to learn more about the 802.11 standard and cracking their encryption. However, what also interested me in the OSWP was the price and introduction into Offensive Security courses and exams which is easiest achieved with WiFu/OSWP.

OSWP is by far the most affordable certification Offensive Security Offers, excluding the KLCP. Albeit, the KLCP is the same price, the multiple-choice-only exam doesn't fully portray the lab environments in all of their other certification exams. The chart below illustrates the price differences:

* * *
<!--kg-card-begin: markdown-->

| Course | Certification | Cost |
| --- | --- | --- |
| Kali Linux Revealed | Kali Linux Certified Professional (KLCP) | $450 |
| **Offensive Security Wireless Attacks with Kali (WiFu)** | **Offensive Security Wireless Professional (OSWP)** | **$450** |
| Penetration Testing with Kali Linux (PwK) | Offensive Security Certified Professional (OSCP) | $800+ |
| Cracking the Perimeter (CTP) | Offensive Security Certified Expert (OSCE) | $1,200+ |
| Advanced Web Attacks and Exploitation (AWAE) | Offensive Security Certified Professional (OSCP) | $1,400+ |
| Advanced Windows Exploitation (AWE) | Offensive Security Exploitation Expert (OSEE) | ~$5,000+ |

<!--kg-card-end: markdown-->
* * *

**_Note:_** _ **AWE/OSEE cost is based on live training offerings through Black Hat USA 2018 and prior.** _

## Enrollment Process

The enrollment process is straightforward. As of this writing the fee for the course materials and an exam attempt is $450 USD. Upon enrollment and payment, Offensive Security will send several emails to keep you up to date on the process of enrollment. Typically, enrollment, payment, and processing takes a few days so don’t expect to enroll and get started the same day.

<!--kg-card-begin: markdown-->

![Enrollment Screenshot](/content/images/2019/06/OSWP_Enrollment_pic.png)

_The enrollment and one time fee includes all of the educational content and an exam attempt._

<!--kg-card-end: markdown-->
## WiFu
<!--kg-card-begin: markdown-->

The Offensive Security Wireless Attacks (WiFu) course covers every aspect you need to know in order to successfully pass the OSWP exam. There's a reason the course materials are bundled with the exam attempt above. That's a testament to how easy the course is to both enroll and learn course material.

Offensive Security did the honor of providing the course syllabus in it's entirety which gives a good idea on what the OSWP exam could entail. The syllabus can be found here: [WiFu Syllabus](https://www.offensive-security.com/documentation/wifu-syllabus.pdf)

Within the syllabus I want to highlight some important concepts and some things to consider. First, and most importantly, there are hardware requirements within the course prerequisites. **You must have a compatible wireless card/adapter and compatible router for the course!** Offensive Security provides recommendations for hardware:

![hardware_specs_oswp](/content/images/2019/06/hardware_specs_oswp.png)

The hardware is a bit outdated so I used similar models of the products I could find on Amazon. A small table shows:

| | Router | Wireless Card |
| --- | --- | --- |
| Recommended: | D-Link DIR-601 **OR** Netgear WNR1000v2 | Netgear WN111v2 USB **OR** ALFA Networks AWUS036H USB 500mW |
| I Used: | [D-Link DIR-615](https://www.amazon.com/D-Link-DIR-615-Wireless-N-Router-4-Port/dp/B000QD7B6W) | [Alfa AWUS036NHA](https://www.amazon.com/Alfa-AWUS036NHA-Wireless-USB-Adaptor/dp/B004Y6MIXS/ref=pd_lpo_sbs_147_t_1?_encoding=UTF8&psc=1&refRID=33T8YXZB52A00PDN1F2H) |

Additionally, an ISO for BackTrack 5 is provided, but BackTrack was superseded by Kali Linux in March of 2013. **KALI WORKED PERFECTLY FOR THESE EXERCISES. I USED VERSION 2019.1a**

Rather than regurgitating the syllabus and course overview, I will discuss what WiFu does well and where it can improve. To begin, WiFu is coauthered by Thomas d’Otreppe de Bouvette, the author of the most widely used WiFi hacking toolkit that exists today, the Aircrack-ng suite of tools. This is the blueprint for how most of the attacks are carried out within this course. A quick look at the course outline in the syllabus shows that the course discusses:

- the 802.11 standard
- how packets are designed
- how to configure and troubleshoot hardware and software
- Aircrack-ng ins and outs
- How to perform the attacks with a few other tools  
The WiFu course does a great job of explaining how to perform the attacks as well as enough background information to understand how and why things happen. Furthermore, you'll understand how some Aircrack-ng attacks can be performed via a CLI only.

It is hard to come up with cons about my experiences with the course. Many people harp on how some content is outdated, for example how much WEP content overshadows the WPA/WPA2 content. Although this it true, it isn't necesarily at the fault of the authors. WiFi security hasn't really progressed much in terms of encryption. WEP also has more granular flaws than WPA/WPA2. Essentially, at a high-level, WEP has various vulnerabilities within the crpytographic alrogithms themsevles, whereas WPA/WPA2 really only has a brute-force attack with a mapped 4-way handshake. These exclude the recent [KRACK](https://www.krackattacks.com/) and [PMKID](https://www.bitcrack.net/the-pmkid-attack/) attacks recently discovered.

<!--kg-card-end: markdown-->
## OSWP
<!--kg-card-begin: markdown-->

The Offensive Security Wireless Professional (OSWP) exam is a 4-hour online exam where the user must SSH into the provided Offensive Security infrastructure. I can't go over specficis about the exam but I can attest the the WiFu course covers everything you need to know to successfully pass the exam. My experiences can help clear up some other confusions about the exam which I ran into.

Offensive Security will email you all of the SSH information at the exam time you scheduled your exam. That means that it is crucial that you understand how to SSH into their environment and get to work immediately. Also, Offensive Security provides a penetration test template to submit your answers on. **Make sure to take screenshots of your commands for the report!** Once the exam time is over, you can't go back and take more, access will be revoked based on the 4-hour time slot. I used [reenshot]{[https://getgreenshot.org/](https://getgreenshot.org/)} take screenshots.

According to the OSWP website, an OSWP holder can:

1. Conduct wireless information gathering.
2. Circumvent wireless network access restrictions.
3. Crack various WEP, WPA, and WPA2 implementations.
4. Implement transparent man-in-the-middle attacks.
5. Demonstrate their ability to perform under pressure.
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

Here is a timeline inforgraphic from initial enrollment to email verification of passing:

<!--kg-card-end: markdown--><figure class="kg-card kg-image-card"><img src="/content/images/2019/06/OSWP-Certification-Timeline.jpg" class="kg-image"></figure><!--kg-card-begin: markdown-->
## Conclusion

To wrap up, I'd say the OSWP certification and prerequisite WiFu course is not only a great way to learn how to crack WiFI networks and learn conceptual aspects of the 802.11 standard, but a great teaser on Offensive Security certifications and processes. I only studied for about 2 weeks total and passed my certification attempt on my first try. I plan to use this certification to jumpstart my wireless security research and to possibly attempt the Offensive Security Certified Professional (OSCP) in the near future.

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
#### Verify my OSWP via Acclaim
<!--kg-card-end: markdown--><!--kg-card-begin: html-->

<script type="text/javascript" async src="//cdn.youracclaim.com/assets/utilities/embed.js"></script><!--kg-card-end: html-->
* * *
