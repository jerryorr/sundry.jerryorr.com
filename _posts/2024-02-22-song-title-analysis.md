---
layout:     post
title:      The most common words in song titles
date:       2024-02-22
summary:    
categories:
tags:       music programming
author:     jerry_orr
---

Ever wonder what words show up most often in song titles? Anyone? Well, I did. And [Discogs](https://www.discogs.com) has a database of over 156 million song, so I put together [a couple Node.js scripts](https://github.com/jerryorr/song-analyzer) in search of some answers!

You can look at [the raw numbers](/data/song-title-analysis) yourself, but here are some things that stood out to me:

---

After skimming past common articles and prepositions, the most popular word in song titles is **You**, with 5.8 million occurrences, followed closely by **I** with 5.5 million. This outward focus on others might seem endearing, but then I decided to combine some first-persion pronouns and common contractions (**I**, **Me**, **I'm**, **I've**) and compare with the third-person equivalents (**You**, **You're**, **You've**). Turns out we're a lot more self-centered (or introspective?) than it first seemed: the first-person shows up 11 million times, while the third-person is only 6.2 million. And don't get too hopeful for reflections on our collective humanity: **We** came in 50th at a mere 818 thousand.

---

**Mix** and **Remix** are 12th and 19th. Not a big win for originality.

---

The most popular non-article/pronoun/preposition is, unsurprisingly, **Love**, showing up 4.1 million times. **Time** is the next noun at 1.2 million (after skipping things like **Mix**, **Remix**, **Version**, etc).

---

**No** comes in 14th with 2.3 million appearances. **Yes** isn't even in the top 500!

---

The most popular number in a title is **2** (1.3 million), just ahead of **1** (1.2 million). **3** put in a solid showing at 682 thousand; much better than the disappointing performance from **4** (which has the advantage of being a [numeronym](https://en.wikipedia.org/wiki/Numeronym) for **for**). I have no idea why some other numbers like **5** (296 thousand) show up so much.

---

If you like your song titles to let you know what to expect up front, here are the most popular genres to show up:
<ol>
	<li value="39"><strong>Blues</strong></li>
	<li value="86"><strong>Rock</strong></li>
	<li value="92"><strong>Instrumental</strong></li>
	<li value="426"><strong>Polka</strong></li>
	<li value="466"><strong>Disco</strong></li>
</ol>

**Rap** didn't appear in the top 500; rappers must feel that their genre is self-evident. Classics like [Ninja Rap](https://youtu.be/xOV6H4NcGEs) are clearly the exception.

And if you really want your song titles to be extra clear, **Song** itself came in 36th (1 million). So, roughly 0.6% of the time, songwriters are concerned that people might wonder what they're about to listen to, so they'd better make sure they know it's a song?

---

For classical music fans: 

<ol>
	<li value="26"><strong>Allegro</strong></li>
	<li value="133"><strong>Andante</strong></li>
	<li value="144"><strong>Adagio</strong></li>
	<li value="293"><strong>Moderato</strong></li>
	<li value="341"><strong>Allegreto</strong></li>
</ol>

Clearly people like some tempo in their classical music! But if you're not going for speed, Andante and Adagio are far more popular than a wishy-washy tempo like Moderato. Whether slow or fast, be bold!

---

**Blue** (81st) is the most popular color. Right behind is **Black** (99th), probably getting a big boost from metal songs. I expected **Red** (166th) to do better. **White** (216th), **Green** (339) **Brown** (491) were the only other colors I saw in the top 500. C'mon songwriters, let's get some more songs about Orange and Purple!

---

**Heaven** (212th) is a more popular topic than **Hell** (350th), and **Good** (74th) beat out **Bad** (183rd). A win for optimistic songs! Though **Die**, **Dead**, and **Death** showed up a combined 1.2 million times, so...

---

I could go on all day with this, but you should [check out the full list](/data/song-title-analysis) yourself and see what catches your eye!

_Data provided by [Discogs](https://www.discogs.com/developers)._
