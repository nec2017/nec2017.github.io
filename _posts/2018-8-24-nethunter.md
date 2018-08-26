---
layout: post
title: 手机刷入Nethunter的常规操作
categories:
- blog
tags:
- kali安全
- 刷机
- nethunter
---

## 写这篇文章时回忆的过程真是扎心而且为什么会写得这么熟练啊，你可以想象一个慢性子+菜鸡属性的人1个星期刷了至少5次nethunter的痛苦吗。希望米娜桑入坑前避免重蹈我的覆辙。

  <audio autoplay="autoplay">
  <source src="/resources/Kali Linux NetHunter(TRY HARDER-UZIMON).mp3" />
  </audio>

### Ⅰ 必看

本文以<strong>Nexus5X</strong>为例（有一个很好的[英文指导视频](https://www.youtube.com/watch?v=XFmvn7_R9fs)在油管上）。我掉进去的第一个坑就是nethunter对硬件和系统的要求上，求求你们刷机前先看看我下面分享的这个表格（[原链接](https://github.com/offensive-security/kali-nethunter/wiki)）。

我们先看有没有自己的机型（没有的话可以去油管上查好像有的还支持奥利奥，博主专门入的二手机来玩nethunter，这种系统装上去可能手机自身的安全性也会受到影响故不建议作为日常机，虽然本身安卓机除了谷歌大厂及时发布补丁基本其他厂子没那么关心漏洞问题），再看看手机的系统合不合适（不合适要刷入要求的）据说三星刷机就不保修了，大大们自己掂量吧：

|                     Device                      |                   Android Version                   |                            Notes                             |
| :---------------------------------------------: | :-------------------------------------------------: | :----------------------------------------------------------: |
|                 Nexus 4 (mako)                  |               **5.1.1**   **CM 13.0**               |                                                              |
|              Nexus 5 (hammerhead)               | **5.1.1** or **6.0.1**   **CM 13.0** or **CM 14.1** |                                                              |
|               Nexus 5x (bullhead)               |                      **6.0.1**                      |                                                              |
|                 Nexus 6 (shamu)                 |               **5.1.1** or **6.0.1**                |                                                              |
|                Nexus 6P (angler)                |               **6.0.1** or **7.1.1**                |                                                              |
|               Nexus 7 2013 (flo)                |        **5.1.1** or **6.0.1**   **CM 13.0**         |                                                              |
|               Nexus 9 (flounder)                |               **5.1.1** or **6.0.1**                |                                                              |
|                Nexus 10 (manta)                 |                      **5.1.1**                      |                                                              |
|             OnePlus One (oneplus1)              |               **CM 12.1** or **13.0**               |                     Our preferred device                     |
|              OnePlus 2 (oneplus2)               |               **CM 12.1** or **13.0**               |                                                              |
|            OnePlus 3 & 3T (oneplus3)            |               **6.0.1** or **7.0.0**                |              Unified build in 7.0.0 (OxygenOS)               |
|              OnePlus X (oneplusx)               |                     **CM 13.0**                     |                                                              |
|              Galaxy Note 3 (hlte)               |     **CM 12.1** or **13.0**   **TouchWiz 5.0**      |                                                              |
|                Galaxy S5 (klte)                 |  **LineageOS 14.1**   **TouchWiz 5.1** or **6.0**   |                                                              |
|               Galaxy S7 (herolte)               |                 **TouchWiz 6.0.1**                  |               **Warning**: Exynos models only!               |
|            Galaxy S7 edge (hero2lte)            |                 **TouchWiz 6.0.1**                  |               **Warning**: Exynos models only!               |
|              LG G5 T-Mobile (h830)              |                      **7.0.0**                      |                                                              |
|           LG G5 International (h850)            |                      **7.0.0**                      |                                                              |
|             LG V20 T-Mobile (h918)              |                      **7.0.0**                      | **Warning**: Requires exploit on v10d firmware to unlock flashing! |
|           LG V20 US Unlocked (us996)            |                      **7.0.0**                      | **Warning**: US Cellular branded US996 is **not** unlocked!  |
|            HTC One M7 GPE (onem7gpe)            |                      **5.1.1**                      |                     Google Play Edition                      |
|               HTC 10 (htc_pmewl)                |                      **6.0.1**                      |                                                              |
|              Sony Xperia ZR (dogo)              |                      **6.0.1**                      |                                                              |
|              Sony Xperia Z (yuga)               |                      **6.0.1**                      |                                                              |
| SHIELD tablet (shieldtablet)   SHIELD tablet K1 |               **6.0.1**   **CM 13.0**               |                                                              |
|              ZTE Axon 7 (ailsa_ii)              |                      **6.0.1**                      | [@jcadduono](https://github.com/jcadduono)'s preferred device |

emmmm其实看这个感觉国外开发者们起名方式还是挺好玩的，Android系统都是甜点，像lollipop棒棒糖，据说9.0出来了叫pie，nexus的不同版本名也都是一些很有既视感的造型。

## Ⅱ 原料下载

这里我给大家放个[百度云链接](https://pan.baidu.com/s/1Bnf7nvMKd_J9CIFi9dXmdg)（密码:mjhy，里面包含我们需要的工具和我自己用到的nethunter文件和安卓系统）。

* [nethunter](https://www.offensive-security.com/kali-linux-nethunter-download/)
* adb
* fastboot
* supersu
* twrp
* nexus root tookit installing（傻瓜式操作好助手，可以不用，文章第一句话我分享的油管视频就是用的这个，但它也会存在一些问题所以本次我不介绍。)

## Ⅲ 适配系统

nethunter大概是在16年推出或者火起来的，所以这里面很多系统版本不适配的话就要刷回去，注意<strong>备份</strong>，由于我的机子没有东西就可以随便搞，如果是nexus或pixel手机我比较推荐谷歌的[系统源](https://developers.google.com/android/ota)，先点击acknowledged，然后找到自己的型号下载，我的是bullhead6.0.1（下载的bullhead-ota-mtc20f-6303e5cd.zip）。

Nexus在关机状态同时长按“电源键”和“音量减小键”应该能进入fastboot mode模式，我们就能看到一个被打开的安卓小人，用音量键调整我们下一步要进入的模式。

我们把它用数据线（说到数据线不得不感谢我的小伙伴蒋某(等我问问看看能不能放他友链过来)在我手机数据线快递还没送到时慷慨地随时借我乱搞😂）连上电脑，没错又要用win系统，用fastboot把twrp镜像刷入（bullhead建议用我分享的那个3.2.2的文件）：

```powershell
fastboot flash recovery .\twrp-3.2.2-0-bullhead.img
```



然后我们按音量键到recovery mode，感觉就像pe软件一样，进入后该输密码输密码我们就可以备份和刷系统了。

我记得我当时是把系统搞崩了然后wipe然后点击install，下面有两种方法install：

①

电脑端cd到要刷入的系统zip所在文件夹，然后：

```powershell
adb sideload .\bullhead-ota-mtc20f-6303e5cd.zip
```

静待其刷完，最后reboot就好，当然了开机可能有有一堆设置等着你，不过并不麻烦。

②

把zip文件在电脑端复制到手机的存储空间中，再点手机的install选项选中安装。

## Ⅳ 解锁bootloader和root

进入系统设置->关于手机->拉到最后点击7次左右版本号进入开发者模式->返回系统设置->进入开发者选项->开启开发者模式->选择OEM解锁

