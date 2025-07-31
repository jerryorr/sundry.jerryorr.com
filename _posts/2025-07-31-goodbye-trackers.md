---
layout:     post
title:      Goodbye trackers
date:       2025-07-31
summary:    Google will track you all over the web, but not on my site.
categories:
tags:       programming technology
author:     jerry_orr
---

Back when I first started this blog, I was curious about the traffic I was getting. How many people were visiting? What lead them here? So—like many others at the time—I set up Google Analytics on my blog.

And, well, I still _am_ curious about all these things.

But not enough to subject you to [Google's surveillance](https://en.wikipedia.org/wiki/Privacy_concerns_with_Google#Tracking).

So as of today, I have removed all 3rd party components from by blog. That means no Google Analytics. No Google Fonts. Not even any CDNs{%include link-to-footnote.html i=1 %}, just in case. When you load this blog, every request goes to my web host, and nowhere else.

Now, I have to admit that my web host is GitHub Pages, which is owned by Microsoft, which is—ah, not exactly innocent in the [enshittification of the web](https://en.wikipedia.org/wiki/Enshittification). So maybe I will someday get my blog off big-tech hosting entirely.

But I think this is a good start.

* * *

{%include footnote.html i=1 content="I used to load FontAwesome from a CDN." %}