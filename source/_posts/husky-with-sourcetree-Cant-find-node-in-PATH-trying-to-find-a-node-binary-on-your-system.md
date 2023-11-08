---
title: >-
  husky with sourcetree Cant find node in PATH, trying to find a node binary on
  your system
catalog: true
date: 2023-11-08 18:46:18
subtitle:
header-img:
tags:
- git
categories:
- TECH
- Tools
- Environment setup
---

如果在 git GUI 软件, 例如sourcetree遇到 `pre-commit` / `pre-push` 报错找不到 yarn，可以参考这个 husky 的官方方案: <https://github.com/typicode/husky/issues/390#issuecomment-1082345670>

## Solution

- Create `~/.huskyrc` file in my home directory
- With this content:
如果使用`nvm`来管理node版本：

```bash
# Load Yarn command coming from homebrew
export PATH="/opt/homebrew/bin/:$PATH"

# This loads nvm.sh and sets the correct PATH before running hook
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

nvm use default
```

或者制定node版本：

```bash
export PATH="/opt/homebrew/bin/: $PATH"
export PATH="/opt/homebrew/opt/node@18/bin: $PATH"
```
