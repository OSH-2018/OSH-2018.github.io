# 制作根文件系统

Linux系统需要一个文件系统作为运行的基础，其中有特殊设备节点、程序和普通文件等。

## 创建目录

内核需要挂载一些虚拟文件系统，用于与用户态程序交换信息，这些文件系统仅在运行时会被挂载，并不占用磁盘空间，我们需要在文件系统中创建这些目录：

```
# mkdir -pv /usr/local/mini-os/rootfs/{dev,proc,sys,run}
```

## 创建初始设备节点

系统初始化依赖于几个设备节点，我们需要逐个创建它们：

```
# cd /usr/local/mini-os/rootfs
# mknod -m 622 ./dev/console c 5 1
# mknod -m 666 ./dev/null c 1 3
# mknod -m 666 ./dev/zero c 1 5
# mknod -m 666 ./dev/ptmx c 5 2
# mknod -m 666 ./dev/tty c 5 0
# mknod -m 666 ./dev/ttyS0 c 4 64
```
