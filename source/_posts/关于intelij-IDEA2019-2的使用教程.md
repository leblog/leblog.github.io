---
title: 关于intelij IDEA2019.2的使用教程
top: false
cover: false
toc: true
mathjax: true
date: 2018-05-02 21:43:03
password:
summary:
tags: [Intelij IDEA,学习笔记]
categories: IDEA
---



## 前言
>工欲善其事
必先利其器

同时，在这次分享之后，本人自己也学习到了一些新的使用技巧，所以借着这次机会，一起分享出来。希望可以帮到一些人，不能浪费IDEA这个优秀的IDE呀。

>基于的 IDEA 版本信息：IntelliJ IDEA 2019.2版本
## 知识点概览：


 - 高效率配置

 - 日常使用 必备快捷键（★★）
	


	- 查找

	- 跳转切换

	- 编码相关

	- 代码阅读相关

	- 版本管理相关

- 编码效率相关（★★）

	- 文件代码模板

	- 实时代码模板

	- 其他
- 代码调试 源码阅读相关（★★★）

	- 视图模式

	- 代码调试

	- ...
- 插件方面

	- 插件的安装与使用

	- 插件推荐

- 参考
<hr/>

 ## 标题高效率配置
 
 1. 代码提示不区分大小写
 
 Settings -> Editor -> General -> Code Completion
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNPaWJub0V0dVNpYVVhRjdjblRyanFjbWlhZHBEdHJwcXEwYlV1SHNvMUx5WlZJbElCMUwyeEJwckEvNjQw?x-oss-process=image/format,png)
 (低版本 将 Case sensitive completion 设置为 None 就可以了)

2. 自动导包功能及相关优化功能

Settings -> Editor -> General -> Auto Import
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNuYmg2bjVSOTF2eUI3a05XZkZyd2tQNDJhQm1GcFdvRWQ1dnp2OGlia1I0WHZDbTFOQ1lUNUhnLzY0MA?x-oss-process=image/format,png)
3. CTRL + 滑动滚轮 调整窗口显示大小

Settings -> Editor -> General -> Change font size (Zoom) with Ctrl+Mouse wheel

![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNMNWJRVkZtRzl0RG9vU3hSY3ppYnpveU5PZWtNTHhWTFg3RHFYRGYzeXR2SlVsWGZMaWFuaWJOeEEvNjQw?x-oss-process=image/format,png)

选择之后，就可以通过CTRL+滑动滚轮的方式，调整编辑器窗口的字体大小
 	 	
4.tab 多行显示

这点因人而异，有些人喜欢直接取消所有tab，改用快捷键的方式，我屏幕比较大，所以喜欢把tab全部显示出来。

Window -> Editor Tabs -> Tabs Placement，取消勾选 Show Tabs In Single Row选项。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnN3VWNBemxpY016NGVpY2s1YW9ZUGtjcVRWcWVqbjQzZDM0NmpraWI3UkZ3VXBINlYySzcxRGdGQWcvNjQw?x-oss-process=image/format,png)
效果如下：

![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy96Nzl5SWJHQkVRQnNBZmo2WU9JMlNqdExKZHQzMnBkMzZqQUNMWGd0ODdoc0Zzd2liOURFaWNqanlJODFlOFRzYkF0djVpY3B4aWJkdEF0MlJyN0ZOTlhpYVFBLzY0MA?x-oss-process=image/format,png)
5.  代码编辑区显示行号
Settings -> Editor -> General -> Appearance 勾选 Show Line Numbers

![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnM5cmJ1NUpIREtVM1RJcjZmWFVFVEw0aWNUR0NpYzBOZW9zRFRubVlPakpxdld4N1FpYkt1Nm5PSkEvNjQw?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNob2FRSGJWcnlHTmdSS2Z3VW9BejZWaWJ0S0dxSlBZUmoxVE1tTTdMa3VPRTFUMTg1bEw4a0R3LzY0MA?x-oss-process=image/format,png)
<hr/>

## 日常使用 必备快捷键（★★）
查找
| 快捷键                       | 介绍                |
|---------------------------|-------------------|
| Ctrl \+ F                 | 在当前文件进行文本查找       |
| Ctrl \+ R                 | 在当前文件进行文本替换       |
| Shift \+ Ctrl \+ F        | 在项目进行文本查找         |
| Shift \+ Ctrl \+ R        | 在项目进行文本替换         |
| Shift  \+ Shift           | 快速搜索              |
| Ctrl \+ N                 | 查找class           |
| Ctrl \+ Shift \+ N        | 查找文件              |
| Ctrl \+ Shift \+ Alt \+ N | 查找symbol（查找某个方法名） |

跳转切换

| 快捷键                 | 介绍            |
|---------------------|---------------|
| Ctrl \+ E           | 最近文件          |
| Ctrl \+ Tab         | 切换文件          |
| Ctrl  \+ Alt \+ ←/→ | 跳转历史光标所在处     |
| Alt \+ ←/→ 方向键      | 切换子tab        |
| Ctrl \+ G           | go to（跳转指定行号） |

编码相关
| 快捷键                           | 介绍                                                |
|-------------------------------|---------------------------------------------------|
| Ctrl \+ W                     | 快速选中                                              |
| \(Shift \+ Ctrl\) \+ Alt \+ J | 快速选中同文本                                           |
| Ctrl \+ C/Ctrl \+ X/Ctrl \+ D | 快速复制或剪切                                           |
| 多行选中 Tab / Shift  \+ Tab      | tab                                               |
| Ctrl \+ Y                     | 删除整行                                              |
| 滚轮点击变量/方法/类                   | 快速进入变量/方法/类的定义处                                   |
| Shift \+ 点击Tab                | 快速关闭tab                                           |
| Ctrl \+ Z 、Ctrl \+ Shift \+ Z | 后悔药，撤销/取消撤销                                       |
| Ctrl \+ Shift \+ enter        | 自动收尾，代码自动补全                                       |
| Alt \+ enter                  | IntelliJ IDEA 根据光标所在问题，提供快速修复选择，光标放在的位置不同提示的结果也不同 |
| Alt \+ ↑/↓                    | 方法快速跳转                                            |
| F2                            | 跳转到下一个高亮错误 或 警告位置                                 |
| Alt \+ Insert                 | 代码自动生成，如生成对象的 set / get 方法，构造函数，toString\(\) 等    |
| Ctrl \+ Shift \+ L            | 格式化代码                                             |
| Shift \+ F6                   | 快速修改方法名、变量名、文件名、类名等                               |
| Ctrl \+ F6                    | 快速修改方法签名                                          |

代码阅读相关

| 快捷键                        | 介绍                   |
|----------------------------|----------------------|
| Ctrl \+ P                  | 方法参数提示显示             |
| Ctrl \+ Shift \+ i         | 就可以在当前类里再弹出一个窗口出来    |
| Alt \+ F7                  | 可以列出变量在哪些地方被使用了      |
| 光标在子类接口名，Ctrl \+ u         | 跳到父类接口               |
| Alt \+ F1 \+ 1， esc        |
| \(Shift\) \+ Ctrl \+ \+/\- | 代码块折叠                |
| Ctrl \+ Shift \+ ←/→       | 移动窗口分割线              |
| Ctrl  \+ \(Alt\) \+ B      | 跳转方法定义/实现            |
| Ctrl  \+ H                 | 类的层级关系               |
| Ctrl  \+ F12               | Show Members 类成员快速显示 |

版本管理相关

| 快捷键             | 介绍        |
|-----------------|-----------|
| Ctrl \+ D       | Show Diff |
| \(Shift\) \+ F7 | （上）下一处修改  |

更多快捷键请参考此文章

>leblog.github.io
<hr/>

## 编码效率相关（★★）

文件代码模板

Settings -> Editor -> File and Code Template
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNhY0d6aWNrcklOOHhmZ05UaE15cU5mOUVLQzNGdk5VbzIzRUxWU2VHUTR4M3V2aHVIVW41bmV3LzY0MA?x-oss-process=image/format,png)

在这里可以看到IDEA所有内置的文件代码模板，当你选择某个文件生成时，就会按照这里面的模板生成指定的代码文件。

另外，你可以在这里设置文件头。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnM3SWg1RGw2aWI0eVY1QmdGb0RQVk5BU0ZMRXNaYmhpYlRUQjRhdnJ0VGliTjNvZmN1TExobk9FVUEvNjQw?x-oss-process=image/format,png)
设置之后，效果如下

![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy96Nzl5SWJHQkVRQnNBZmo2WU9JMlNqdExKZHQzMnBkM0docDZyUGtONzBueGc5bGtwVlBKNG5jVjNjREZ1TjBpYU14WTF3aWN4UEUwTksxVzJsMVpkTUJ3LzY0MA?x-oss-process=image/format,png)
实时代码模板

IDEA提供了强大的实时代码模板功能，并且原生内置了很多的模板，比如，当你输入sout或者psvm，就会快速自动生成System.out.println();和public static void main(String[] args) {}的代码块。


![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnM4QjFZaklFdnZNZ2VtNlVQNnRkY2x2d1BXcGlhaWJDY2pFWEx1dDZGNTRzMUpFWXR1dndxTXBuQS82NDA?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy96Nzl5SWJHQkVRQnNBZmo2WU9JMlNqdExKZHQzMnBkM2lhUEtCY2JSQnE4VHdYRDlmZ3pLUm5PU3p6VFZUUlFEbXdXa3IxdlRqRHBDeFdneHNzSWdpYll3LzY0MA?x-oss-process=image/format,png)
这些的模板可以在Settings -> Editor -> Live Templates看到。使用者可以按照自己的使用习惯来熟悉相关的代码模板。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNoa2xEOXhKRTdDbzYzamZHMm10R2ZLS2ZaaWJreGliUWNaQXhad2dpYXY2V08wWlJXU0NsRWRBcWcvNjQw?x-oss-process=image/format,png)
定制代码模板

IDEA也提供自己定制实时代码模板的功能。

- 创建自己的模板库

- 创建定制的代码模板
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy96Nzl5SWJHQkVRQnNBZmo2WU9JMlNqdExKZHQzMnBkM0R6aWJMNmY2YUdERGliaWN6YnQ4ZzBIdjRoT1RweGRBZUVhbjFKRDU4RUNSTVBYYUN0bVZVa3ZPUS82NDA?x-oss-process=image/format,png)
图中的MyGroup就存放着我自己定义的代码模板。

其他

CRTL+ALT+T	
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNsRmxNZ2NHMjJ3S0Y2SnkxZUVCNVNKeWFXajFERUN3SEVhYUkydVYxV01STmJiZDVCejZNbEEvNjQw?x-oss-process=image/format,png)

Ctrl + Alt + T 提供的是代码块包裹功能 - Surround With。可以快速将选中的代码块，包裹到选择的语句块中。

本地历史版本

IDEA 自带本地版本管理的功能，能够让你本地编写代码变得更加的安心和方便。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNBV2pYSk1RMURPNmROcUUwSmliTkwxSVlWVWlhbm1nNElXS2g0S2lhaGVPVU1idWxpYkN1T0NEaWFYdy82NDA?x-oss-process=image/format,png)<hr/>

## 代码调试 源码阅读相关（★★★）

视图模式
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNQUUJLdTVMU3hVQzJOcXF4OVVjRURGdUtaUWliOXZOZWtJVmlhVVpRQ2libExlM2RXb01FR0Q1N3cvNjQw?x-oss-process=image/format,png)
IDEA提供两种特殊的视图模式，

- Presentation Mode - 演示模式，专门用于Code Review这种需要展示代码的场景

- Distraction Free Mode - 禅模式，专注于代码开发

代码调试

**1. 条件断点**

IDEA 可以设置指定条件的断点，增加我们调试的效率。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNpYkZHdGFpYm43RlpJMEl3OGxibHZMRGVpYjhLNUZGN0F2dmRwOWdBVU10bWhvRDkxaWEyZ2c4VzlBLzY0MA?x-oss-process=image/format,png)
**2. 强制返回**

IDEA 可以在打断点的方法栈处，强制返回你想要的方法返回值给调用方。非常灵活！
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNoVUhGQ1piVGljNmZpYnYwR0tCMkJOWXNlSlRXZzJIVGJtM3NnVUhxdFltdEpyYlFqRjFsaWJCTVEvNjQw?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnMxZ3FCWGVzR2lhUkxsTzJnZ0V1V0NaUk1YTGlhSURxVEhRUDcxUFBxYTk4TkhjZnRBRThSN3hyZy82NDA?x-oss-process=image/format,png)
**3. 模拟异常**

IDEA 可以在打断点的方法栈处，强制抛出异常给调用方。这个在调试源码的时候非常有用。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnN3VHYyS0hvRnNMd3JvajlwUlNwYzhnUUttYm9mSWo1YjUzMHVGTHM0RlBWR0Q4bzg4RFBpYXlnLzY0MA?x-oss-process=image/format,png)
**4. Evaluate Expression**

IDEA 还可以在调试代码的时候，动态修改当前方法栈中变量的值，方便我们的调试。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNCeVQ3QXhTaWJNWTVDbTZmeG5xR1RKMWliVDRoY1NLREpReDFHRkM1SjY1U1REZUlGMFJMRmNkQS82NDA?x-oss-process=image/format,png)
<hr/>

### 插件方面
**插件安装**

File -> Setting -> Plugin

插件安装，可以直接在IDEA的插件库中实时搜索安装。browse plugin repository

对于网络不好的用户，可以登录官方插件仓库地址：plugins.jetbrains.com/idea，下载压缩包之后，选择`install from disk`

**插件推荐**

本人日常开发中使用的插件

**Alibaba Java Coding Guidelines**

阿里Java编程规约插件

**FindBugs**

代码缺陷扫描
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy96Nzl5SWJHQkVRQnNBZmo2WU9JMlNqdExKZHQzMnBkM1E5cWZVOVM4SE1SQ2tTM2liMjZtZ0x5OHl2cm9OY0NKaWNOcjRlcHBYMXprcXJaMW5IQ25zRVZRLzY0MA?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNrOXNJYmRDaGRpY0NZdWhydVlZWWljRTc1SXBpY2NVcVFWR3dWdjdsQWdVaWNxbUNINURadDVIMTFBLzY0MA?x-oss-process=image/format,png)
**PMD**

代码缺陷扫描

**InnerBuilder**

builder模式快速生成
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNWSG9uT2FGRERtOG5XcXlTT2V1OUFQWklZODFTVzJkRVFUT2liVjlldWJmWGdKZVlDdXQ1SUh3LzY0MA?x-oss-process=image/format,png)
**lombok plugin**

lombok 插件

**maven helper**

maven 依赖管理助手 ，解析maven pom结构，分析冲突；
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNnaEQ2aWFvaWJoaWJpYklyWERQenBXMTROS2lhNmlheWdpYmdIbXhobkc3aWF4TDVXdnZxakl0WlUzeDI2QS82NDA?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnMxWUZrYlE5YWlieENoa3NSTU5vbktibU9LNnRGcE83S2VXalM3bTB4TUdNSlZjM3hhQ3YwcGtBLzY0MA?x-oss-process=image/format,png)

**Rainbow brackets**

让代码中的括号更具标识性
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNyTkNKOTVNeFJPZVFXMFhaNVR3dk5HMDJ1MVVVaWJDZGJrdEJYQWZ5V3QzU2ljOFZ1aWNncWpOOUEvNjQw?x-oss-process=image/format,png)
**String Manipulation**

String相关辅助简化，搭配 CTRL+W 、ALT+J等文本选择快捷键使用
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2dpZi9lUVB5QmZmWWJ1ZmVEUGY4MzkydkFqdHp6MzNMWGVjd2xMZ005dmNFZ1NNU2M1QTZLRGQxVTZ3VzlYMHlRUzFYNDdQMnlDR0hQa1Y4Rm4zbUhMQjRvZy82NDA?x-oss-process=image/format,png)
**Translation**

翻译插件，阅读源码必备
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnM2RlhueEtRM04wYlgxekVvak1DNENxU1NISHU0QnBvM2pJaHVaOWZJNXBpYjRXN3psNmpBU1NRLzY0MA?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNxTVViZjNiZ1o2ZWliaWJZdkdBOTlkQUZPYUlZR2t3TkR0MEFVZm1NRVV6akVyMnVMWW5hSVNrZy82NDA?x-oss-process=image/format,png)
**GenerateAllSetter**
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2dpZi9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNLSHJtSGJDVUtrcThjT1JhYmljSXY5RE9vSnpqWGZoTmliMUVubDlOVWlhdXpFV2gxYVFmUjd2T3cvNjQw?x-oss-process=image/format,png)

	**Key Promoter X**

对你的鼠标操作进行 快捷键提示
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2dpZi9lUVB5QmZmWWJ1ZmVEUGY4MzkydkFqdHp6MzNMWGVjd0FFSUhSTUw3bHpqckppYmxRUUFvUTZ2MjRHNG1wY2cwN3VWTFhxN2JGMFZxMlJ2MWg4Qk51dGcvNjQw?x-oss-process=image/format,png)
**GenerateSerialVersionUID**

Alt + Insert 快速生成SerialVersionUID
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2dpZi9lUVB5QmZmWWJ1ZmVEUGY4MzkydkFqdHp6MzNMWGVjdzB1a2dxcEpHdFdpYjM1NzA1QmRiaFlkRkJwdGxvSXRDQlZUTG9MSEJQZmVFaWNaWE5Vb3dQVEFRLzY0MA?x-oss-process=image/format,png)
**GsonFormat**
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2dpZi9lUVB5QmZmWWJ1ZmVEUGY4MzkydkFqdHp6MzNMWGVjd3B5Z2tOSzhmeERBQkN5aWFXQVVpYk15cGtDaDM5aWFxMlVFUHlHVzI0eWVEOFBPY25weG5ZQnlwZy82NDA?x-oss-process=image/format,png)
**RestfulToolkit**

- 快速跳转到Restful Api处( use: Ctrl(Command) + \ or Ctrl + Alt + N )

- 展示Resultful 接口结构

- http 简单请求工具![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNrMWljeHNzc0pOaWNLaWI1VmliY3hLbDU3bW5NOFhjNFY4QmlhWUJhSGZrblpSdE9FQlpKWVNIQ05jUS82NDA?x-oss-process=image/format,png)
- ![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy96Nzl5SWJHQkVRQnNBZmo2WU9JMlNqdExKZHQzMnBkM0NOc0tZTHVWaWJsRXp2Vm01b1ZXVVVlZ0xQeG1DNUpwU0poR0pGVFhHd1NzZ0QzaWJsZEtMTFF3LzY0MA?x-oss-process=image/format,png)
**Material Theme UI**

本人自用的主题就是这个。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNTdVNKdk5oYlhDOGxhN0Z4b2xpYUtyYUdGOHRhaldHMmxIR3RYbFcxcXhBYWEzM1ZTaWNKR29ody82NDA?x-oss-process=image/format,png)
**MyBatis Log Plugin**

把 Mybatis 输出的sql日志还原成完整的sql语句，看起来更直观。
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9RQ3U4NDlZVGFJTUFDenU1RHYweWhpYzRHUldVSm1qUnNla0J5Y091UDY4WG1xeGliYnZUN3BaU1pDSEVXQUdFN1BpYzJ0OGliVWd5VWlhemY3a2JtaElPTVVRLzY0MA?x-oss-process=image/format,png)
**Free Mybatis**

MyBatis 免费的插件

<hr/>

参考
> https://github.com/judasn/IntelliJ-IDEA-Tutorial

(By the way, 更多IDEA使用请参考此延伸文档以及官方文档)

<h1>（完）<h1/>

