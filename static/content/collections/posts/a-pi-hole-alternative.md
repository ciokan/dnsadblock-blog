---
title: A Pi-hole alternative
created_at: 2019-08-04T18:55:27.763Z
tags:
  - pihole
  - dnsadblock
  - dns ad block
  - pihole alternatives
authors: Romeo Mihalcea
categories: Dns
meta:
  description: 'An introduction to dnsadblock as a pi-hole alternative '
  keywords: 'pihole, dnsadblock, dns ad block, pihole alternatives'
isPage: false
showAuthor: false
isFeatured: false
pinSidebar:
  categories: Dns
  enable: false
hero:
  alt: A pi-hole alternative
  image: /images/uploads/dashboard.png
excerpt: 'An introduction to dnsadblock as a pi-hole alternative '
---
I will be clear from the start and say that PI-Hole is a really awesome project which I support. It is serving the same purpose with dnsadblock, but, with some drawbacks and I'm going to be covering these differences in this article.


{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IlNhbWUgYmFzaWMgZmVhdHVyZXMiLCJ0eXBlIjoicHJpbWFyeSJ9"}


Both dnsadblock and Pi-Hole act as dns servers that check each requested domain against a database of rules with blocked domains. If a rule matches, the query is then denied the request fails, saving you bandwidth and clearing your online experience from ads, tracking and other suspicious endpoints. You can add your own custom rules, see charts and diagrams regarding your activity and take action based on the logs.


{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IlRlY2huaWNhbDogUGktSG9sZSBvdmVyIGRuc2FkYmxvY2siLCJ0eXBlIjoicHJpbWFyeSJ9"}


If you're leaning more towards a technical experience and you don't mind getting your hands dirty, working with the "black screen" and you want the absolute control over the working software then Pi-Hole might be better. The software is open source and the code is visible to everyone. In some situations, because it is usually installed on LAN, Pi-Hole might even be faster due to a lower latency.


{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IlRlY2huaWNhbDogZG5zYWRibG9jayBvdmVyIFBpLUhvbGUiLCJ0eXBlIjoicHJpbWFyeSJ9"}


The advantages of Pi-Hole that I just described might be too much for the average user that just wants stuff to work, out of the box. [**dnsadblock**](https://dnsadblock.com) does not need any sort of software setup (you just have to change your DNS server), upgrades or maintenance. Pi-Hole is usually loaded on a small Raspberry Pi box and it sits between you and your router or between the router and the internet. That box needs power, cords, maintenance and upgrades - pretty much the same as the software. At [**dnsadblock**](https://dnsadblock.com) we do all that for you.

With Pi-Hole, you have to specify sources of commonly blocked domains. From experience I can tell you that somewhere between 30% and 60% of those domains are dead, lowering the average response rate due to so many rules with dead domains being checked against each request. We keep our lists healthy and always in-check on a regular basis and we group everything into groups that can be enabled or disabled at will allowing you to fully personalize your experience.


{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IkROUyBiYXNlZCBnZW8gcmVzdHJpY3Rpb25zIiwidHlwZSI6InByaW1hcnkifQ=="}


It's no secret that certain websites apply geo restrictions based on your DNS. You may change your IP address but they also query your DNS server to find out its location. If there's a missmatch between your IP address location and your DNS server location your request might be denied. DNS based geo restrictions are more popular than you might think and it makes it hard to access the content, even frustrating sometimes. They do it because a DNS is, theoretically, harder to fake in contrast to an IP address where proxies tend to be quite cheap these days.

This is an area where [**dnsadblock**](https://dnsadblock.com) has clearer advantages. With Pi-Hole, your DNS server is not changed and you can't do much about it. You could install it on a VPS somewhere but you lose many of its advantages while keeping the same disadvantages plus some (latency especially). We have servers in many locations and it only takes one minute from signing up to having a full and working connection. Changing the locations of the DNS servers can be done in seconds as well.


{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IkROUyBiYXNlZCBleGNsdXNpdmUgY29udGVudCIsInR5cGUiOiJwcmltYXJ5In0="}


The first type of DNS based filtering that comes to my mind is Netflix and BBC and I'm sure there are hundreds if not thousands more operating on the same principle. This is a geo-fenced wall that is often applied to completely block or alter the experience based on DNS location. Similar to the geo restrictions explained above, geo filtering and redirection works the same way, with clear advantages on the dnsadblock side.


{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6Ik1vYmlsZSBpbnRlcm5ldCwgb3IgcHVibGljIFdpLUZpJ3MiLCJ0eXBlIjoicHJpbWFyeSJ9"}


This is another area where Pi-Hole lacks. Being tied to your local network, remains effective only where you place it. Connecting to public networks or mobile internet leaves you completely open, with the same bloated experience that you're trying to avoid in the first place. Your ad filtering DNS server is basically tied to a physical location and cannot help you outside of it. With dnsadblock you only change the DNS servers once and they remain effective wherever you are. We even have mobile apps because it's hard to put a private DNS server on iOS and Android if you're not connected to a Wi-Fi network.

In general, I see a clear winner here but I'll let you decide what works best for you.
