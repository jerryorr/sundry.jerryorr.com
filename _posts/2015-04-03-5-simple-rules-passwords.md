---
layout:     post
title:      5 simple rules for securely storing passwords
date:       2015-04-03
summary:    
categories:
tags:       programming technology
author:     jerry_orr
permalink:  2015/04/5-simple-rules-for-securely-storing.html
---

Far too frequently, systems are hacked and their user databases are compromised. And there are far too many cases where the database contains [plain text passwords](http://motherboard.vice.com/blog/hackers-leaked-42-million-plaintext-dating-site-passwords), [poorly hashed passwords](http://arstechnica.com/security/2012/06/8-million-leaked-passwords-connected-to-linkedin/), or [two-way encrypted passwords](https://nakedsecurity.sophos.com/2013/11/04/anatomy-of-a-password-disaster-adobes-giant-sized-cryptographic-blunder/), despite the wealth of resources available on how to properly store user credentials. And it's not just legacy databases; just this week, I saw a [reddit thread](https://www.reddit.com/r/programming/comments/313cwa/enough_with_the_salts_updates_on_secure_password/) with at least one developer advocating custom hashing functions and "security through obscurity".

Though cryptography is a complex subject, you don't need to be an expert to be a good steward of your users' credentials. Just follow these simple rules when selecting a scheme:[1](#fn1)<a name="top1"></a>

1.  Use a proven one-way hashing algorithm that has been publicly reviewed by security experts, such as [bcrypt](http://en.wikipedia.org/wiki/Bcrypt), [PBKDF2](http://en.wikipedia.org/wiki/PBKDF2), or [scrypt](http://en.wikipedia.org/wiki/Scrypt).
2.  Don't attempt to write your own hashing algorithm. You can't rely on "security by obscurity"; you must assume the attacker has your source code, and can attack your inferior algorithm.[2](#fn2)<a name="top2"></a>
3.  I mean it, don't write your own hashing algorithm! Just use one of the ones from Rule #1. They are free, available on virtually any platform, and have been proven secure by the best minds in security.
4.  Seriously, why are you even still reading this? Rule #1 is all you need!
5.  Alright, if you are really going to ignore Rule #1, please at least notify your users that you are not safely storing their passwords, and in the event of a database breach, their passwords will become public knowledge.

I don't like to deal in absolutes, particularly in software development, but I truly feel strongly about this. **There is no situation in which you should be developing your own password hashing algorithm!**[3](#fn3)<a name="top3"></a> Here's an example of [using PBKDF2 in Java](http://blog.jerryorr.com/2012/05/secure-password-storage-lots-of-donts.html) without importing any external libraries; if Node.js is your thing, there's [a module for bcrypt](https://www.npmjs.com/package/bcrypt); there's a [Ruby gem for scrypt](https://github.com/pbhogan/scrypt); hell, even PHP has a [built-in password hashing function](http://php.net/password_hash) that uses bcrypt. Really, virtually any language has a freely available library for any of those three algorithms. Just Google "**[your-language-of-choice bcrypt OR scrypt OR pbkdf2](https://www.google.com/webhp#q=java+bcrypt+or+scrypt+or+pbkdf2)**" and you'll find plenty of options.

Any hash function that has not been through rigorous public peer review is almost certainly not properly designed. If [Niels Provos](http://en.wikipedia.org/wiki/Niels_Provos) himself — one of the creators of bcrypt — was on my team and wanted to use a new hash function he created in private, I would pass on it and use bcrypt. Although I doubt Mr. Provos would be foolish enough to suggest using such an algorithm; he may have created the next great password hashing algorithm, but he would likely realize that it could not be relied upon until it had been evaluated by his fellow security experts.

So when you need to store user credentials, just please, _please_ hash them with bcrypt, scrypt, or PBKDF2. It's easy. Don't try to be clever.

* * *

<a name="fn1"></a><sup>1</sup> Even better: don't store user credentials if you don't have to. Consider using an OAuth provider, or your organization's internal identity system. It saves some effort, and saves your users from remembering yet another set of credentials.[↩](#top1)

<a name="fn2"></a><sup>2</sup> This is essentially [Kerckhoff's principle](http://en.wikipedia.org/wiki/Kerckhoffs%27s_principle): "The system must not require secrecy and can be stolen by the enemy without causing trouble"[↩](#top2)

<a name="fn3"></a><sup>3</sup> Okay, I suppose if you are entering something like the [Password Hashing Competition](https://password-hashing.net/) or doing academic research, that's fine. But you still shouldn't be using it in a real application until it has been through thorough public review.[↩](#top3)
