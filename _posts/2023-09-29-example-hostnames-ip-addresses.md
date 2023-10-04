---
layout:     post
title:      Safe hostnames and IP addresses for examples
date:       2023-09-29
summary:    
categories:
tags:       programming
author:     jerry_orr
---

Scenario: you're writing up some documentation for your HTTP library. You've been working on it for hours, and it is getting mind-numbingly boring. You need to provide some examples of fetching by hostname and IP address. No problem:

```
client.fetchByHostname("fake.com")
client.fetchByIP("123.123.123.123")
```

But what happens if someone pastes your example into their code and runs it without thinking to change the hostname/IP? `fake.com` is a real website, currently selling landscaping services. And while `123.123.123.123` doesn't seem to be serving any content right now, it's owned by "China Unicom Beijing Province Network", so who knows what could be served up by that IP in the future?

Fortunately, IANA has been kind enough to reserve some [domain names](https://www.rfc-editor.org/rfc/rfc2606.html) and [IP addresses](https://www.rfc-editor.org/rfc/rfc5737.html) for use in examples.

Safe host names (also good for URLs and email addresses):
 * `*.example.com`
 * `*.example.org`
 * `*.example.net`
 * `*.test`
 * `*.example`
 * `*.invalid`

Note that IANA actually returns a web page for [example.com](http://example.com), [example.org](http://example.org), and [example.net](http://example.net). The reserved TLDs (`.test`, `.example`, and `.invalid`) do not have any full hostnames that resolve to any actual servers that I'm aware of.

Safe IPv4 addresses:
 * `192.0.2.0` to `192.0.2.255`
 * `198.51.100.0` to `198.51.100.255`
 * `203.0.113.0` to `203.0.113.255`

For IPv6, IANA [has reserved the unicast prefix](https://www.rfc-editor.org/rfc/rfc3849.html) `2001:DB8::/32`, so anything from `2001:DB8::1` to `2001:DB8:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF` is safe (h/t [@AKostur
](https://www.reddit.com/r/programming/comments/16yzo4p/comment/k3fmyd4)).

There are lots of good options for example IP addresses and hostnames. Don't be lazy and don't be cute: just use the reserved ones.
