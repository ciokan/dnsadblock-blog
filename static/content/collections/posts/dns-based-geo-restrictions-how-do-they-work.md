---
title: Dns-based geo restrictions - how do they work?
created_at: 2019-03-29T22:41:08.840Z
tags:
  - geo restriction
  - dns geo
  - dns geo restriction
authors: Romeo Mihalcea
categories: Dns
meta:
  description: Learn how a DNS-based geo restriction works
  keywords: 'geo restriction, dns geo, dns geo restriction'
isPage: false
showAuthor: true
isFeatured: false
pinSidebar:
  categories: News
  enable: false
hero:
  alt: Dns-based geo restriction
  image: /images/uploads/eugenio-mazzone-190204-unsplash.jpg
excerpt: >-
  Learn how a DNS-based geo restriction works and how our services can help you
  bypass them.
---
Nowadays if you want to stay anonymous or simply appear like you're from somewhere else you have to go the extra mile. It's not enough to change your IP address as a lot of companies introduced DNS based geo restrictions/detection into their arsenal and this one is a bit trickier to evade.

{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IkhvdyBkb2VzIEROUyB3b3JrIiwidHlwZSI6InByaW1hcnkifQ=="}

In short, the DNS server is responsible for turning a domain name to an actual IP address that points to a server serving the content under that domain. It's because servers should be replaceable without hurting the address, domains names as strings are easier to remember, brandable and easier to manage.

{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IkhvdyBkb2VzIGEgRE5TIGdlby1yZXN0cmljdGlvbiB3b3Jrcz8iLCJ0eXBlIjoicHJpbWFyeSJ9"}

The actual party responsible for knowing what is the IP address of the server of a domain name is called a DNS server. If a new request comes in and it doesn't know the address to respond with (out of it's own database or cache) it goes out and accesses that address to determine the IP address of the server behind it. This is a part where the IP address of the DNS server is visible to the server itself.

In practice, all you have to do is request a domain or subdomain that you're sure it's not in the cache of any DNS server out there, a generated one like this: `fs00nlsc3n9vwy1yu89b.dnsadblock.com`. In the backend of this thing there must be a webserver that listens to all subdomains `*.dnsadblock.com` and simply logs what is the IP address of the server trying to access each subdomain.

Once the logged IP addresses are present all you have to do is to query them against a geo-ip database and see the location of the DNS servers based on their IP address. Since most users are using their ISP nameservers, changing only your IP address will output some inconsistencies where your own IP location is pretty far away from your nameserver location.


{"widget":"qards-section-heading","config":"eyJ0aXRsZSI6IlllcywgYnV0IEkgY2FuIHVzZSBhIHB1YmxpYyBETlMgc2VydmVyIGluc3RlYWQifQ=="}


Yes you can but that won't help you too much. Most dns servers like google's `8.8.8.8` or Cloudflare's `1.1.1.1` are assigning a server based on lowest latency so that's always something really close to you. They want to provide performance but that same performance will mess with your plans.

We also use Cloudflare as an upstream to our servers but they only see the IP address of our own server and respond from somewhere close to it.

This is the same method that is used to detect DNS leaks of VPNs but more on that later.
