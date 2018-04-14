# 准备Gentoo编译环境

由于Gentoo本身是面向用户的编译需求构建的操作系统，因此使用Gentoo配置编译环境会相对简单一些。

## 获取基础镜像

### 下载镜像压缩包

浏览[Gentoo官方镜像](http://distfiles.gentoo.org/releases/amd64/autobuilds/current-stage3-amd64)或[科大镜像](https://mirrors.ustc.edu.cn/gentoo/releases/amd64/autobuilds/current-stage3-amd64)，选择下载stage3-amd64-((buildtime)).tar.xz，或者通过以下命令下载：

（注意以下操作均使用root用户）

Gentoo官方源：

```
# wget http://distfiles.gentoo.org/releases/amd64/autobuilds/$(curl http://distfiles.gentoo.org/releases/amd64/autobuilds/latest-stage3-amd64.txt|grep -v "^#"|cut -d' ' -f1) -O /opt/stage3-amd64.tar.xz
```

如果下载速度较慢，亦可从科大开源软件镜像站下载：

```
# wget https://mirrors.ustc.edu.cn/gentoo/releases/amd64/autobuilds/$(curl https://mirrors.ustc.edu.cn/gentoo/releases/amd64/autobuilds/latest-stage3-amd64.txt|grep -v "^#"|cut -d' ' -f1) -O /opt/stage3-amd64.tar.xz
```

### 解压

解压镜像到`/opt/gentoo`：

```
# mkdir -pv /opt/gentoo
# cd /opt/gentoo
# tar xpf ../stage3-amd64.tar.xz --xattrs-include='*.*' --numeric-owner
```

## 切换根目录前的准备

将本机的DNS配置复制到新的环境中：

```
# cp --dereference /etc/resolv.conf /opt/gentoo/etc/
```

挂载proc文件系统：

```
# mount --types proc /proc /opt/gentoo/proc
```

## 修改软件仓库地址（可选）

为了加快下载速度，可以将官方源地址修改为[科大开源镜像站](https://mirrors.ustc.edu.cn)提供的镜像地址：

```
# echo GENTOO_MIRRORS=\"http://mirrors.ustc.edu.cn/gentoo/\" >> /opt/gentoo/etc/portage/make.conf
```

## 安装编译环境

### 改变根目录

下面的命令将改变根目录`/`所代表的实际指向，我们需要将其修改为刚才解压得到的gentoo镜像：

```
# chroot /opt/gentoo /bin/bash
# source /etc/profile
```

chroot的第二个参数`/bin/bash`表示在新的根目录环境中执行的命令。在这里，我们启动了一个bash shell。

source命令使用/etc/profile配置一些基本的环境变量，如PATH等。

注：执行`exit`可以退出chroot环境。

**请特别注意：下面的命令都将在新的根目录中执行！**

### 更新仓库索引

```
# emerge-webrsync
```

### 安装软件包

Gentoo自带编译器和文本编辑器nano，这里需要安装一些编译Linux内核所需要的工具：

```
# emerge -av bc cpio net-misc/curl
```

如果你倾向于使用vim，也可以通过此方式安装：

```
# emerge -av vim
```

## 附注

如果你想在本机安装Gentoo，可以参考[Gentoo官方的安装文档](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation)。
