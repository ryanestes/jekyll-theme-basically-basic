---
layout: post
title: SMiShing Campaign Leverages USPS and Parcel Service Distrust
featured: true
excerpt_separator: <!--more-->
date: '2020-08-30 18:35:29'
tags:
- phishing
- SMiShing
- social engineering
- scam
---

Beginning the week of August 23rd, a [SMiShing](#smishing) campaign began to unfold that, by and large, impersonated large mail carrier and parcel services with the intention of stealing sensitive information from the victims. This post will explain the high-level tactics and technologies the attacker(s) used to send these SMiShes as well as several real-world text message examples that were attributed to this campaign, including myself. At the end of this post will be the list of known domains and URLs used in this campaign (tentative).
<!--more-->
## Preliminary Information

### Definitions

Here a few definitions for need-to-know terms for this post.

**Phishing**: An attempt to steal sensitive information or perform malicious actions by masquerading as a trustworthy entity

**SMiShing**: SMS + Phishing. An Attempt to perform a phish via SMS.

**Social Engineering**: Manipulating individuals from divulging sensitive information used for malicious purposes. Commonly known as "hacking people".

### What is SMiShing

SMiShing campaigns, and other similar [social engineering](#socialengineering) attacks, often utilize current events and other psychological tricks to further coerce victims into divulging sensitive information. For example, I bet you have received an email, text, or instant message that claims you can lose 50 pounds fast and all you have to do to get a limited supply of their supplement is to click a link. Well, there are several psychological factors at play here, but there are two that stick out immediately:

1. The attacker assumes that the victim wants to lose weight or has body image issues. Considering about [half of Americans say that they're trying to lose weight](https://time.com/5334532/weight-loss-americans/), this is an effective approach
2. The use of the words "limited supply" imply that the stock is low and the victim needs to react fast to get this supplement. This is a common tactic in social engineering that combines emotion with time-sensitive decisions.

The SMiShing campaign in this post impersonated common postal and parcel services in the United States such as USPS, UPS, FedEx, DHL, and Amazon. This is another effective industry to impersonate as the general public doesn't exact have much trust in these services. For starters, a [report from Clutch](https://clutch.co/logistics/resources/package-theft-statistics-people-trust-ups-most-deliver-packages-safely) states that 29% of people trust UPS to deliver their package securely, the highest score of all 5 carriers listed (USPS 27%, Amazon 22%, FedEx 20%, DHL 2%). Not to mention an increasing number of people have distrust towards the USPS considering the political charade occurring there that is [undermining confidence](https://www.theguardian.com/us-news/2020/aug/20/trump-usps-attacks-vote-by-mail-confidence) and [continuing despite promises to cease](https://www.forbes.com/sites/andrewsolender/2020/08/19/reports-of-dismantled-usps-sorting-machines-continue-despite-dejoy-announcing-halt/#7a6bd2c026b9). To make it worse, [1 in 5 of people who receive their packages are victims of porch piracy](https://www.valuepenguin.com/nearly-one-in-five-consumers-experienced-package-theft-since-start-of-quarantine). A perfect topic for a SMiShing campaign, indeed.

## The SMiShes

This section will cover the SMiShes themselves (pictures) and information about the origins/infrastructure of the attacker. First, all of the SMiShes.

### l1smc[.]info

<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l1smc.PNG" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l1smc-2.PNG" width="250" height="auto">

### l2scr[.]info

<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l2scr.PNG" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l2src-2.png" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l2scr-3.PNG" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l2scr-4.PNG" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l2scr-5.PNG" width="250" height="auto">

### l3smr[.]info

<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l3smr.png" width="250" height="auto">

### l4sve[.]info

<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l4sve.png" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l4sve-2.PNG" width="250" height="auto">

### l5ssv[.]info

<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l5ssv.png" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l5ssv-2.png" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l5ssv-3.PNG" width="250" height="auto">
<img src="https://raw.githubusercontent.com/ryanestes/ryanestes.github.io/master/assets/images/08-30-2020/l5ssv-4.PNG" width="250" height="auto">

### Passive Reconnaissance

As can be seen from the variety of images above that this attack didn't target a specific victim type or technology. Rather, this SMiShing campaign simply leveraged the distrust in the parcel services discussed above. What we initially know from these SMS messages above:

- Each domain is a 5 alphanumeric string that follows a certain pattern ("l" + incrementing number + "s" + 2 random letters)
- Each message mentions something about an old package that wasn't received
- Each message asks users to click a link to figure out information about the package
- Clicking on the links leads to [several different landing pages](#landingpages)

#### IP Address

A `dig` command was used to figure out the IP address of the server hosting this webpage.

**IP Address: 8.210[.]108.16**

![dig command](/assets/images/08-30-2020/dig_command.png)

#### Whois Lookup

The DomainTools Whois lookup tool was used to discover information about the IP address/server. Based on the information in the Whois lookup, this server is hosted on an Alibaba cloud server in Hong Kong, China. This means the attackers are using a cloud service to host or send these SMiShing messages out and are likely harvesting sensitive information using scam tactics. Based on the landing pages, these SMS message links likely lead to pages that have been compromised or are hosted by the attackers themselves. There's not too much more than can be gathered unless a PCAP is gathered and further analysis is done, but that is out of scope.

![Whois](/assets/images/08-30-2020/whois1.png)
![Whois](/assets/images/08-30-2020/whois2.png)

#### Landing Pages

Listed here are all the possible landing pages resulting from clicking any of the URLs in this post. Note: This is only the *known* list of landing pages, there could be more.

![USPS SMiSh](/assets/images/08-30-2020/usps_smish.png)
![Membership Rewards SMiSh](/assets/images/08-30-2020/membershiprewards_smish.png)
![Free iPhone 11 SMiSh](/assets/images/08-30-2020/freeiphone11_smish.png)
![FedEx SMiSh](/assets/images/08-30-2020/fedex_smish.png)
![Cox SMiSh](/assets/images/08-30-2020/cox_smish.png)
![Cox SMiSh 2](/assets/images/08-30-2020/cox2_smish.png)

## Domains and URLs

Listed below are the domains and URLs discovered from this SMiShing campaign, so far.

### domains

- l1smc[.]info
- l2scr[.]info
- l3smr[.]info
- l4sve[.]info
- l5ssv[.]info
- bgfdc[.]info
- sbcae[.]info
- utzho[.]info

### URLs

- l1smc[.]info/i4B8uiee0a
- l1smc[.]info/i4B8uin2vq
- l2scr[.]info/KiF46J87bC
- l2scr[.]info/KiDo37zjMj
- l2scr[.]info/KigKalF3R9
- l2scr[.]info/KiDo375mT7
- l2scr[.]info/KilMlbzjMj
- l3smr[.]info/09Nh46erLO
- l4sve[.]info/o6icgxntOe
- l4sve[.]info/o6icgxzjMj
- l5ssv[.]info/QTyhVcBhKs
- l5ssv[.]info/QTuVNYkWh3
- l5ssv[.]info/QTwBRAjqK2
- l5ssv[.]info/QTyhVc6tel
- bgfdc[.]info/7vsqg76ZGz
- sbcae[.]info/BYhxV4jAB1
- utzho[.]info/Tf7Slh4POr
