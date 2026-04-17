---
layout:     post
title:      Find a needle in a haystack with git bisect
date:       2024-11-15
summary:    A story about using `git bisect`, my favorite tool for finding the source of regression bugs.
categories:
tags:       programming
author:     jerry_orr
---

My favorite tool for finding the source of regression bug is `git bisect`, and I'd like to tell you a story about how I used it today. Here's what I knew to start with:

 1. A bug report was filed on October 21 (**almost a month ago**) on our `main` branch.
 2. This bug doesn't exist in the previous version of our software, which was branched from `main` as the branch `release-5.7.0`.
 3. The branch `release-5.7.0` was created **about two months ago**, and a _lot_ has changed in `main` since then.

This is the process I went through to find the change that caused this bug.

## Find a commit where I know things were working

Since this bug doesn't exist in `release-5.7.0`, I know that the bug was introduced sometime after that branch was created from `main`:

```
git merge-base main release-5.7.0  
```

That gives me a "good" commit. To make this easier to follow, we'll call this `commit0001`.

## Find the commit from when the bug was reported

Since the bug was reported on October 21, I can narrow things down a bit by finding a commit where I _know_ the bug existed:

```
git log --before="2024-10-21" -n 1 main
```

That gives me a "bad" commit. Again, to make this easier to follow, we'll call this `commit9999`

Out of curiosity, I wanted to know how many commits there were between when I know it was working and when I know it was broken:

```
git rev-list --count commit0001..commit9999
```

Which tells me that I've narrowed it down to only... **2,088 commits**! Obviously, it's not practical to browse through 2,088 commits trying to guess which one might have caused the bug. 

## `git bisect` to the rescue

Fortunately, `git bisect` makes this _way_ easier. I already have a "good" commit where things work, and a "bad" commit where they don't:

```
git bisect start
git bisect good commit0001
git bisect bad commit9999
```

`git bisect` now basically guides me through a [binary search](https://en.wikipedia.org/wiki/Binary_search) to find the commit that caused the bug. It's helpfully started me out with this message:

```
Bisecting: 1044 revisions left to test after this (roughly 10 steps)
```

Like a binary search, `git bisect` has checked out the commit right in the middle of the good and bad commits. Now I run my code, and see if the bug is still there. In this case, the bug wasn't present, so I enter:

```
git bisect good
```

Using binary search logic, `git bisect` knows that the bug must have been introduced _after_ the commit I just tested. So it tells me:

```
Bisecting: 522 revisions left to test after this (roughly 9 steps)
```

And again, it sticks me half-way between the commit I just tested and the oldest commit that I know is bad. So I keep going, telling it `git bisect good` if things work, or `git bisect bad` if the bug is there. Each time, the list of suspects is cut in half.

Finally, after I've narrowed it down enough, `git bisect` tells me:

```
commit1234 is the first bad commit
commit commit1234
Author: Some Person <somebody@example.com>
Date:   Wed Oct 16 13:43:01 2024 -0400

[commit message]
```

So by testing **just 11 commits**, I've found the needle in a 2,088 commit haystack. Turns out the bug was introduced about **one month** and **767 commits** ago.

Once again, `git bisect` saved me a ton of time... even when subtracting the time I spent writing up this post!
