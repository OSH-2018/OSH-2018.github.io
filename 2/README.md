实验二
======

*第一次自动评测在4月20日晚23:00，建议大家在此之前做好，以防由于格式等原因意外失分。提交截止时间为4月22日晚23:00，GitHub将在截止时间到达时锁定你的仓库，不再接受变更。*

本实验旨在构建出一个精简的Linux操作系统，并在其上运行一个shell进程，接受用户控制。

为了降低实验难度，文档略去了grub和libc的构建过程。因此最终构建的成果无法直接运行在裸金属上，需要借助QEMU模拟器来运行。

1.  [写在前面](before)
1.  [准备编译环境](prepare)
1.  [裁剪Linux内核](kernel)
1.  [制作根文件系统](rootfs)
1.  [编译busybox](busybox)
1.  [编写shell程序](shell)
1.  [运行操作系统](run)

请大家按照上述步骤进行实验，并按下述要求在GitHub上提交[实验二](https://classroom.github.com/a/pZ5o0E0D)。

仓库根目录中需要有`bzImage`文件（二进制内核镜像）、`initramfs.gz`文件（打包的根文件系统）和`init.c`文件（你编写的shell源码），其他文件将被评测过程忽略。

使用这两个文件启动系统后，应当能从键盘输入类似下方列出的命令并成功运行。准确地说，你所编写的shell程序应当支持`cd`、`pwd`这两个内建命令，支持修改环境变量，支持所有busybox命令，支持管道符号`|`。

```
cd /
pwd
ls
ls | wc
ls | cat | wc
env
export MY_OWN_VAR=1
env | grep MY_OWN_VAR
```

为了减少失误导致的失分，我们会进行两次自动评测，实验二的成绩将计为其中较高者。每次评测后我们会通过邮件通知大家本次的结果。

*程序检测到的抄袭将会进行人工复核，确认的抄袭行为将导致本次实验0分，请不要复制他人的代码或提交非本人编译的结果。*
