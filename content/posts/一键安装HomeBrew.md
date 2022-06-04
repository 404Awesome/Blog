---
title: 一键安装HomeBrew
toc: true
date: 2022-03-15 21:03:05
tags: ['Mac', 'HomeBrew']
---

### 项目地址

> 项目地址Gitee：<a href="https://gitee.com/cunkai/HomebrewCN" target="_blank">点击访问</a>



### 一键安装HomeBrew

> 苹果电脑标准安装脚本:（推荐 优点全面 缺点慢一点）

```sh
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

> 苹果电脑极速安装脚本:（优点安装速度快 缺点update功能需要命令修复 ）

```shell
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)" speed
```

> Linux 标准安装脚本：

```shell
rm Homebrew.sh ; wget https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh ; bash Homebrew.sh
```



### 一键卸载HomeBrew

> 苹果电脑卸载脚本：

```shell
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/HomebrewUninstall.sh)"
```

> Linux卸载脚本：

```shell
rm HomebrewUninstall.sh ; wget https://gitee.com/cunkai/HomebrewCN/raw/master/HomebrewUninstall.sh ; bash HomebrewUninstall.sh
```

