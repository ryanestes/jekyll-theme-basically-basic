---
layout: post
title: SMiShing Campaign Leverages USPS and Parcel Service Distrust
date: '2020-08-30 18:35:29'
tags:
- phishing
- SMiShing
- social engineering
- scam
---

Beginning the week of August 23rd, a ![SMiShing](#smishing) campaign began to unfold that, by and large, impersonated large mail carrier and parcel services with the intention of stealing sensitive information from the victims. This post will explain the high-level tactics and technologies the attacker(s) used to send these SMiShes as well as several real-world text message examples that were attributed to this campaign, including myself. At the end of this post will be the list of known domains used in this campaign (tentative).

## Preliminary Information

SMiShing campaigns, and other similar ![social engineering](#socialengineering) attacks, often utilize current events and other psychological tricks to further coerce victims into divulging sensitive information. For example, I bet you have received an email, text, or instant message that claims you can lose 50 pounds fast and all you have to do to get a limited supply of their supplement is to click a link. Well, there are several psychological factors at play here, but there are two that stick out immediately:

1. The attacker assumes that the victim wants to lose weight or has body image issues. Considering about ![half of Americans say that they're trying to lose weight](https://time.com/5334532/weight-loss-americans/), this is an effective approach
2. The use of the words "limited supply" imply that the stock is low and the victim needs to react fast to get this supplement. This is a common tactic in social engineering that combines emotion with time-sensitive decisions.

The SMiShing campaign in this post impersonated common postal and parcel services in the United States such as USPS, UPS, FedEx, DHL, and Amazon. This is another effective industry to impersonate as the general public doesn't exact have much trust in these services. For starters, a ![report from Clutch](https://clutch.co/logistics/resources/package-theft-statistics-people-trust-ups-most-deliver-packages-safely) states that 29% of people trust UPS to deliver their package securely, the highest score of all 5 carriers listed (USPS 27%, Amazon 22%, FedEx 20%, DHL 2%). Not to mention an increasing number of people have distrust towards the USPS considering the political charade occurring there that is ![undermining confidence](https://www.theguardian.com/us-news/2020/aug/20/trump-usps-attacks-vote-by-mail-confidence) and ![continuing despite promises to cease](https://www.forbes.com/sites/andrewsolender/2020/08/19/reports-of-dismantled-usps-sorting-machines-continue-despite-dejoy-announcing-halt/#7a6bd2c026b9). To make it worse, ![1 in 5 of people who receive their packages are victims of porch piracy](https://www.valuepenguin.com/nearly-one-in-five-consumers-experienced-package-theft-since-start-of-quarantine). A perfect topic for a SMiShing campaign, indeed.

## The SMiShes

This section will cover the SMiShes themselves (pictures) and information about the origins of the attacker.

![Facebook Phish 2](/content/images/08-14-2020/fb-phish-2.png)

### Passive Reconnaissance

A DNS lookup shows that this domain is using Cloudflare as a proxy. However, the TXT record shows that the owner of this domain has an SPF record displaying a different IP than the A record. So I looked up this IP.

![Facebook Phish 3](/content/images/08-14-2020/fb-phish-3.png)

###

This IP address appears to be located in Moscow, Russia. It is also worth noting that this IP address has ports open for HTTP(S), FTP(S), IMAP(S), SMTP(S), and DNS.

![Facebook Phish 4](/content/images/08-14-2020/fb-phish-4.png)

![Facebook Phish 5](/content/images/08-14-2020/fb-phish-5.png)

## Conclusion

Based on the information gathered from analyzing the original website I have concluded the following:

- The initial phishing website impersonated Facebook and used a warning banner to coerce victims into entering credentials
- By looking at the source code it shows that submitting credentials attempts a POST request to https://lsdd[.]host/mango.php
- Doing a DNS lookup on lsdd[.]host shows an SPF record in the TXT record of the probable real IP address of the attacker
- Doing a lookup of this IP address shows that it originates from Moscow, RU (allegedly)

We could obviously perform more steps to gather even more information such as a PCAP or even probing the IP for other possible hostnames and more, but I gather enough on this phish
=======
---
layout: post
title: Attackers Leaving IP Address in SPF Record on Attempted Facebook Phish
featured: true
excerpt_separator: <!--more-->
date: '2020-08-14 18:19:00'
tags:
- phishing
- SPF
- social engineering
---

I haven't posted in a while so I figured I had enough time to do a simple post on a phishing attempt I came across today. This short post will show how I used open-source information to discover an attacker's *apparent* location from a phishing attempt that impersonated Facebook.
<!--more-->
## The Phish

**URL:** s3[.]us-west-1[.]wasabisys[.]com/tranqueavisp/indexs[.]html

![Facebook Phish 1](/assets/images/08-14-2020/fb-phish-1.png)

When navigating to the site, there are immediate red flags.

1. The URL is not of a Facebook domain.
2. There is a warning banner at the top of the page in red lettering which, is not inherently bad or malicious, but it creates a sense of urgency for the user which is seen in some phishing campaigns.

## Inspection

I've already determined that this is a phish just from the assumptions above, but it doesn't hurt being curious to see what else attackers are up to. Upon inspecting the source code of the website and navigating to the authentication form I noticed an obvious anomaly - the form action sends the credentials to an external website. So I looked into this website too.

![Facebook Phish 2](/assets/images/08-14-2020/fb-phish-2.png)

## DNS Information

A DNS lookup shows that this domain is using Cloudflare as a proxy. However, the TXT record shows that the owner of this domain has an SPF record displaying a different IP than the A record. So I looked up this IP.

![Facebook Phish 3](/assets/images/08-14-2020/fb-phish-3.png)

## IP Address Lookup

This IP address appears to be located in Moscow, Russia. It is also worth noting that this IP address has ports open for HTTP(S), FTP(S), IMAP(S), SMTP(S), and DNS.

![Facebook Phish 4](/assets/images/08-14-2020/fb-phish-4.png)

![Facebook Phish 5](/assets/images/08-14-2020/fb-phish-5.png)

## Conclusion

Based on the information gathered from analyzing the original website I have concluded the following:

- The initial phishing website impersonated Facebook and used a warning banner to coerce victims into entering credentials
- By looking at the source code it shows that submitting credentials attempts a POST request to https://lsdd[.]host/mango.php
- Doing a DNS lookup on lsdd[.]host shows an SPF record in the TXT record of the probable real IP address of the attacker
- Doing a lookup of this IP address shows that it originates from Moscow, RU (allegedly)

We could obviously perform more steps to gather even more information such as a PCAP or even probing the IP for other possible hostnames and more, but I gathered enough on this phish

## Definitions

##### Phishing



##### SMiShing



##### Social Engineering



##### SMiShing
