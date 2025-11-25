---
layout:     post
title:      Solve your problem by almost asking a question on StackOverflow
date:       2014-04-15
summary:    
categories:
tags:       programming
author:     jerry_orr
permalink:  2014/04/solve-your-problem-by-almost-asking.html
---

If you were to look at my [StackOverflow](http://stackoverflow.com/) profile, you would see that I’ve only asked a handful of questions in the years that I’ve been a member. However, this is _not_ because I don’t run into programming problems or don’t think to ask questions. In the process of formulating a [good StackOverflow question](http://stackoverflow.com/help/how-to-ask), I usually find the answer myself.  
  
First of all, it’s embarrassing to spend time typing up a question and have someone respond with a Google search providing dozens of hits that provide the answer. So before I even start typing, you’d better believe I **Google the hell out of the problem.** And many times, I find what I'm looking for.  

<img src="/images/help-me-help-you-gif.gif" alt="Famous scene of Jerry Maguire saying &quote;Help me help you!&quote;" class="wrap-right"/>

Assuming Google fails me, now I start explaining my problem. Since my audience is a group of complete strangers that have no knowledge of my application, I can’t simply say “I’m getting a SplinesNotReticulatedException from my FlangerFactory.” Even if I happen to be working on an open source project, I can’t expect the StackOverflow community to take the time to understand my full code base in depth. Thus, I am forced to **write a small example demonstrating the problem**. This is a fantastic way to narrow down the problem, because if I think the problem is with Dojo, but I can’t write a small example outside of my code base to reproduce the problem, then I’m most likely not dealing with a Dojo bug. In fact, there’s a good chance I’m looking in the wrong area of my code base. And if I can reproduce the problem, then maybe I can file a bug report with Dojo.  
  
Now I have a simple code example that helpful members of the community can work from. So that they don’t waste their time running into the same walls I did, I **explain exactly what I’ve tried thus far that hasn’t worked**. This saves a lot of back-and-forth “nope, I tried that and it doesn’t work” comments. And in the process of documenting what I’ve already tried, I often come up with new ideas. And sometimes, one of those ideas actually solves the problem.  
  
Of course, while I used StackOverflow as an example, this process really works with any community and medium, including emailing my coworkers. I respect the time of those who help me, so I make every effort to ask for help in the most efficient manner possible. In every forum I use, I always follow this process:  
  

1.  Thoroughly search Google (and any other available non-human resources).
2.  Write a concise example demonstrating the problem.
3.  Explain any failed attempts to solve the problem.

  
More often than not, I solve the problem myself by going through this process. And if I don’t discover the solution myself, then I have constructed a proper question that gives me the best chance of getting the help I need from my community.  
  
**Update:** as several Redditers [have pointed out](http://www.reddit.com/r/programming/comments/237518/solve_your_problem_by_almost_asking_a_question_on/), if you've documented a problem and found a solution, you should share it! StackOverflow [actually encourages posting and immediately answering your own question](http://stackoverflow.com/help/self-answer), and I imagine most communities feel the same way. My focus in this post was on discussing how to properly research and document a problem before asking for help, and highlighting how often you could end up solving the problem yourself, but I left out the importance of sharing that information with others.  
  
I wouldn't necessarily recommend posting your solution if it's "oops, I found a missing comma in one of my modules", and I don't think we need any more StackOverflow questions that could easily be solved via a Google search (that probably points back to a dozen StackOverflow questions). But if your solution could actually help others, then go ahead and publish it in whatever forum you like, or put it up on your personal blog, or email it to your coworkers...