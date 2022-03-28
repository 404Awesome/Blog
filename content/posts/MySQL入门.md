---
title: MySQL入门
toc: true
date: 2020-05-30 16:08:40
tags: ['MySQL']
---

# MySQL 简介

1. MySQL 由瑞典 MySQL AB 公司开发，目前属于 Oracle 公司
2. MySQL 是一个开源的关系型数据库管理系统
3. MySQL 分为社区版和企业版



# MySQL 安装

## 下载

> 推荐使用 <a href='http://mirrors.163.com/' target='_blank'>mirrors.163.com</a> 网易镜像站下载



## 安装方式

1. MSI 安装 (Windows Installer)
2. ZIP 安装
2. HomeBrew安装(Mac Installer)



### 一. MSI 方式

#### 安装简介

1. 安装简单
2. 通过可视化页面进行操作
3. 适合 Windows install

#### 安装方式

1. 下载 / 打开

2. 选择安装类型
   1. 典型安装
   2. 自定义安装
   3. 完全安装
3. 安装服务

4. 点击添加到环境变量

5. 设置端口号 / 用户名 / 密码



### 二. ZIP 方式

#### 安装简介

1. 需自行添加环境变量
2. 需自行安装数据库服务
3. 需自行配置

#### 安装方式

1. 下载解压
2. 配置文件
3. 配置环境变量
4. 安装服务 / 启动
5. 配置用户名与密码



### 三. HomeBrew 安装

1. 安装 MySQL 之前需安装 HomeBrew
2. 终端输入 brew install mysql
3. 接着输入 brew services start mysql
4. MySql 服务就启动了

