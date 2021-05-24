---
title: Linux LVM 磁盘扩容
top: false
cover: false
toc: true
mathjax: true
date: 2018-08-16 12:29:32
password:
summary:
tags: Linux
categories: Linux
---


# LVM 的基本概念
### 物理卷 Physical volume (PV)
可以在上面建立卷组的媒介，可以是硬盘分区，也可以是硬盘本身或者回环文件（loopback file）。物理卷包括一个特殊的 header，其余部分被切割为一块块物理区域（physical extents）。

#### 卷组 Volume group (VG)
将一组物理卷收集为一个管理单元。

#### 逻辑卷 Logical volume (LV)
虚拟分区，由物理区域（physical extents）组成。

#### 物理区域 Physical extent (PE)
硬盘可供指派给逻辑卷的最小单位（通常为 4MB）。

# 磁盘操作相关命令
#### ``df -h``（查看挂载点）
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/5EF5AB70A7864D6CB778E29F1E49ECE8/1848)

#### `lvdisplay`（显示当前的 logical volume）
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/B46A16706BE84D7785ABDEDB2ABC8447/1850)

备注： 注意这里目前有两个，一个是文件系统所在的 volume，另一个是 swap 分区使用的 volume，当然，我们需要扩容的是第一个

#### `vgdisplay`（显示当前的 volume group）
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/28102956E5304EDB9F65AAB4B89F132A/1854)

# 开始 LVM 扩容
### 查看 fdisk
```
fdisk -l
```
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/8F4B442E5D8347AA80C023E193659953/1856)

因为这台机器默认开启了 LVM，所以目前有一个 ``extended ``分区和一个`` LVM`` 分区，并且他们是完全重叠的。这是因为，LVM 分区作为一个虚拟的分区，完全占用了这个 extended 分区，原理图见下：
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/53A82CC632A94D21A2599C391E79EA61/1858)

因此，现在需要做的就是将 extended partition (`sda2`) 扩展到最大，然后创建一个新的 LVM logical partition (`sda6`)，用它来填满 sda2

### 查看所有连接到电脑上的储存设备
```
disk -l |grep '/dev'
```
#### 1 块磁盘效果图
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/8E0985A5EA2C46C497CFC5DCB2EAD87B/1860)

2 块磁盘效果图（新增磁盘，尚未挂载）
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/8E87CFC5237D4B0A9E1A6A8805976569/1862)

### 创建 sdb 分区
```
fdisk /dev/sdb
n	# 新建分区
l	# 选择逻辑分区，如果没有，则首先创建扩展分区（p），然后再添加逻辑分区（硬盘：最多四个分区  P-P-P-P 或 P-P-P-E）

```
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/93D8E728C55248EE82F285D4F05CA1F6/1864)
```
回车
回车
回车
w	# 写入磁盘分区
```
### 格式化磁盘
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/892B518A557C4A0EB276B13C47321F53/1867)

```
mkfs -t ext4 /dev/sdb1
```
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/BA2F4D79A22C44E6BCFA5E65947028D4/1866)

### 创建 PV
```
pvcreate /dev/sdb1
```
### 查看卷组
```
pvscan
```
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/41E6D108CF2F44198EA424D347F7E837/1869)


### 扩容 VG
```
vgdisplay
```
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/706E617A0E414CD98E818626EB74198D/1871)
```
vgextend ubuntu-vg /dev/sdb1
```
### 扩容 LV
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/7679140594AB463E83101E4BC2C55CAA/1873)

![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/81FCD01AD5F64245BE31AABB7D422071/1875)
```
# 增加指定大小
lvextend -L +30G /dev/ubuntu-vg/root
# 按百分比扩容
lvextend -l +100%FREE /dev/ubuntu-vg/root
```
### 刷新分区
```
resize2fs /dev/ubuntu-vg/root
```

### 删除 unknown device
```
pvscan
vgreduce --removemissing ubuntu-vg
```
注意：不要卸载扩容的磁盘，可能出现丢失数据或是系统无法启动