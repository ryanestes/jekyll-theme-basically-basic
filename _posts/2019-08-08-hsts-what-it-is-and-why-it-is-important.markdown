---
layout: post
title: 'HSTS: What It Is, Why It is Important, and Vulnerabilities Within'
date: '2019-08-08 23:44:26'
excerpt_separator: <!--more-->
tags:
- hacking
- hsts
- web-security
- ssl-tls
- http
- https
---

## Intro
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

**HTTP Strict Transport Security (HSTS)** is an HTTP security mechanism that allows web sites to declare themselves as accessible only via secure connections and for users to direct user agents (UAs), or your browser, to interact with web sites only over a secure connection. A "secure connection" in this case means an SSL/TLS encrypted HTTP connection, or HTTPS. This mechanism is designed to protect against downgrade attacks such as **sslstrip** which downgrades HTTPS to HTTP via redirection mappings. I will talk more about that later, but first, how did HSTS come about?
<!--more-->
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
## Origins
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

HSTS is defined in [RFC 6797](https://tools.ietf.org/html/rfc6797), but the beginnings of HSTS start with the work from Adam Barth and Collin Jackson from Stanford University. In their paper from the 17th International World Wide Web Conference (2008), ForceHTTPS: Protecting High-Security Web Sites from Network Attacks, Jackson and Barth describe how the prolific rise in wireless web browsing has led to wireless attacks on users browsing the web. **"ForceHTTPS"** , as they called it, was built to fix HTTPS configuration mistakes and, as we all know, configuration mistakes lead directly to breaches and financial losses for organizations such as the [Capital One breach](https://www.nytimes.com/2019/07/30/business/bank-hacks-capital-one.html) earlier in 2019. The implementation of ForceHTTPS is simple, the site owner sets the ForceHTTPS cookie and the browser will treat HTTPS misconfigurations as attacks, not simple misconfigurations. An attack in ForceHTTPS means that connections to HTTP sites are redirected to HTTPS, all TLS errors terminate the session, and embedded HTTP content within an HTTPS web site fail (HTTP ads for example).

Shortly after this paper was published by Adam Barth and Collin Jackson, In November of 2012, after a few publications, HSTS was published and defined in RFC 6797. According to RFC 6797, "(RFC 6797) embodies and refines the approach proposed in (ForceHTTPS)", which means HSTS is an evolution of what Barth and Jackson proposed with ForceHTTPS. HSTS was, seemingly, a direct response to Moxie Marlinspike's sslstrip demonstration at Black Hat DC 2009 considering its release was in November 2012. However, HSTS also attempted to address "click-through insecurity", which is when a security mechanism in a browser prompts a modal telling the user of a security infraction and the user clicks through the prompts anyways, voiding the security mechanism.

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
## How it Works
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

RFC 6797 presents 7 core requirements and 2 ancillary requirements for web site owners and browsers/User Agents (UAs) to meet HSTS. As a domain owner you must:

- Have a valid certificate verifiable by a Root CA
- Redirect HTTP to HTTPS through all subdomains using a 301/302 redirect, including the root www subdomain
- Serve a valid HSTS header in the HTTPS request which also specifies how long the HSTS entry will be cached

**A valid HSTS header looks like this:**

    Strict-Transport-Security: max-age=31536000; includeSubDomains; preload

##### Breakdown

- **Strict-Transport-Security** - Required; defined in RFC 6797 as how to start header
- **max-age** - Required, amount of time in seconds for which the UA regards the host as a known HSTS host
- **includeSubDomains** - Optional, asserts to UA that the entire policy applies to the subdomains of the given domain
- **preload** - Part of the preloaded list

The preload parameter in the header allows a web site to specify to browsers that they meet the requirements of HSTS and only want to be accessible via TLS. This prevents one vulnerability of HSTS as defined in RFC 6796 - the first request that contains a valid HSTS header, prior to caching the web site as HSTS enabled, is vulnerable to a MitM attack such as sslstrip. The preload list is an opt-in only policy typically done within a browser. Google owns its own HSTS preload list and many other browsers use this master list for theirs as well. Albeit, if you have a service such as Cloudflare, Akamai, and others, they have their own HSTS option to perform this action for you.

There are several websites that allow you to check to see if your domain has met the requirements for HSTS and to add to the preload list:

[https://hstspreload.org/](https://hstspreload.org/)  
[https://securityheaders.com/](https://securityheaders.com/)  
[https://www.ssllabs.com/ssltest/index.html](https://www.ssllabs.com/ssltest/index.html)  
[https://www.whoishostingthis.com/tools/user-agent/](https://www.whoishostingthis.com/tools/user-agent/)

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
## Why It's Important
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

The importance of HSTS lies within the attacks its used to prevent. RFC 6797 describes 3 types of attacks HSTS is used to prevent; **passive network attacks** , **active network attacks** , and **website development bugs**.

**A passive network attack** is most notably performed via 802.11 networks by sniffing packets and performing a MitM through a rogue AP or evil twin. Then, an attacker could either sniff all information unecrypted or at a worst case scenario, get unencrypted cookie information which could still be used for session hijacking among other attacks

**An active network attack** could also be performed via 802.11 networks could perform a MitM attack against a victim by placing a proxy between the web traffic and redirecting HTTPS traffic to their HTTP equivalent. Another important attack HSTS prevents is stealing of secure cookies or any other content sent over HTTPS. An attacker could also serve a victim false certificates and see all traffic in plaintext too!

**Website development bugs** happen and are impossible to avoid. The best form of action is to prevent errors through a vetted software development lifecycle and ensure developers are up-to-date with current coding standards and security controls. Also, make it harder for developers to make errors by creating easy-to-implement standards and fluid UI.

**Additionally, RFC 6797 conveys that UAs must disallow users to click through certificate warning messages which actively protects user negligence errors.**

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
## Exploits Against It
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

HSTS seems coincidentally in response to a presentation in 2009 at Black Hat DC by **Moxie Marlinspike** who demonstrated a MitM attack against HTTPS deemed **SSL stripping** , or originally, **SSL sniffing**. He also announced an accompaning tool called **sslstrip** which automates these attacks.

sslstrip2, sslstrip's predecessor, exploits HSTS by placing a proxy between the communications of the client and the server. A screenshot from his presentation shows what this looks like:

![SSLStrip](/assets/images/08/SSLStrip.png)

A user sending HTTPS traffic to a web server can be manipulated via a MitM attack to redirect to an HTTP equivalent (e.g. [https://facebook.com](https://facebook.com) would redirect to [http://facebook.com](http://facebook.com)). The extent of the threat landscape doesn't stop at just domains, sslstrip(2) can also strip secure cookies which hold session keys, unique identifiers, and any other information developers decide to put in.

Outside of the realm of sslstrip, attackers can perform simple security reconnaisance of websites just by checking headers with simple applications such as [https://securityheaders.com/](https://securityheaders.com/) and [https://www.ssllabs.com/ssltest/index.html](https://www.ssllabs.com/ssltest/index.html). The headers can reveal if HSTS is being used, if it allows redirects, what version of SSL is being used, if cookies are being used at all, and others.

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
## Conclusion
<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

HSTS is a security mechanism enforced by a specific header in an HTTPS request which was almost a direct response to the Moxie Marlinspike presentation of SSL sniffing and sslstrip. HSTS tries to fix the inconsistencies of websites not having HTTPS and prevents users from clicking through security. By placing a proxy in between communications, an attacker can serve a fake certificate and 'strip' SSL encryption from HTTPS traffic via a redirect to a genuine HTTP website.

In response, RFC 6797 provides a relatively easy implementation to HSTS, allowing for website owners to always use SSL/TLS encryption for all domains, including subdomains. The glaring issue arises when this is an opt-in only policy and many small, and even large, website owners neglect to opt-in correctly. Thus, many websites do not, and will not, have HSTS for their domains allowing another attack vector into networks, specifically wireless networks.

It's a small fix to a small problem with large implications. Hijacking HTTPS traffic could allow an attacker to read sensitive data in plaintext via a LAN or 802.11 networks.

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->
### References

#### Websites

- [https://tools.ietf.org/html/rfc6797](https://tools.ietf.org/html/rfc6797)
- [https://crypto.stanford.edu/forcehttps/](https://crypto.stanford.edu/forcehttps/)
- [https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)
- [https://https.cio.gov/hsts/](https://https.cio.gov/hsts/)
- [https://www.chromium.org/hsts](https://www.chromium.org/hsts)
- [https://www.troyhunt.com/understanding-http-strict-transport/](https://www.troyhunt.com/understanding-http-strict-transport/)
- [https://wiki.openssl.org/index.php/SSL\_and\_TLS\_Protocols](https://wiki.openssl.org/index.php/SSL_and_TLS_Protocols)
- [https://www.globalsign.com/en/blog/what-is-hsts-and-how-do-i-use-it/](https://www.globalsign.com/en/blog/what-is-hsts-and-how-do-i-use-it/)

#### Security Checks

- [https://hstspreload.org/](https://hstspreload.org/)
- [https://securityheaders.com/](https://securityheaders.com/)
- [https://www.ssllabs.com/ssltest/index.html](https://www.ssllabs.com/ssltest/index.html)
- [https://www.whoishostingthis.com/tools/user-agent/](https://www.whoishostingthis.com/tools/user-agent/)

#### PowerPoints

- [https://crypto.stanford.edu/forcehttps/forcehttps.ppt](https://crypto.stanford.edu/forcehttps/forcehttps.ppt)

#### Videos

- [https://www.youtube.com/watch?v=MFol6IMbZ7Y](https://www.youtube.com/watch?v=MFol6IMbZ7Y)

#### Banner Picture

- [http://www.iannecor.com/how-to-enable-http-strict-transport-security-hsts/](http://www.iannecor.com/how-to-enable-http-strict-transport-security-hsts/)
<!--kg-card-end: markdown-->
