---
layout: post
title:  "Effective Code Reviews"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## Why do code reviews?

__The best code review is the one done as you create the code.__ Pair or mob programming creates a so short feedback loop that most issues won't even make it into the code, let alone into the code review.

## Good practices for reviews

__Everyone in the team should do code reviews.__ It keeps the entire team up to date with the code. Everyone can learn new things by seeing new constructs, and it can spark interesting discussions about the software and domain. Making everyone do reviews also prevents long waiting times and possible quality reduction from only a select few doing reviews.

__Automate all checks you can such as static analysis, formatting etc.__ This will avoid tedious and unnecessary work for reviewers.

__Create a checklist for what to review__. It's important that everyone has a shared view of what is important and not in a review. Let the tools handle the rest! Consider things like:

* Are there any obvious logical errors in the code?
* Does the new code meet the requirements, even in the edge cases?
* Are there enough tests to cover the new functionality?
* Is the solution the right one for your codebase? Does it introduce any duplication, and does the abstractions match what you'd expect?

__Don't be petty__. If it's a matter of opinion or taste, avoid commenting and take it offline instead.

__Agree on how to introduce new members to the team.__ A wall text in your first code review makes for an appaling first impression.

__Don't keep scores for individuals.__ This may seriously lower the team morale.

__Use a code review tool__. It helps you keep track of code, comments and progress, and can help you set up the workflow you want without letting it become a burden. I would recommend [Gerrit](https://www.gerritcodereview.com) as such a tool, provided you don't have access to the excellent [GitHub](github.com/) pull requests or similar.

### For submitters

* Make your commits small and frequent
* Provide context for the commit
* Create a personal checklist with your most common mistakes
* Make sure to use the checklist yourself first
	* The code review should catch mistakes, not be an autocorrect feature.

### For reviewers

* Use the checklist, let tools do the rest
* Review often and for short sessions
