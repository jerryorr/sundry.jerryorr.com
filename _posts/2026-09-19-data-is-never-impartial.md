---
layout:     post
title:      Data is never impartial
date:       2026-09-19
summary:    Even raw data reflects the judgment and perspectives of the people who decide what to collect and what to show.
categories:
tags:       programming technology
author:     jerry_orr
---


In the beginning of _Walden_, 19th-century philosopher Henry David Thoreau explains his choice to write in the first person:

> In most books, the I, or first person, is omitted; in this it will be retained... We commonly do not remember that **it is, after all, always the first person that is speaking.** I should not talk so much about myself if there were anybody else whom I knew as well.

It's a refreshingly honest admission that everything you read has _someone's_ perspectives embedded in it, no matter how carefully they may (or may not) try to remain neutral. It is impossible to entirely disassociate our experiences from what we write.

Thoreau could probably never have imagined the kind of data we can collect with 21st-century technology, but his caution is just as applicable today. Even raw datasets reflects the perspectives of the people who choose to collect it.

Data is never impartial. Several decisions go into every piece of raw data we see. Consider something as seemingly straightforward as application server logs.

**What data is *important* to collect?** A server request has a vast set of data points one _could_ record, but there's a cost in disk space and resource usage to collecting each one. Do I think the user's IP address is important? What about their browser? How long the request took? How long the TLS handshake took? How long it took until the response began? How long each plugin took? How long each database query took?

**What data is _appropriate_ to collect?** We're capable of tracking an astounding level of detail about web application visitors. Their location, the particular pages they access, third-party cookies that can be used to find out just about anything we want about them. Hopefully we're not so preoccupied with whether or not we _could_ collect data, that [we don't stop to think if we _should_.](https://www.youtube.com/watch?v=g3j9muCo4o0)

**What data do we actually _report_ on?** A pile of unanalyzed raw data is of little use by itself. When we share that data with someone, we make choices about what to emphasize from the results. Do I report on our excellent average response time? What about the 5% of requests that are excessively long and could be driving away customers? Are certain classes of request taking longer than others?

Each of these decisions requires judgment, and they reflect the experiences of the individual (or individuals) making the call{%include link-to-footnote.html i=1 %}. Nobody needs to falsify or hide data to present several versions of the truth.

So always remember that nothing you read—whether an essay, a blog post, documentation, data analysis, or even just raw data—is truly impartial. There is always a "first person that is speaking," someone who has decided what data to collect, how to interpret it, and what to show you.

* * *

{%include footnote.html i=1 content='And even if an AI made the decision, a human made the judgment call to use an AI, what model to use, what prompts to give it, etc.' %}
