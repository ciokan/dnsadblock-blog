---
title: You are still being tracked. Even with ad blockers installed
created_at: 2020-03-02T16:49:26.974Z
tags:
  - cname
  - cloaking
  - redirects
authors: Romeo Mihalcea
categories: Dns
meta:
  description: >-
    Tracking companies are using CNAME masking techniques to bypass
    browser-based ad blocks and track you
  keywords: 'cname cloaking, tracking, advertising, third-party cookie'
isPage: false
showAuthor: true
isFeatured: true
pinSidebar:
  categories: Dns
  enable: true
hero:
  alt: >-
    Tracking companies are using CNAME masking techniques to bypass
    browser-based ad blocks and track you
  image: /images/uploads/arvin-keynes-v4mnfkdmix4-unsplash.jpg
excerpt: >-
  Tracking companies are using CNAME masking techniques to bypass browser-based
  ad blocks and track you on the internet without being detected.
---
Advertisers and tracking entities are rolling out new ways of bypassing traditional ad blockers by using a disguising technique which conceals third-party content making it look as first-party content. This is important because most of the ad blockers we use today operate based on first-party input. For example, if your browser makes a request towards **dnsadblock.com**, an ad-blocking addon will apply its rules against that target.

The principle is simple so far. You gather millions of such rules and iterate over them to see if any will match against our target. If the match returns negative, the extension does not block the request. This worked wonders for years but the game is changing. Advertisers and tracking entities are masking their address behind CNAME entries now and this makes it harder if not impossible for browser-based filters to block since they do not have access to the DNS records.

A CNAME (Canonical Name Record or Alias Record), in simple terms, is a way of pointing a domain name to another one - as an alias. I can have one domain pointing to another one, just like a normal redirect but at the DNS level. Let's take Netlify as an example. Whenever you deploy a new application to their control panel, you receive a unique address in the form of: `festive-nobel-876c06.netlify.com` (this is actually the address for our blog). It's ugly but it works for them. This is the main address of the app and you can't change it but you can add aliases and point your own domain towards this one using a CNAME:

```
$: dig blog.dnsadblock.com

;; ANSWER SECTION:
blog.dnsadblock.com.	103	IN	CNAME	festive-nobel-876c06.netlify.com.
festive-nobel-876c06.netlify.com. 20 IN	A	157.230.120.63
```

```
$ dig festive-nobel-876c06.netlify.com

;; ANSWER SECTION:
festive-nobel-876c06.netlify.com. 20 IN	A	68.183.215.91
```

So one domain points to an `A` record which hosts a service but other domains can point to the same resource using a CNAME towards the first domain.

Back to out adblocking story. Let's say our extension is blocking a tracking domain such as `device-metrics-us-2.amazon.com`. Whoever uses that domain to track users will fail because it won't work with requests being filtered by our extension. What happends if I create a CNAME from `device-metrics-us-2.bogus.com` towards `device-metrics-us-2.amazon.com` and start using `device-metrics-us-2.bogus.com` in my app in order to track users? Those requests will slip through and it's business as usual with a simple CNAME. We can start injecting first-party javascript into our pages without any worries of them being filtered:

```
<script src="https://device-metrics-us-2.bogus.com/track.js"></script>
```

In all honesty, I'm surprised it took them so many years to come up with this method. It's only now that this subject enters mainstream. CNAME's were here many years ago when adblocking started being a thing.

So…what can we do about this? Do we ditch our ad blockers because they're not good any more? No, we combine multiple services to combat these advertisers. One of the strengths of a DNS-based content filter such as DnsAdBlock is that it can catch these `CNAME` masking techniques and filter them out. At DnsAdBlock we run our filters against the initial request gut also against the response we receive from our DNS upstreams so `device-metrics-us-2.bogus.com` might slip through for us as well but the DNS response will show a CNAME towards `device-metrics-us-2.amazon.com` and we will catch that one and deny the request.

In case you're curious about the amount of tracking being performed on the internet I invite you to see the attached screenshot of blocked requests in just 24 hours of activity for a simple computer (mine). I didn't even used it the whole time since I regularly have to change my DNS servers because I'm testing and developing new features for DnsAdBlock.


{"widget":"image","config":"eyJsaWdodGJveCI6dHJ1ZSwic3JjIjoiL2ltYWdlcy91cGxvYWRzL3NjcmVlbnNob3QtZG5zYWRibG9jay5jb20tMjAyMC4wMy4wMi0xOV8xOF80Ny5wbmciLCJhbHQiOiJCbG9ja2VkIEROUyByZXF1ZXN0cyBieSBEbnNBZEJsb2NrIiwiY2FwdGlvbiI6IjI0aCBzY3JlZW5zaG90IG9mIGJsb2NrZWQgRE5TIHJlcXVlc3RzIGJ5IERuc0FkQmxvY2siLCJsYXlvdXQiOiJmdWxsLXdpZHRoIn0="}


This is a combined effort that completes the circle. Browser based ad blockers do a fantastic job but fail on many fronts:

* they can't block system-wide requests (you would be surprised to know how busy is `Chrome` or `Windows` all the time)
* they can't detect `CNAME` redirects
* they are about to be [limited by Chrome](https://www.wired.com/story/google-chrome-ad-blockers-extensions-api/) and other browser vendors
* some offer questionable results by allowing "acceptable ads"

The only solution that works is to combine DNS based filtering with browser based filtering so I'm inviting you to give us a try with a 6-month coupon (for the **Home** plan) for being so patient in reading our blog (valid during our BETA): **BETALISTERS**
