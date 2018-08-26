---
layout: post
title: 手机刷入Nethunter
categories:
- blog
tags:
- kali
- 刷机
- nethunter
---

## 写这篇文章时回忆的过程中真是扎心，你可以想象一个慢性子+菜鸡属性的人1个星期刷了至少5次net hunter的痛苦吗。希望米娜桑入坑前避免重蹈我的覆辙。

### Ⅰ 必看

我掉进去的第一个坑就是netthunter对硬件和系统的要求上，求求你们刷机前先看看这个表格（[原链接](https://github.com/offensive-security/kali-nethunter/wiki)）。

我们先看有没有自己的机型（没有的话可以尝试刷个内核试试，博主专门入了个Nexus5X二手机来玩nethunter，这种系统装上去可能手机自身的安全性也会受到影响故不建议作为日常机，虽然本身安卓机除了谷歌大厂及时发布补丁基本没其他厂子那么关心漏洞问题），再看看手机的系统合不合适（不合适要刷进要求的）据说三星刷机就不保修了大大们自己掂量吧：

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

emmmm其实看这个感觉国外开发者们起名方式还是挺好玩的，Android系统都是甜点，像lollipop棒棒糖，nexus的不同版本名也都是一些很有既视感的造型。



