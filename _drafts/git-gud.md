---
layout: post
title:  "Git gud"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## Common issues

Git is a wonderful tool. It does take some getting used to though, and it's easy to end up in . If you're still stuck pasting around commands and hoping they do what you think, this post may be for you.

### Large merge conflicts 

Most large merge conflicts are caused by merging updates too seldom. "If it hurts, do it more often" to quote the well known mantra of continuous delivery advocates. The root cause is often having a rigid verification process revolving around release versioning and quality assurance environments. This fits well with selecting a clunky branching strategy like [Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow), usually leading to long release cycles and big merging points. If you feel this hits home with your situation, I'd suggest reading up on [continuous delivery](), [DevOps]() and [GitHub flow](). 

In other cases, this is caused by accidentally rewriting history. Anyone versed in time travel knows that is a terrible idea, and in git it's often translated to "rebase everything". [The golden rule of rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) is to _never_ do it on a public branch.