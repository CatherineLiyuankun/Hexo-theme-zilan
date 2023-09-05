---
title: 'Chrome116 chromedriver 下载及配置 '
catalog: true
date: 2023-09-04 14:41:49
subtitle: 踩坑
header-img:
tags:
---

## chromedriver 116 版本下载

- 老版本下载（<=114）： <https://chromedriver.chromium.org/downloads>
- 新版本下载: <https://googlechromelabs.github.io/chrome-for-testing/>
  - 具体步骤可参考文章： [Chrome116驱动下载路径 解决版本不匹配问题](https://www.cnblogs.com/wuxianfeng023/p/17650789.html)

新版本下载后是`Google Chrome for Testing.app`， 官网介绍[Chrome for Testing: reliable downloads for browser automation](https://developer.chrome.com/blog/chrome-for-testing/)

## chromedriver 环境变量配置

我下载的版本是： [116 mac-arm64](https://edgedl.me.gvt1.com/edgedl/chrome/chrome-for-testing/116.0.5845.96/mac-arm64/chrome-mac-arm64.zip)

- 下载后`chrome-mac-arm64.zip`解压为：`/chrome-mac-arm64/Google Chrome for Testing.app`
- 在`/usr/local`下新建文件夹`chromedriver`
- 移动文件`Google Chrome for Testing.app`到`/usr/local/chromedriver`
- 懒得空格转义，就把`Google Chrome for Testing.app`改名为`chromedriver.app`， 所以得到`/usr/local/chromedriver/chromedriver.app`
  - `/usr/local/chromedriver/chromedriver.app/Contents/MacOS/Google Chrome for Testing.app`也改名为
`chromedriver.app`， ， 所以得到`/usr/local/chromedriver/chromedriver.app/Contents/MacOS/chromedriver`

<!-- - 在`~/.bash_profile` 配置了`export PATH="$PATH:/usr/local/chromedriver"`， 并且`source ~/.bash_profile`。 -->
  <!-- - 在命令行输入 chromedriver不管用 -->
```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

# 指定Chromedriver的路径
driver_path = '/usr/local/chromedriver/chromedriver.app/Contents/MacOS/chromedriver'

# 创建一个Chrome WebDriver实例
driver = webdriver.Chrome(executable_path=driver_path)

url = 'https://www.baidu.com'
driver.get(url)
```

这时候执行，chromedriver可以启动chrome窗口，但是无法打开页面'https://www.baidu.com', 然后报错：

```
    driver = webdriver.Chrome(executable_path=driver_path)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "~/anaconda3/lib/python3.11/site-packages/selenium/webdriver/chrome/webdriver.py", line 73, in __init__
    self.service.start()
  File "~/anaconda3/lib/python3.11/site-packages/selenium/webdriver/common/service.py", line 104, in start
    raise WebDriverException("Can not connect to the Service %s" % self.path)
selenium.common.exceptions.WebDriverException: Message: Can not connect to the Service /usr/local/chromedriver/chromedriver.app/Contents/MacOS/chromedriver
```

## 踩坑

### “Google Chrome for Testing.app” is damaged and can’t be opened. You should move it to the Trash."

提示程序含有恶意代码或者已经打开所有来源还是提示扔到垃圾桶

Google Chrome for Testing.app官方解决方法： <https://github.com/GoogleChromeLabs/chrome-for-testing#macos-says-the-app-is-damaged-what-now>

在终端输入 `sudo xattr -cr 'Google Chrome for Testing.app'`

## [WebDriverManager setup failing to download chromedriver 116](https://stackoverflow.com/questions/76932496/webdrivermanager-setup-failing-to-download-chromedriver-116)

