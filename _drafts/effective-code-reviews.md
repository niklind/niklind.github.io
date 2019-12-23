---
layout: post
title:  "Effective Code Reviews"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## Why do code reviews?



## Good practices for reviews

__Everyone in the team should do code reviews.__ It keeps the entire team up to date with the code. Everyone can learn new things by seeing new constructs, and it can spark interesting discussions about the software and domain. Making everyone do reviews also prevents long waiting times and possible quality reduction from only a select few doing reviews.

__Automate all checks you can such as static analysis, formatting etc.__ This will avoid tedious and unnecessary work for reviewers.

__Create a checklist for what to review__. It's important that everyone has a shared view of what is important and not in a revuew. Let the tools handle the rest! Consider things like:

* Are there any obvious errors in the code?
* Does the new code meet the requirements, even in the edge cases?
* Are there enough tests to cover the new functionality?
* Is the solution the right one for your codebase? Does it introduce any duplication?

__Don't be petty__. If it's a matter of opinion or taste, avoid commenting and take it offline instead.

__Agree on how to introduce new members to the team.__ A wall of code review comments is not a very nice introduction.

__Don't keep scores for individuals.__ This may seriously lower the team morale.

__Use a code review tool__. It helps you keep track of code, comments and progress, and can help you set up the workflow you want without letting it become a burden. I would recommend [Gerrit](https://www.gerritcodereview.com) as such a tool.

### For submitters

* Make your commits small and frequent
* Provide context for the commit
* Create a personal checklist with your most common mistakes
* Make sure to use the checklist yourself first
	* The code review should catch mistakes, not be an autocorrect feature.

### For reviewers

* Use the checklist, let tools do the rest
* Review often and for short sessions
