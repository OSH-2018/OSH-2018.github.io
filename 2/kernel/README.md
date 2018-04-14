# 裁剪Linux内核

本小节主要阐述如何从源代码构建一个最小化的Linux内核，了解必要的内核编译选项。

## 获取内核源码

下载Linux内核源代码：

```
# cd /usr/local/src
# curl https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.10.7.tar.xz | tar xJf -
# cd /usr/local/src/linux-4.10.7
```

P.S. `curl`是一个多协议的网络通讯工具。在上一条命令中，`curl`从互联网获取内核源码的压缩包，并借助管道(pipe)将数据提供给文件存档工具`tar`，`tar`将`curl`获取的数据解压到当前目录中。 参数中`x`表示解压，`J`表示解压xz格式的数据，`f`表示指定输入文件，`-`表示使用标准输入作为输入文件。

本文撰写时，Linux内核最新的稳定版本为4.10.7，为了避免内核版本不同带来的配置差异，建议大家统一使用`4.10.x`系列的内核。

如果由于网络原因难以下载，可以使用科大源：

```
# curl https://mirrors.ustc.edu.cn/kernel.org/linux/kernel/v4.x/linux-4.10.7.tar.xz | tar xJf -
```

## 编译

### 生成初始配置

生成一个空的配置文件：

```
# make allnoconfig
```

### 修改内核配置

启动配置（编辑）器：

```
# make menuconfig
```

**说明：方向键可以移动光标，空格键用于选中（或取消选中）当前选项，ESC键返回上层菜单（或退出），回车键进入子菜单，按下高亮的字母可以快速跳转至对应选项。**

打开64位内核支持：

```
[*] 64-bit kernel
```

为了让内核能够打印调试信息，我们需要打开kernel print function的支持：

```
-> General setup
  -> Configure standard kernel features
[*] Enable support for printk
```

打开内存文件系统的支持：

```
-> General setup
[*] Initial RAM filesystem and RAM disk (initramfs/initrd) support
```

打开ELF可执行文件的支持：

```
-> Executable file formats / Emulations
[*] Kernel support for ELF binaries
```

打开TTY驱动的支持：

```
-> Device Drivers
  -> Character devices
[*] Enable TTY
```

为了能让QEMU能正常显示终端，需要打开UART串口的支持：

```
-> Device Drivers
  -> Character devices
    -> Serial drivers
[*] 8250/16550 and compatible serial support
[*]   Console on 8250/16550 and compatible serial port
```

为了让标准UNIX工具能够正常工作（如获取启动时间），需要打开`/proc`和`sysfs`文件系统的支持：

```
-> File systems
  -> Pseudo filesystems
[*] /proc file system support
[*] sysfs file system support
```

全部设置完成后，请保存修改后退出配置编辑器。

### 编译

开始编译内核：

```
# make
```

将编译的结果复制到`/usr/local/mini-os`目录备用：

```
# mkdir -pv /usr/local/mini-os
# cp arch/x86_64/boot/bzImage /usr/local/mini-os/bzImage
```
