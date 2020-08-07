---
layout: post
title: 免费就是麻烦，记七牛云数据迁移
categories:
- blog
tags:
- 七牛云
- cmd
- powershell
- 博客运维
---

## 太久没更新博客🌶，出来炸个尸。害，由于我的博客图片只要不是引用的其他外链都是存放在七牛云上的，但他提供的存储服务单次只帮我存放一个月，所以每个月都需要新开通服务进行数据迁移，但是大多我都会等这个过期了都没有进行迁移，所以据我所知似乎只用通过命令行来执行数据在bucket之前复制的命令。

### qshell在win10平台下的数据迁移操作

qshell是七牛云自己用go语言开发的七牛云服务命令行操作工具，官方文档与下载地址：[https://developer.qiniu.com/kodo/tools/1302/qshell](https://developer.qiniu.com/kodo/tools/1302/qshell)

关于除了数据迁移以外的操作，其他操作命令、在qshell程序旁边有readme.md文件，非常详细地介绍了使用方法，比俺的blog写得专业多了。

废话不多说，show myself（根本没有人康我的blog啦） the code：

```powershell
cd qshll所在目录
#如果是初次使用未登录，先在七牛云网页查看个人中心-->密钥管理，执行
.\qshell-windows-x64.exe account AK SK
.\qshell-windows-x64.exe listbucket2 待迁移的bucket名称 list.txt
.\qshell-windows-x64.exe batchcopy 待迁移的bucket名称 目标bucket名称 -i list.txt
```

照做就大功告成啦。

大概过几天有时间会写个python脚本辅助完成。







