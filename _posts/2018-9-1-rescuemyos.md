---
layout: post
title: 记一次多系统电脑翻车及修复
categories:
- blog
tags:
- 多系统
- linux启动盘
- 引导修复
---

## 昨天想把一个电脑上的win7扩容，想增加C盘容量，发现多余的空闲空间与C盘不连续无法实现，于是准备新增一个D盘分区，发现主分区已经有6个了（别问我为什么，一个Debian一个Arch一个Win很好凑6个分区的），无法再增加分区了，电脑管理和Diskgenius都不管用，于是下了个分区助手（当时surface无法合并硬盘分区时就用的这个神器），这就是翻车的开始...

### Ⅰ 误清分区丢引导

好像当时用分区助手时没看仔细，把arch系统（我用的这个上的grub作为开机引导）的120个G给格式化了，准备重启看看是不是真翻车了，果不其然。

### Ⅱ 黑屏界面惹人恼

因为这个grub引导所在的系统被清空了，于是我们就进入了grub rescue的“清爽”界面，按照1、2年前我刚接触linux系统时我会果断放弃然后重装，但手头有事要用win7啊，不能就这样godie，总觉得还能抢救一下。

![screenshot1](http://pv8gr0ppd.bkt.clouddn.com/screenshot1.JPG)

先百度了下，发现了一篇很好的[博客](https://blog.csdn.net/weixin_39772481/article/details/79212364)，我大致再复述一遍这个思路：

``` bash
#查看已有设置
grub rescue> set 
#我目前的情况是arch系统被清的差不多了，也无法从外部访问，但是grub依然挂载再这个系统的分区上，我的显示结果是：
cmdpath=(hd0)
prefix=(hd0,msdos4)/boot/grub
root=hd0,msdos4
#到这，我们应该把prefix和root重新挂载到没受影响的系统，所以要查看现在的分区情况
grub rescue> ls
grub rescue> ls (hd0,msdos1)
grub rescue> ls (hd0,msdos2)
grub rescue> ls (hd0,msdos...)
#掀桌(╯‵□′)╯ 果然无图形化什么的让我心慌，只能看到文件系统的类别，这点信息不够啊
```

### Ⅲ U盘启动盼修复

感觉就要卡在上一步时，突然我灵光一现，能不能制作一个Linux的live启动盘用图形界面查看一下现在的各系统文件呢（我可真是个小机灵鬼）。手头没U盘，借的一个小伙伴的，感觉自己总是麻烦别人（逃。

于是我刻了kali-live进去，通过U盘启动，文件管理器可以查到其他分区界面如下(手残抖了别介意)：

![screeshot2](http://pv8gr0ppd.bkt.clouddn.com/s2.JPG)

同时我们也可以用自带的gparted分区工具查看，点进去发现我的/dev/sda6的boot/grub目录下本应有的<strong>grubx64.efi</strong>文件丢失刚好我在其他区有备份这个文件，便复制回去。

这个<strong>/dev/sda3</strong>就是我没受影响的Debian系统的根目录，<strong>/dev/sda6</strong>就是boot分区，<strong>/dev/sda7</strong>是我的home分区，好了现在找到了一个健康的linux并知道了他的分区情况。

### Ⅳ 重回grub终修好

重启进入刚刚吓人的grub修复界面：

```bash
#set设置
grub rescue> set prefix=(hd0,msdos6)/boot/grub
grub rescue> set root=hd0,sda3
grub rescue> insmod normal
grub rescue> normal
```

此时我们应该就能通过Debian的grub正常进入Debian系统了，但是你会发现上面grub修复时的设置只是暂时性的，后面重启还是grub修复界面，所以我们先选择Debian的修复模式。除此以外选择系统进入的列表里应该没有Win系统的标识。

于是，想起之前刚安装好black arch系统时，本机原有的Debian和Win系统引导都不见了，后来用了一个叫<strong>os-prober</strong>的软件包，可以自动扫描本机存在的其他系统，它便自动找回了Win系统的引导并添加到了grub界面。

一路下来不容易，每一步都小心谨慎，希望这篇文章能让我以后处理分区时引以为戒吧。



