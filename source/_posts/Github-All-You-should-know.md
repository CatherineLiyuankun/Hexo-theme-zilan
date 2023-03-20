---
title: Github All You should know
catalog: true
date: 2019-10-15 15:33:20
subtitle: "Assignees"
header-img:
tags:
- git
categories:
- TECH
- Tools
---

## Who is Assignees?

[ What do reviewer and assignee mean in pull request?](https://stackoverflow.com/questions/43617352/) 里的答案：
> For a pull request, you can now "request a review explicitly from collaborators, making it easier to specify who you'd like to review your pull request."
但是Assignees
Assignees, on the other hand, "clarify who is working on specific issues and pull requests."

> In sum, the difference is whether you'd like to ask someone to work on fixing an issue or contribute to a pull request (**assignee**), versus asking someone to quality check your work (**reviewer**).
Sources:
https://github.com/blog/2291-introducing-review-requests
https://help.github.com/articles/assigning-issues-and-pull-requests-to-other-github-users/

[ On GitHub, what's the difference between reviewer and assignee?](https://stackoverflow.com/questions/41087206/on-github-whats-the-difference-between-reviewer-and-assignee)里的答案：
> After discussing with several OSS maintainers, reviewers is defined as what the word supposed to be: to review (someone's code) and "assignee" has a looser definiton explained below.

> For "reviewer": someone you want to review the code. Not necessarily the person responsible for that area or responsible for merging the commit. Can be someone who worked on that chunk of code before, as GitHub auto-suggests.

> For "assignee": up to the project's team/maintainer what it means and there's no strict definition. It can be the PR opener, or someone responsible for that area (who is going to accept the PR after the review is done or just close it). It's not up to GitHub to define what it is leaving it open for project maintainers what fits best for their project.

> Previous answer:
Ok I'll go ahead and answer my own question.
> For PR of users with write-access: the Assignee would be the same person who opened the PR, and reviewer would replace the old assignee function (reviewing code), being this one someone of assignee choice.
> For PR of users without write-access (outside contributors): Someone with write-access would assign herself (or other write-priviledge member), to review the PR (Reviewer). Assignee is blank.
> For unfinished PR from outside contributors: the write-access member would take the unfinished work and assign for her. She will be responsible for finishing the task, being the Assignee. Since the main reason of PRs is reviewing changes, she would select some other people to review the changes.

总结下：
reviewer: 一般很好理解，就是来review你代码的人。可以是原来改过这段代码的人，负责这块代码的人或是负责merge代码的人。
Assignees: 其实，没有严格定义，可以具体看项目组怎么用这个选项。一般分两个场景
1. Pull request：创建pull request的人（这种在另一个组的时候用过，如果你是创建的人，可以指定自己），或者是负责merge代码的人（我们组是这么用的），或者就是当review/colse PR完后accept PR的人.
2. Issue：当你收到一个issue（通常不是你建的issue）， 你需要指定人来fix这个issue，就可以在Assignees填。

## Tip

### online editor

On github.com when you are viewing a repo or pull request you can press the . (period) key to browse the repo or PR in a VS Code-like editor running in your browser.
https://github.com/github/dev
https://www.youtube.com/watch?v=ywUZOOzLX3c

### tab indenting

Github show tab indenting as 8-letter long, this would:
- make code file mixes tab and spaces indenting looks ugly, you know we have some code repo with long history.
- consume more horizontal screen space when we review code on Github.
We can change this [setting](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-personal-account-settings/managing-your-tab-size-rendering-preference)


# Reference Links:
- [ On GitHub, what's the difference between reviewer and assignee?](https://stackoverflow.com/questions/41087206/on-github-whats-the-difference-between-reviewer-and-assignee) 
- [ What do reviewer and assignee mean in pull request? [duplicate]](https://stackoverflow.com/questions/43617352/what-do-reviewer-and-assignee-mean-in-pull-request?noredirect=1&lq=1) 
- [ 如何使用 Issue 管理软件项目？](http://www.ruanyifeng.com/blog/2017/08/issue.html) 
- [ 完善 GitHub Flow 最後一哩路 — Probot -Assignees 下拉選單](https://tech.hahow.in/%E5%AE%8C%E5%96%84-github-flow-%E6%9C%80%E5%BE%8C%E4%B8%80%E5%93%A9%E8%B7%AF-probot-d1cda24e4455) 
