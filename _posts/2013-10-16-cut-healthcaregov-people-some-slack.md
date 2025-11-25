---
layout:     post
title:      Cut the HealthCare.gov people some slack
date:       2013-10-16
summary:    
categories:
tags:       technology
author:     jerry_orr
permalink:  2013/10/cut-healthcaregov-people-some-slack.html
---

On October 1, 2013, [HealthCare.gov](http://healthcare.gov/) was opened to the nation. As one of the more tangible aspects of the Affordable Care Act (aka ACA, Obamacare), the glitches it has experienced are getting lots of negative attention. It's been described as an "[inexcusable mess](http://www.usatoday.com/story/opinion/2013/10/07/health-care-insurance-exchanges-obamacare-editorials-debates/2940207/)" and a "[disaster](http://www.businessinsider.com/frustrated-with-the-new-health-care-exchange-2013-10)". I'm not going to discuss the merits of the ACA here. But as someone who spends every day building software, I think the criticisms of the HealthCare.gov application have been unfair. Here are a few reasons why we should cut them some slack.   

## Most webapps aren't immediately released to millions of users

When Google or Facebook are releasing a new app, do you think they just flip a switch and release it to the world? Absolutely not! They slowly release it to beta testers, or add the feature to a subset of users. They encounter bugs, fix them, slowly scale up their infrastructure, and wait until they've seen it succeed before opening it up to the general public. 

HealthCare.gov, on the other hand, launched to the entire nation at once. It didn't just have to deal with traffic from thousands (hundreds of thousands? millions?) of people looking for health plans for themselves; I'm sure a lot of curious people (like myself) went there [just to check it out](http://www.cnn.com/2013/10/15/health/obamacare-signup-issues-cohen/). There was no chance to work out the bugs, and no chance to gradually scale the infrastructure. This was almost guaranteed to be a problem.  

Now, perhaps they _should_ have slowly rolled out the site. I suspect, however, that the reasons were political. How do you decide who gets to sign up for healthcare first? By state? By last name? Random drawing? People who signed up ahead of time? And how do you explain to everyone else that they have to wait? People expect this from Google, but a highly charged political issue like the ACA makes it dicey.
  

## Much of what happens in the exchange is out of their control

HealthCare.gov is an extremely distributed application. John McDonough, a health policy professor at the Harvard School of Public Health, described it as:

> "an enormously complex task. The number of systems that have to work together – federal, state, insurance companies, the Internal Revenue System – the number of systems that have to align here is pretty daunting."

If there's a bug in the IRS endpoints, there's going to be a problem. If one of the hundreds of private insurance companies' systems can't handle the increased workload, there's going to be a problem. And as someone who has built plenty of distributed systems, I know that end users don't say "oh, it must be a problem with system X that this app depends on". They think it's a problem with whatever webapp they're using, and don't care what's going on in the backend.  
  
Nor should they care. But professional IT people should know better.  

## Most webapps aren't serving as a referendum on a heated national controversy

Frankly, there are a lot of people that want HealthCare.gov to fail primarily because they want the ACA to fail. And many people who oppose the ACA will still have a need to use HealthCare.gov. New Google apps are not typically tied to such a heated political issue, and are generally not used by people who don't want to use them. 

## So let's have some empathy for the people who build HealthCare.gov

This application was an enormous undertaking, with many challenges that few (if any) systems out there need to deal with. My expectation and hope is that the bugs will be worked out in the coming weeks, as happens with any new system. Whether the Affordable Care Act will be a success is yet to be seen; but the healthcare exchanges that support it were built by regular IT professionals that are just trying to do their jobs. Let's cut them some slack.
