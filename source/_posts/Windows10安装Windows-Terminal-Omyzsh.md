---
title: "Windows10安装Windows Terminal + oh-my-posh"
top: false
cover: false
toc: true
mathjax: true
date: 2021-06-26 12:23:52
password:
summary:
tags: [Windows，oh-my-posh]
categories: oh-my-posh
---


# Windows10安装Windows Terminal + oh-my-posh

各位 Windows 开发者，是不是很羡慕他们 Linux 和 mac 用户的 terminal 在配置过 oh-my-zsh 之后变得非常漂亮？现在不用羡慕了，因为你的 Powershell 也可以变得非常漂亮


### 安装步骤

#### 1. 步骤一

首先得为 Powershell 安装必要的插件，安装这些插件需要管理员权限，所以别忘了以管理员身份启动 Powershell。

```powershell
# 为当前用户安装 posh-git
Install-Module posh-git -Scope CurrentUser
# 为当前用户安装 oh-my-posh
Install-Module oh-my-posh -Scope CurrentUser
```

#### 2.添加配置文件

然后打开PowerShell配置文件，这个文件你可以通过`notepad $PROFILE`命令打开编辑，当然`notepad`也可以换成你自己常用的文本编辑器。

![image-20210626111556535](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210626111556535.png)

如果没有可以**拷贝下面的内容 并且 更改文件名**为`Microsoft.PowerShell_profile.ps1`

````shell
Import-Module posh-git # 引入 posh-git
Import-Module oh-my-posh # 引入 oh-my-posh
Set-PoshPrompt -Theme Paradox # 设置主题为 Paradox

#Set-PSReadLineOption -PredictionSource History # 设置预测文本来源为历史记录
 
Set-PSReadlineKeyHandler -Chord Tab -Function Complete # 设置 Tab 键补全
Set-PSReadLineKeyHandler -Chord Ctrl+d -Function MenuComplete # 设置 Ctrl+d 为菜单补全和 Intellisense
Set-PSReadLineKeyHandler -Chord Ctrl+z -Function Undo # 设置 Ctrl+z 为撤销
Set-PSReadLineKeyHandler -Chord Ctrl+u -Function RevertLine # 设置 Ctrl+u 为重置行
Set-PSReadLineKeyHandler -Chord UpArrow -Function HistorySearchBackward # 设置向上键为后向搜索历史记录
Set-PSReadLineKeyHandler -Chord DownArrow -Function HistorySearchForward # 设置向下键为前向搜索历史纪录
# Chocolatey profile
$ChocolateyProfile = "$env:ChocolateyInstall\helpers\chocolateyProfile.psm1"
if (Test-Path($ChocolateyProfile)) {
  Import-Module "$ChocolateyProfile"
}
````

其中快捷键的设置可以根据自己需要随意配置，具体文档看这 [PSReadLine](https://docs.microsoft.com/en-us/powershell/module/psreadline/?view=powershell-7.1)

然后关闭powershell再次重新打开

#### 3.安装字体

oh-my-posh 和 oh-my-zsh 一样，需要一套带各种图标的等宽字体才能正常的显示，所以我们现在该去安装字体了。

对于字体，你可以有以下几种选择方案：

- 直接按教程来，使用`Cascadia Code PL`字体，字体可以在[这里](https://github.com/microsoft/cascadia-code/releases)下载
- 或者在 [Nerd Fonts](https://www.nerdfonts.com/) 这个网站中下载字体，这个网站的字体几乎都是为了开发定制的

安装好之后右键 Powershell 的菜单栏，打开`属性 -> 字体`，把字体设置为上面安装的字体之后就可以了。

## 安装 Windows Terminal

巨硬新款终端，帅气又漂亮，安装也非常简单，打开 [Microsoft Store](https://www.microsoft.com/zh-cn/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab) 直接搜索 Windows Terminal 然后安装就行了，至于 Windows Terminal 本身的配置的话，截至本文发布时间，已经可以支持界面化设置，不用再直接修改配置文件了，所以对于设置就不过多赘述了。



![image-20210626111803571](https://raw.githubusercontent.com/leblog/img/main/huiyi/image-20210626111803571.png)



#### 4.可能会出现的情况

powershell中文乱码![image-20210626112340986](C:\Users\58387\AppData\Roaming\Typora\typora-user-images\image-20210626112340986.png)

解决方案

cmd 控制台默认编码，一般是简体中文默认的GBK，如果出现中文乱码，一般改为UTF-8可解决。

##### 打开 cmd 控制台窗口

win（窗口键，在Ctrl与Alt之间）+R，输入 cmd，回车，这样操作会打开 cmd 控制台窗口。

##### 检查当前的编码

```
C:\Users\AndyChen>chcp
Active code page: 936
```

显示当家的编码格式为 936。

##### 常用的编码及对应的码值(10进制)

| 十进制码值 | 对应编码名称      |
| :--------- | :---------------- |
| 950        | 繁体中文          |
| 65001      | Unicode (UTF-8)   |
| 936        | 简体中文默认的GBK |
| 437        | MS-DOS 美国英语   |

##### 测试中文显示

将以下代码保存为一个批处理文件，如 test.bat，或者 test.cmd，双击运行

```
@echo off
echo test chinese character view  测试中文字符显示
pause
```



我的测试如下：

```
test chinese character view  娴嬭瘯涓枃瀛楃鏄剧ず
Press any key to continue . . .
```



当为936时，中文显示乱码。

##### 修改控制台CMD编码格式为UTF-8

##### 临时修改为 UTF-8

执行 `chcp 65001`

```
C:\Users\AndyChen>chcp 65001
Active code page: 65001
```



这种方式在关闭 cmd 之后会自动失效，下次再打开，还是会变回默认的 936。

##### 永久修改方法一

1. win+R 或者点击开始菜单，找到运行，在运行输入框里面输入

   ```
   regedit
   ```

   ，回车，会打开注册码编辑窗口，在地址栏输入：

   ```
   Computer\HKEY_CURRENT_USER\Console\%SystemRoot%_System32_cmd.exe
   ```

   ，回车。

   ![img](https://www.lovesofttech.com/img/general/cmd-chinese-character-01.png)

2. 双击

    

   ```
   CodePage
   ```

    

   然后先择十进制，改为65001。

   ![img](https://www.lovesofttech.com/img/general/cmd-chinese-character.png)

3. 同理，可以修改 PowerShell 的默认编码，位置：`Computer\HKEY_CURRENT_USER\Console\%SystemRoot%_System32_WindowsPowerShell_v1.0_powershell.exe`，如果没有 `CodePage`，则在该项下新建一个 DWORD（32位值），命名为`CodePage`，值设为`65001`

重启 cmd/PowerShell 后生效。

##### 永久修改方法二

创建文本文件 characterSet.reg，内容如下：

```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Console\%SystemRoot%_SysWOW64_WindowsPowerShell_v1.0_powershell.exe]
"CodePage"=dword:0000fde9

[HKEY_CURRENT_USER\Console\%SystemRoot%_System32_WindowsPowerShell_v1.0_powershell.exe]
"CodePage"=dword:0000fde9

[HKEY_CURRENT_USER\Console\%SystemRoot%_System32_cmd.exe]
"CodePage"=dword:0000fde9
```



双击运行。

##### 再次测试中文显示

运行之前的测试脚本，显示如下：

```
test chinese character view  测试中文字符显示
Press any key to continue . . .
```



能够正常显示，说明设置成功。