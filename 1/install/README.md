# 安装Linux操作系统

## 发行版选择

Linux发行版数量众多（见参考资料1），其中部分较为主流的Linux发行版有：

* [Debian](https://www.debian.org/releases/stable/installmanual)
* [Ubuntu](https://www.ubuntu.com/download/desktop/install-ubuntu-desktop)
* [Fedora](https://docs.fedoraproject.org/en-US/Fedora/25/html/Installation_Guide/index.html)
* [Arch Linux](https://wiki.archlinux.org/index.php/Installation_guide_(简体中文))
* [Elementary OS](https://elementary.io/zh_CN/docs/installation#installation)
* [Deepin](https://wiki.deepin.org/?title=原生安装)
* [Gentoo Linux](https://www.gentoo.org/get-started/)

不同的发行版有各自的特点，设计哲学也不尽相同，大家可以选择任意一款自己喜欢的Linux发行版。如果是初次接触Linux，可以选择Ubuntu，安装相对容易。

## 安装方式

常见的两种安装方式：

* 直接安装在裸金属(bare metal)中
* 安装在虚拟机中

如果打算将Linux直接安装在裸金属中，且与Windows/macOS共存，请自行查找相关资料。这种方案操作相对繁琐，但系统性能和使用体验相对较好。

下面列出了一些常用的虚拟化软件，请大家根据自身情况选择。

* [Virtual Box](https://www.virtualbox.org)（免费软件，GPLv2协议，支持macOS, Windows, Linux操作系统）
* [Parallels Desktop](http://www.parallels.com/products/desktop/) （商业软件，支持macOS）
* [VMware Fusion](http://www.vmware.com/products/fusion.html) （商业软件，支持macOS）
* [VMware WorkStation](http://www.vmware.com/products/workstation.html) （商业软件，支持Windows, Linux）
* [VMware Player](http://www.vmware.com/products/player.html) （商业软件，非商业用途免费，支持Windows, Linux）

## 桌面环境

常见的桌面环境：

* GNOME (Debian, Fedora默认桌面环境)
* KDE
* Unity (Ubuntu 17.10以前版本默认桌面环境)
* XFCE

虽然可以在纯命令行(command line)模式下使用Linux，但由于后续实验需要使用浏览器执行部分操作，因此建议大家安装至少一种桌面环境。

许多面向桌面用户的发行版都会默认安装桌面环境，如安装Ubuntu Desktop时，安装程序会默认安装GNOME桌面环境。一般而言，这些默认的桌面环境就能够满足我们的需求。

## 参考资料

1. [现存的Linux发行版](https://upload.wikimedia.org/wikipedia/commons/1/1b/Linux_Distribution_Timeline.svg)
2. [Linux基本概念和安装指南（Linux入门公开课）](https://ftp.ustclug.org/course/)
