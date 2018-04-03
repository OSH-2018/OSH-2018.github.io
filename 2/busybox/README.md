# 编译busybox

任何Linux发行版都需要一些基础的命令以便让系统正确运行（如`mount`, `ls`, `pwd`, `ifconfig`, `cd`, `mkdir`, `touch`, `rm`, `vi` 等等）。我们的构建的操作系统也需要这些工具。一般而言有两种方法：

* 单独下载每个工具的源代码，编译安装
* 使用busybox

busybox能够通过一个单独的可执行文件提供多种UNIX工具的的简化版本。虽然busybox提供的工具的选项并不全面，但亦足以胜任大部分的任务。busybox尺寸较小，编译较为简单，在此我们选择第二种方式。

## 获取源代码

```
# cd /usr/local/src
# curl https://busybox.net/downloads/busybox-1.26.2.tar.bz2 | tar xjf -
# cd busybox-1.26.2
```

P.S. 截止撰文时，busybox最新稳定版本为1.26.2

## 配置编译选项

生成默认配置：

```
# make defconfig
```

启动配置编辑器：

```
# make menuconfig
```

由于我们没有编译libc，因此需要直接编译出静态的可执行文件（即：不依赖任何动态链接库）

```
-> Busybox Settings
  -> Build Options
[*] Build BusyBox as a static binary (no shared libs)
```

## 编译

```
# make
```

## 安装进根文件系统

```
# make CONFIG_PREFIX=/usr/local/mini-os/rootfs install
```
