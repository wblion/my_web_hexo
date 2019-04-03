---
title: 【持续更新原创】魔镜魔镜告诉我谁是世界上最美的人 树莓派diy魔镜第一弹
date: 2018-10-24 11:19:10
tags:
---





很高兴，您来到我的小屋，本人diy爱好者，小白，刚刚开始玩树莓派，希望前辈多多指教。前些日子使用树莓派，做一个魔镜。可以与镜子对话，聊天。 最近工作不是很忙，而且对魔镜有一些心得想法，决心从头开始搞一次，并记录下来。

先上旧版视频 http://www.365yg.com/a6385106114602713345/#mid=51880178041



## 准备原料

原子镜（单面透光的镜子 关键）

显示器（和原子镜差多大。可以稍小一点点）

木条（用来做镜框）

树莓派

sd卡（安装树莓派系统使用）

读卡器

音箱

麦克风

各种工具（锯子，角铁之类的）



## 安装树莓系统

### 准备：

##### 硬件：

树莓派（我是3 b+ 自带wifi版本省的在买一个WiFi了 价格190）

sd卡（我使用的是32g的因为要装很多库，尽量大一些的）

读卡器

音箱（推荐使用带线的，效果会比较好）

麦克风（我买个一个比较便宜的 usb接口）

##### 软件：

[Win32DiskImager v0.9.zip](http://sourceforge.net/projects/win32diskimager/files/Archive/win32diskimager-v0.9-binary.zip/download) ([sourceforge.net](http://sourceforge.net/projects/win32diskimager/))（烧录工具）

[SD Formatter 4.0 for SD/SDHC/SDXC](https://www.sdcard.org/downloads/formatter_4/)（sd卡格式化工具很好用）

[树莓派镜像RASPBIAN STRETCH WITH DESKTOP](https://www.raspberrypi.org/downloads/raspbian/)（树莓派镜像下载 ）

[PUTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)（后台ssh连接工具）

# 步骤



1 首先把使用读卡器把把sd插到电脑中去。使用 SDFormatter 4.0 for SD 把sd格式化

![](\img\mojing\sdfrom.jpg)

2 使用[Win32DiskImager 镜像工具把镜像写入到sd卡中。选择刚才下好的镜像，点击write。

![](\img\mojing\win32diskmager.png)

3 等待几分钟后，显示success 即完成，先不要忙着拔掉读卡器，还需要，制作开启ssh不然没有版本从后台连接。现在应该出现了一个boot 盘符。我们需要在这个盘符下，建立一个名字为ssh的文件夹，这个树莓派就会在通电开机后打开ssh了，之后我们就可以趁虚而入了。哈哈哈。

![](\img\mojing\boot.jpg)

4 完成之后就拔下sd 卡插入树莓派中，然后连接网线，电源线，鼠标键和键盘（有的话），显示器。之后通电，系统安装完成。





啥还没听明白

关门！上视频

http://www.365yg.com/a6614395796592787982/#mid=51880178041

待续。。。。 转载请注明出处。

共享交流群 14580005 一起用脑洞改变世界。相互研究帮助。 这是为了保证群成员质量和活性。需要收费3元请大家理解。



<iframe src="https://github.com/wblion/wblion.github.io/donate_page/simple/" style="overflow-x:hidden;overflow-y:hidden; border:0xp none #fff; min-height:240px; width:100%;"  frameborder="0" scrolling="no"></iframe>