# 运行操作系统

## 安装QEMU

我们编译的操作系统并不包含引导器，因此无法直接运行在裸金属中。我们这里选择QEMU来运行这个操作系统。

```
# apt install -y qemu-system-x86
```

## 打包文件系统

为了让QEMU读取文件系统，我们需要对文件系统进行打包：

```
cd /usr/local/mini-os/rootfs
find . | cpio -oHnewc | gzip > ../initramfs.gz
```

## 运行操作系统

```
# cd /usr/local/mini-os
# qemu-system-x86_64 -kernel bzImage -initrd initramfs.gz -nographic -append "console=ttyS0"
```

如果一切顺利，你按回车键时屏幕上将打印出`# `这样的提示符，可以输入命令。

在宿主机上以root权限执行`killall qemu-system-x86_64`可以关闭QEMU模拟器。

## 写在后面

如果希望这个操作系统运行在裸金属中，需要开启额外的内核编译选项（主要是驱动程序），以及安装引导器（如GRUB）。如果大家对此感兴趣，可以参考Linux From Scratch（见参考资料），也可以与助教交流讨论。

由于本实验主旨是为了精简Linux操作系统内核，因此我们没有创建一个完整的根文件系统。如果要让操作系统正常运行，还需要创建许多配置文件，如`/etc/inittab`, `/etc/passwd`, `/etc/group`, …  具体可以参考Linux From Scratch。

## 参考资料

1. [Linux From Scratch](http://www.linuxfromscratch.org/lfs/view/stable/)
