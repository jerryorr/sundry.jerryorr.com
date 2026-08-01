---
layout:     post
title:      The development pipeline is a production system
date:       2026-07-31
summary:    When your team's development pipeline goes down, your ability to produce software goes down with it.
categories:
tags:       programming technology
author:     jerry_orr
---

Software developers learn early in their careers that nothing is more urgent than fixing a production outage. _Drop everything! All hands on deck!_

However, the same level of urgency is not often given to problems with our development tools, build systems, QA environments, and other parts of the software development pipeline. But for the development team, **the development pipeline is a production system**.

A software developer's job is to deliver value for the company. Sometimes that means building new features, sometimes that means fixing critical bugs for the customers' production systems. But *none of this can happen* when something is broken in the software development pipeline. 

If the code can't compile, the developers are unable to do their jobs, and the team isn't producing software. For the development team, *this is a production outage.* Fixing this should be a top priority.

If the QA server is down, the testers are unable to do their jobs, and the team isn't producing _working_ software. For the QA team, _this is a production outage_. Fixing it should be a top priority.

<figure>
  <img src="/images/software-assembly-line.png" alt="A software assembly line, on fire" class="full-width"/>
  <figcaption class="subtle">You will not be shocked to learn that I drew this myself.</figcaption>
</figure>

In manufacturing, there are [extensive processes and procedures](https://emshandbook.com/vol-12/4/escalation-slas/) on how to prevent and minimize downtime on the assembly line.{%include link-to-footnote.html i=1 %} And similar processes exist for [IT service outages](https://sre.google/resources/practices-and-processes/incident-management-guide). But I've found that most of those focus on outages in the service provided to _customers_, not for the people responsible for _building and supporting the services_.

I recommend thinking about all the components that take you from "customer wants something" to "that something is delivered to customers":

 * Issue reporting and change request systems, like GitHub Issues, Jira, etc
 * Tools developers use to directly build software, like IDEs, build tools (Gradle, Maven, etc), package repositories (npm, Maven Central, internal repositories, etc), local databases, containers, etc
 * CI/CD tools (Jenkins, GitHub Actions, etc).
 * A failing test suite (surely you don't deploy to production if the tests are failing?)
 * QA server outage (surely you don't deploy to production if QA hasn't tested it?)
 * Literally _any_ step in your process that prevents you from making changes and deploying them to production

A team with a broken development pipeline can't produce software, and _must_ treat this as a production outage.

* * *

{%include footnote.html i=1 content='Interestingly, they often call it the "production line". Is the usage of the term "production" in the software world related to its history in the manufacturing world?' %}
