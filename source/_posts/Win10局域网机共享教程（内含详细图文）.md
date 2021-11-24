---
title: Win10局域网机共享教程（内含详细图文）
top: false
cover: false
toc: true
mathjax: true
date: 2021-06-30 23:13:37
password:
summary:
tags: 教程
categories: 打印机
---

### Win10局域网机共享教程（内含详细图文）

本文将详细介绍Win7下如何实现同个局域网内共享机。经测试，Win10/Win7/XP之间均可正常连接。

**第一步：取消禁用Guest用户**

1. 点击【开始】按钮，在【计算机】上右键，选择【管理】，如下图所示：

![image-20210630224804060](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630224804060.png)

2. 在弹出的【计算机管理】在本地用户和组列表中找到【Guest】用户，如下图所示：

![image-20210630224841758](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630224841758.png)

3. 双击【Guest】，打开【Guest属性】窗口，确保【账户已禁用】选项没有被勾选，如下图：

![image-20210630224906839](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630224906839.png)

**第二步：共享目标打印机**

1. 快捷键【win I】，选择【设备】，选择设备与打印机，如下图：

![image-20210630224931869](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630224931869.png)

![image-20210630225028057](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225028057.png)

2. 在弹出的窗口中找到想共享的打印机（前提是打印机已正确连接，驱动已正确安装），在该打印机上右键，选择【打印机属性】，如下图：

![image-20210630225057126](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225057126.png)

3. 切换到【共享】选项卡，勾选【共享这台打印机】，并且设置一个共享名（请记住该共享名，后面的设置可能会用到），如下图：

![image-20210630225123914](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225123914.png)

**第三步：进行高级共享设置**

1. 在右下角系统托盘的网络连接图标上右键，选择【打开网络和共享中心】，如下图：

![image-20210630225218318](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225218318.png)

2. 单击列表中的【更改高级共享设置】，如下图：

![image-20210630225246235](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225246235.png)

3. 具体设置可参考下图，其中的关键选项已经用红圈标示，设置完成后不要忘记保存修改。

![image-20210630225306913](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225306913.png)

![image-20210630225334666](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225334666.png)

注意：如果是工作或专用网络，具体设置和上面的情况类似，相应地应该设置选项，如下图：　

![image-20210630225354701](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225354701.png)

**第四步：设置工作组**

　　在添加目标打印机之前，首先要确定局域网内的计算机是否都处于一个工作组，具体过程如下：

1. 点击【开始】按钮，在【计算机】上右键，选择【属性】，如下图：

![image-20210630225414293](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225414293.png)

2. 在弹出的窗口中找到工作组，如果计算机的工作组设置不一致，请点击【更改设置】；如果一致可以直接退出，跳到第五步。

　　注意：请记住【计算机名】，后面的设置会用到。



![image-20210630225652231](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225652231.png)

**win10更新后在这里**

![image-20210630225606238](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225606238.png)

![image-20210630225638892](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225638892.png)

3. 如果处于不同的工作组，可以在此窗口中进行设置：

![image-20210630225821540](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225821540.png)

注意：此设置要在重启后才能生效，所以在设置完成后不要忘记重启一下计算机，使设置生效。

**第五步：在其他计算机上添加目标打印机**

　　注意：此步操作是在局域网内的其他需要共享打印机的计算机上进行的。此步操作在Win7和XP系统中的过程是类似的，本文以Win10为例进行介绍。

　　添加的方法有多种，在此为小编只介绍两种。

　　首先，无论使用哪种方法，都应先进入【控制面板】{（Win X） P}，打开【设备和打印机】窗口，并点击【添加打印机】，如下图：

![image-20210630225847013](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225847013.png)

系统会自动搜索可用的打印机。

　　如果前面的几步设置都正确的话，那么只要耐心一点等待，一般系统都能找到，接下来只需跟着提示一步步操作就行了。

　　原谅小编机器也没找到...可直接点击【我所需的打印机未列出】，然后点击【下一步】，如下图：

![image-20210630225911685](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225911685.png)

　接下来的设置就有多种方法了。

　　第一种方法：

　　1. 选择【按名称选择共享打印机】，点击【下一步】，如下图：

![image-20210630225928590](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225928590.png)

2. 找到连接着打印机的计算机，点击【选择】，如下图：

![image-20210630225947497](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630225947497.png)

3. 选择目标机器（打印机名就是在第二步中设置的名称），点击【选择】，如下图：

![image-20210630230005463](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230005463.png)

接下来的操作比较简单，系统会自动找到并把该打印机的驱动安装好。至此，打印机已成功添加。

　　**第二种方法：**

　　1.  在【添加打印机】窗口选择【按名称选择共享打印机】，直接输入“\计算机名\打印机名”（计算机名和打印机在上文中均有提及，不清楚的朋友往上翻）。如果前面的设置正确的话，当还输入完系统就会给出提示（如下图）。

　　接着点击【下一步】。

![image-20210630230023632](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230023632.png)

注意：如果此步操作中系统没有自动给出提示，那么很可能直接点击【下一步】会无法找到目标打印机，此时我们可以把“计算机名”用“IP”来替换，如下：

　　例如小编主机IP为192.168.21.170，那么则应输入“\\192.168.21.170\Sharp MX-M350U PCL 6”。查看系统IP的方法如下：

1.1 系统托盘【网络】图标上右键，选择【打开网络和共享中心】，如下图：

![image-20210630230051514](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230051514.png)

1.2 在【网络和共享中心】找到【本地连接】，单击，如下图：

![image-20210630230108796](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230108796.png)

1.3 在弹出的【本地连接 状态】窗口中点击【详细信息】，IPv4 地址就是本机的IP地址。

![image-20210630230125452](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230125452.png)

当然你也可以直接通过快捷键“win R—>cmd—>ipconfig/all”来查看。

2. 接下来继续前面的步骤，和第一种方法一样，系统会找到该设备并安装好驱动，只需耐性等待即可（如下图）。

![image-20210630230147231](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230147231.png)

3. 接着系统会给出提示，告诉用户打印机已成功添加，直接点击【下一步】，如下图：

![image-20210630230205106](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230205106.png)

4. 至此，打印机已添加完毕，如有需要用户可点击【打印测试页】，测试一下打机是否能正常工作，也可以直接点击【完成】退出此窗口，如下图：![image-20210630230225195](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230225195.png)

成功添加后，在【控制面板】的【设备和打印机】窗口中，可以看到新添加的打印机，如下图：

![image-20210630230301813](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210630230301813.png)

至此，整个过程均已完成，没介绍的其他方法（使用TCP/IP地址或主机名添加打印机）也比较简单，过程类似，这里不想赘述。

　　如果有朋友在第四步的设置中无法成功，那么很有可能是防护软件的问题，可对防护软件进行相应的设置或把防护软件关闭后再尝试添加。

　　最后，希望本文对壳粉们有所帮助。

　　PS：有不明白或遇到问题的朋友可以给我留言，反正小编也不会回复你。

