---
layout: post
title: 【翻译】自底向上学习SMB和Samba
categories:
- blog
tags:
- 安全
---

在这篇教程我们将介绍服务器报文块协议（Server Message Block或SMB）。尽管大多数人听说过这个缩略词（指SMB），但极少数人真正地理解这个重要的协议。SMB可能是通信协议中最难理解的协议了，但它对于网络的流畅运作非常重要，这是安全的特点。

### 什么是SMB

服务器报文块协议（Server Message Block，后文均称SMB）是七层协议中应用层的一个协议，广泛地应用于文件、端口、命名管道和共享打印机。它是C-S（客户端-服务器）型的通信协议，可以使用户（users）和应用程序通过局域网分享资源。如果某个电脑有个其他电脑需要读写等进行文件操作的文件，此时SMB能让用户与其他用户分享文件。此外，SMB还能让你在局域网分享打印机。

在TCP/IP上的SMB占用445端口。

![img](https://static.wixstatic.com/media/6a4a49_81989ac6050f43889aedd310bfb9dfcf~mv2.jpg/v1/fill/w_506,h_499,al_c,lg_1,q_80/6a4a49_81989ac6050f43889aedd310bfb9dfcf~mv2.webp)

SMB为C-S型的有请求和响应的协议。下图展示了这个协议请求-响应的方式。客户端通过TCP/IP或NetBIOS连接服务器。一旦两者建立连接，客户端就能发送指令来获取分享、读写文件和获取打印机。通常SMB能使客户端做任何人们在自己电脑系统做的事，但必须有网（废话(￣_￣|||)）。

![img](https://static.wixstatic.com/media/6a4a49_b032065c98bb4594b4a281823fe8e30d~mv2.jpg/v1/fill/w_577,h_586,al_c,lg_1,q_80/6a4a49_b032065c98bb4594b4a281823fe8e30d~mv2.webp)

SMB最开始在20世纪80年代被IBM公司开发出来，后来微软采用了这个协议并让它适配于Windows操作系统。

### CIFS

CIFS（Common Internet File System，通用Internet文件系统）和SMB经常被新手甚至网络安全专业人士搞混。CIFS代表“Common Internet File System”，是SMB协议的一种形式、一种特殊的实现，被微软开发并应用于其早期的操作系统。

现在CIFS协议逐渐被废弃因为它被更多现代化的SMB（包括2006年Windows Vista引进的SMB2.0、2012年Win8和Windows Server 2012引进的SMB3.0）的实现方法取代。

### 弱点

以前Windows上的SMB和Linux/Unix系统上的Samba是操作系统严重弱点的主要来源，很可能以后也是。过去十年最严重的Windows弱点中有两个是SMB弱点，包括MS08-067和NSA开发的最近的“永恒之蓝”漏洞利用。这两种漏洞利用都使攻击者可以向目标系统的SMB发送特制的数据包并执行远程代码提权。也就是说，有了这些漏洞，攻击者可以拿到任何系统的权限想做什么做什么。

想了解更多“永恒之蓝”通过Metasploit在Win7系统的的利用，可以看原作者的[教程](https://www.hackers-arise.com/single-post/2017/06/12/Metasploit-Basics-Part-8-Exploitation-with-EternalBlue)。此外，通过使用Metasploit攻击者还可以伪造一个假SMB服务器来捕获相关证书。

还有，SMB在Linux/Unix的使用——Samba，同样存在自身的问题。

尽管不是这些弱点和漏洞的完整清单，但当我们在Metasploit5找smb漏洞时我们还是找到了比较详细的以下列表。

![img](https://static.wixstatic.com/media/6a4a49_a874de57645a4ceb9930d680f540630e~mv2.png/v1/fill/w_1040,h_579,al_c,q_85,usm_0.66_1.00_0.01/6a4a49_a874de57645a4ceb9930d680f540630e~mv2.webp)

注意这个被标注的臭名昭著的MS08-067漏洞给百万多的Windows Server 2003、Windows XP和更早的系统带来安全威胁。在列表最下面你可以看到NSA过去威胁无数系统的“永恒之蓝”漏洞（MS17-010），在这个漏洞被Shadowbrokers泄露之后它被Petya和WannaCry等勒索软件利用。

在原网站网络取证部分，原作者详细分享了对抗Win7系统SMB的“永恒之蓝”漏洞的协议包层次。

![img](https://static.wixstatic.com/media/6a4a49_c0ca3c8f8dad40db8c3cf2d3d5eeda4f~mv2.png/v1/fill/w_1040,h_623,al_c,q_85,usm_0.66_1.00_0.01/6a4a49_c0ca3c8f8dad40db8c3cf2d3d5eeda4f~mv2.webp)

### Samba

SMB最初被IBM开发然后被微软采用，而Samba被开发用于Linux/Unix系统来效仿Windows服务器。Samba使能够像Windows系统一样把资源分享给Windows系统。

![img](https://static.wixstatic.com/media/6a4a49_1a39e752fd5f4ea09f194d9839e30803~mv2.png/v1/fill/w_788,h_581,al_c,q_85,usm_0.66_1.00_0.01/6a4a49_1a39e752fd5f4ea09f194d9839e30803~mv2.webp)

有时候理解协议或系统的最好方式很简单，就是自己亲自把它们安装部署一遍。

