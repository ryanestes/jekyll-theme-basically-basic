---
layout: post
title: Attackers Leaving IP Address in SPF Record on Attempted Facebook Phish
featured: true
date: '2020-08-14 18:19:00'
tags:
- phishing
- SPF
- social engineering
---

I haven't posted in a while so I figured I had enough time to do a simple post on a phishing attempt I came across today. This short post will show how I used open-source information to discover an attacker's *apparent* location from a phishing attempt that impersonated Facebook.

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

## The Phishing Attempt

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
