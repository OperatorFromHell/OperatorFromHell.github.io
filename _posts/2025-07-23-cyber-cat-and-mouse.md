---
layout: post
title: "My Post Title"
image: /assets/images/my-post-image.jpg
---


# Cyber Cat and Mouse: Law Enforcement vs The Dark Web

![Image of a cyber-looking cat and mouse.]({{ "/assets/images/cyber_cat_and_mouse.webp" | relative_url }})

-----

## Introduction
The Dark Web poses a significant challenge for law enforcement (LE), due to its anonymisation features. These features enable threat actors to operate with relative impunity, hosting illicit domains such as cybercrime forums, drug markets, and Data Leak Sites (DLS). Despite the growing presence of such platforms, there remains a notable lack of structured and direct education and resources available on how to effectively dismantle and takeover these domains. As a result, there is a growing demand for specialised training and support in this area.

This article will be discussing my dissertation project [“VoidCore”](https://github.com/Mrdedsecurity/VoidCore), highlighting the common themes in attacks against Tor domains both from LE and threat actors.

-----
## What is the Dark Web?
The “Dark Web” is an umbrella term for a hidden part of the internet that a user cannot access without access to specific software. Since its creation, it has grown in both user base and illegal activity.

![Iceberg of Webs](https://upload.wikimedia.org/wikipedia/commons/thumb/0/06/Iceberg_of_Webs.svg/960px-Iceberg_of_Webs.svg.png?20251107174510 "Iceberg of Webs")
<p align="center"><em>Iceberg of the webs - https://commons.wikimedia.org/wiki/File:Iceberg_of_Webs.svg </em></p>

The Dark Web can be broken down into multiple technologies that fall under the umbrella. The most popular of which is [Tor (The Onion Router)](https://www.torproject.org/). Other alternatives projects include [I2P (The Invisible Internet Project)](https://geti2p.net/en/) and [Freenet](https://freenet.org/).

-----
## The Onion Router
Tor was [originally](https://www.torproject.org/about/history/) developed by the US Navy for covert communication in the 1990s, later becoming publicly available. Following this, a research and education organisation “The Tor Project” was established to manage the network and maintain the Tor Browser. The network operates by “nodes” which are volunteers donating their network connection to help strengthen the network. If a user wishes to access a Tor domain, it will pass through nodes that will add layers of encryption.

## Law Enforcement Challenges

The Dark Web, unfortunately, causes major challenges for LE with a significant number of operations focused on battling illegal Tor domains, which remains difficult to control. The difficulties fall within the anonymity which Tor provides making it difficult for traditional policing tactics to be deployed. There are substantial barriers for LE when it comes to policing the dark web, causing them to always be on the back foot. The primary limitation for LE is simply the number of illegal domains and the amount of criminality making the task increasingly harder for LE.

LE entities typically exploit cyber security vulnerabilities and capitalise on poor OPSEC (Operational Security) against targeted domains. LE exploits the flaws for several reasons, such as gathering evidence, identify threat actors real-world identities and harvesting decryption keys. LE also use compromised Tor domains for reputational damage against threat actors; Typically defacing seized domains with a notice of seizure, which will affect the impacted domain’s reputation amongst cybercriminals. An example this can be seen below.

![Breach Forums Seizure Notice](https://cdn.sanity.io/images/fo9xc2x1/production/680664edea53e0828fea476584401048438d12db-2832x1636.jpg?w=2832&h=1636&fm=webp&q=90&fit=max&auto=format&dpr=2 "Breach Forums Seizure Notice")
<p align="center"><em>Breach Forums seizure notice (May 15,2024) – https://intel471.com/blog/breachforums-saga-continues-whats-next </em></p>

-----
## LockBit seizure
Several landmark actions have targeted the dark web. One particularly influential case inspired my dissertation is the seizure of the LockBit’s DLS.

![LockBit’s compromised DLS ](https://www.nationalcrimeagency.gov.uk/images/Feb2024/Leak_site.jpeg "LockBit’s compromised DLS")
<p align="center"><em>LockBit’s compromised DLS – https://www.nationalcrimeagency.gov.uk/the-nca-announces-the-disruption-of-lockbit-with-operation-cronos</em></p>

In [February 2024](https://www.nationalcrimeagency.gov.uk/the-nca-announces-the-disruption-of-lockbit-with-operation-cronos), NCA (National Crime Agency) with partners disrupted [LockBit](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-165a), a Russian Ransomware-as-a-Service (RaaS) operation with Operation Cronos; This led to the seizure of the domain and gathered large sums of data such as affiliate names leading to numerous arrests. LE utilised the compromised domain to share several of their findings. According to the education and research group [VX-Underground](https://vx-underground.org/), LE allegedly compromised the domain via [CVE-2023-3824](https://nvd.nist.gov/vuln/detail/cve-2023-3824), a PHP Buffer overflow flaw.

![vx-ug tweet.]({{ "/assets/images/vx-ug_tweet.png" | relative_url }})
<p align="center"><em>VX-Underground tweet – https://x.com/vxunderground/status/1759732862335504773</em></p>

-----
## The findings
For VoidCore, I drew on a range of information sources, including research articles and law enforcement announcements. However, a key challenge was the limited technical depth in many of these references, which restricted the level of detail I could incorporate.

**Please note, that these findings come from my independent research and I have had no collaboration with others or organisations including LE.  My findings have not been peer-reviewed. Overall, I would like to say my findings give a good picture however I likely missed some things! My findings also only dated to May 2025.**

The top vulnerabilities as shown above are the following: 

1. Infrastructure misconfiguration = 22% 
2. SQLi = 22% 
3. Access into infrastructure = 15% 
4. Compromising database = 15% 
5. Cross-site-scripting (XSS) = 11%
6. OTHER = 15%

-----

## VoidCore

The theme of VoidCore is a ransomware Data Leak Site (DLS). The design of the domain took inspiration from LockBit’s DLS.

For hosting the domain, an AWS EC2 instance was utilised.  As previously discussed, the domain had the most common vulnerabilities implanted into it, which are the following:

### 1) Infrastructure misconfiguration

The sever-status endpoint was left accessible, exposing sensitive information such as the server’s IP address, software version, active connections, and other diagnostic data. In a real-world scenario, this misconfiguration could significantly aid law enforcement and may be used to potentially seize the a Tor domain.

![VoidCore Serer Status Exposed]({{ "/assets/images/voidcore_server_status.webp" | relative_url }})
<p align="center"><em>VoidCore server-status exposed.</em></p>

### VoidCore server-status exposed.

2) Cross-site scripting (XSS)

A XSS vulnerability exists within the “victims” search bar. This flaw could opening the door to allow LE harvest session tokens thereby identifying perpetrators and gaining access to their accounts.

![VoidCore XSS Flaw]({{ "/assets/images/voidcore_xss.webp" | relative_url }})
<p align="center"><em>VoidCore XSS Flaw</em></p>

### 3) SQL Injection (SQLi)

The login portal for affiliates and the operations leader “VoidSoup” is vulnerable to SQLi, which allows access to accounts and access data. 

![VoidCore SQLi]({{ "/assets/images/voidcore_sqli.webp" | relative_url }})
<p align="center"><em>VoidCore SQLi</em></p>

-----
## Conclusion

The dark web continues to pose a significant challenge for LE. Despite growing efforts from governments, threat actors show no indication of fully abandoning Tor. A major contributing factor to this issue is the lack of accessible education and training on how to combat the illegal domains.

Thanks for reading, hope you found it interesting! 
