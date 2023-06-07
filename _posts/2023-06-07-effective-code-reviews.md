---
layout: post
title:  "Effective Code Reviews"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## Do you really need formal reviews?

__The best code review is the one done while writing the code.__ Pair or mob programming creates a so short feedback loop that most issues won't even make it into a commit, and can work as a perfectly good replacement for formal code reviews, as well as provide many other benefits. That's the way I prefer to work - if you'd like to try that instead, you can stop reading now and wait for the separate post on programming together I'll be adding soon!

If you still want to do asynchronous code reviews, consider the advice below.

## Good practices for reviews

__Everyone in the team should do code reviews.__ It keeps the entire team up to date with the code. Everyone can learn new things by seeing new constructs, and it can spark interesting discussions about the software and domain. Making everyone do reviews also prevents long waiting times and possible quality reduction from only a select few doing reviews.

__Automate all checks you can, such as static analysis, formatting etc.__ This will avoid tedious and unnecessary work for reviewers.

__Create a checklist for what to review__. It's important that everyone has a shared view of what is important and not in a review. Let the tools handle the rest! Consider things like:

* Are there any obvious logical errors in the code?
* Does the new code meet the requirements, even in the edge cases?
* Are there enough tests to cover the new functionality?
* Is the solution the right one for your codebase? Does it introduce any duplication, and does the abstractions match what you'd expect?

__Be kind__. If it's a matter of opinion or taste, there is no need for argument. Be happy that someone cares enough to make the change. If you get stuck up on details, chances are you will both lose speed and wind up in arguments that bring no value and lowers morale for no good reason. 

__Agree on how to introduce new members to the team.__ A wall text in your first code review makes for an appaling first impression.

### For submitters

* Make your commits small, frequent and with good commit messages
* Provide context for the commit
* Create a personal checklist with your most common mistakes
* Make sure to use the checklist yourself first
	* The code review should catch mistakes, not be an autocorrect feature.

### For reviewers

* Use the checklist, let tools do the rest
* Review often and for short sessions
