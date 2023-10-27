---
title: hexo deploy error with wrong git user
catalog: true
date: 2023-10-27 15:23:25
subtitle: Permission to yourGitUserName/yourGitUserName.github.io.git denied to xxx
header-img:
tags:
- Hexo
- Blog
categories:
- TECH
- Hexo
---

## error

```bash
$ hexo d
(node:52405) ExperimentalWarning: The fs.promises API is experimental
INFO  [hexo-math] Using engine 'mathjax'
INFO  DPlayer.min.css is not found in this version of dplayer, skip it.
INFO  Deploying: git
INFO  Clearing .deploy_git folder...
INFO  Copying files from public folder...
INFO  Copying files from extend dirs...
On branch master
nothing to commit, working tree clean
remote: Permission to yourGitUserName/yourGitUserName.github.io.git denied to anotherGitUserName.
fatal: unable to access 'https://github.com/yourGitUserName/yourGitUserName.github.io/': The requested URL returned error: 403
FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/docs/troubleshooting.html
Error: Spawn failed
    at ChildProcess.task.on.code (/Users/yuanli/GitRepos/LYKGit/Blog/Hexo-theme-zilan/node_modules/hexo-deployer-git/node_modules/hexo-util/lib/spawn.js:51:21)
    at ChildProcess.emit (events.js:189:13)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:248:12)
```

这个报错`remote: Permission to yourGitUserName/yourGitUserName.github.io.git denied to anotherGitUserName.`表明使用错了这个repo的username，`anotherGitUserName`是我另一个repo的用户名，所以解决方法是设置对username。

### 检查git config user.name

```bash
git config --global --list
git config --local --list
user.name=xxx
```

如果不正确，设置正确

```bash
git config --global user.name "XXX
git config --local user.name "XXX
```

发现还是不行，后来突然意识到这个设置的是hexo的这个repo使用的username, 而不是deploy到的那个repo的username

### 改变deploy到repo的username

修改hexo repo里面的`_config.yml`
Make sure your `_config.yml` file in your Hexo project contains the correct repository URL and branch information under the deploy section. For example:

```yaml
deploy:
  type: git
  repo: https://github.com/yourusername/yourusername.github.io.git
  branch: gh-pages
```

修改为：

```yaml
deploy:
  type: git
  repo: https://yourusername@github.com/yourusername/yourusername.github.io.git # 指定user
  branch: gh-pages
  token: $LYK_GIT_TOKEN
```

如果使用git token, 可以在[`_config.yml`指定token](https://hexo.io/zh-cn/docs/one-command-deployment.html#google_vignette)
> Token Authentication: If you are using a private repository or facing authentication issues, consider using a personal access token instead of your GitHub password. Generate a personal access token on GitHub and use it as the password when prompted. “令牌身份验证：如果您正在使用私有仓库或遇到身份验证问题，请考虑使用个人访问令牌代替您的 GitHub 密码。在 GitHub 上生成个人访问令牌，并在提示时将其用作密码。”