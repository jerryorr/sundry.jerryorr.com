---
layout:     post
title:      Perception of a technology's reliability
date:       2025-03-25
summary:    It doesn't take much for software to go from being considered "reliable" to "flaky garbage".
categories:
tags:       programming technology
author:     jerry_orr
---

I often think about Evan Hahn's article "[95% is very different from 99%](https://evanhahn.com/95-percent-is-very-different-from-99-percent/)". He classifies it as "a rant", but I think he really hit on something. He says:

> I think there’s a huge difference between “usually works” and “almost always works”.

One of his examples is a phone's autocorrect, saying:

> My phone’s autocorrect, though essential and impressive, fails all the time.

I'd like to dig further into that. When typing on my phone, I _constantly_ have to break my chain of thought to look back and make sure that autocorrect hasn't turned my text into complete nonsense. Sure, it might have corrected some errors, but it also might have changed what I _intentionally_ typed into what autocorrect _thinks_ that I _meant_ to type. 

By contrast, when typing on a keyboard, I can be certain that whatever I typed is what showed up on the screen. Granted, I might{%include link-to-footnote.html i=1 %} make some mistakes, but I can be certain they are _my_ mistakes and that the _keyboard_ has not been responsible for any errors. This near-certain reliability means that, as a fairly competent touch-typer, I can confidently type out large blocks of text without breaking my chain of thought, and then just go back later to proofread.

This difference in reliability is the biggest reason why I can't bear to write anything more than a couple sentences long on my phone.

## A programming example

I do most of my Java programming in IntelliJ, and there's a handy shortcut to "Build and rerun test". This is normally a lot faster and than hitting "Build", waiting for the build to complete, then hitting "Rerun test". It keeps me in my [flow state](https://en.wikipedia.org/wiki/Flow_(psychology)).

However, there was a period where something was wonky in either my environment or IntelliJ. "Build and rerun test" would usually work, but _very occasionally_ build the code yet somehow run the tests on the _previous_ version of the code.

I didn't compile stats on this, but it probably worked about 95% of the time. Yet this absolutely _tanked_ my productivity, because any time I ran "Build and re-run test", I couldn't really be sure if the results I saw were from my latest code. I then either had to run the tests again every time to be absolutely sure, or abandon "Build and rerun test" entirely in favor of manually building, waiting for the build to complete, and _then_ running the tests.

That 5% failure rate was effectively doubling the time for my build/test cycle!

## What's the point?

As a software developer, this reinforces that I need to be extra vigilant about fixing "intermittent" errors. It doesn't take a very high failure rate for software to go from being considered "reliable" to "flaky garbage".

It also reminded me how important it is to have reliabile development tools. Losing my flow state was killing my productivity, and I need to always be on the lookout for anything else in my development process that could be doing this.

* * *

{%include footnote.html i=1 content="I will." %}
