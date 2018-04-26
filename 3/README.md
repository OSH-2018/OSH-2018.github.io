实验三
======

提交截止时间为5月13日晚23:00，请注意GitHub将在截止时间到达时锁定你的仓库，不再接受变更。

请大家通过此链接在GitHub上提交[实验三](https://classroom.github.com/a/yeJkKW4S)。


实验目的
--------

本实验旨在通过编写一个基于内存的文件系统，加深对文件系统和内存管理方面的理解。

注：本实验不强制要求使用何种编程语言、使用FUSE、或使用Linux操作系统，只要完成实验要求即可，但为了叙述方便，以下文档使用C语言在Linux上通过FUSE实现。


实验要求
--------

1. 创建一个可挂载的内存文件系统，此文件系统的文件信息均存储于内存中
2. 可以进行基本的文件操作（增删改普通文件）
3. 自行实现此文件系统的内存分配


实验环境
--------

本文档默认使用64位Linux操作系统，使用gcc编译器，并使用目前大部分Linux操作系统自带的2.9.x版本的libfuse为例编写，请先安装相应的编译环境，并安装libfuse（如在Ubuntu下安装libfuse-dev软件包，或在Gentoo下安装sys-fs/fuse软件包）。


使用FUSE
--------

FUSE是用户空间文件系统，它避免了在内核模式开发文件系统，可以大幅简化工作量，但不可避免的会带来额外的内核态/用户态的开销。

请先创建一个`oshfs.c`文件，内容如下：

```c
#define FUSE_USE_VERSION 26
#include <fuse.h>
static const struct fuse_operations op;
int main(int argc, char *argv[])
{
    return fuse_main(argc, argv, &op, NULL);
}
```

使用如下指令编译：

```sh
$ gcc -D_FILE_OFFSET_BITS=64 -o oshfs oshfs.c -lfuse
```

新建挂载点：

```sh
$ mkdir mountpoint
```

之后即可使用`oshfs`挂载你的文件系统到mountpoint上：

```sh
$ ./oshfs mountpoint
```

此时可以通过`mount`命令确认你的文件系统已被挂载，但如果运行`ls mountpoint`，则会出现以下错误提示：

```sh
$ ls mountpoint
ls: cannot access 'mountpoint': Function not implemented
```

说明我们还未实现相关函数，因此此文件系统不支持列目录操作。


libfuse的示例程序
-----------------

在进行以下实验之前，请大家先了解一下FUSE的工作原理。

libfuse自身有几个简单的例子，可参见[libfuse的代码](https://github.com/libfuse/libfuse/tree/fuse_2_9_bugfix/example)。

其中fusexmp是一个简单的passthrough，可供参考。

hello则是一个简单的只读文件系统，其中只有一个hello文件，存放了"Hello World!\n"字符串。


一个朴素的实现
--------------

既然是内存文件系统，那么最简单的实现也就是直接将文件列表的链表和文件内容直接存放在malloc分配的内存中，一个简单的实现见[示例程序](oshfs.c)。

此程序可创建、修改文件，但未实现删除文件，也不支持目录操作。

你需要自行实现对文件的删除操作，对于目录操作的实现则不做强制要求。


存储管理
--------

在上述示例程序中，我们采用了malloc分配内存，在本实验中需要自行使用mmap向操作系统申请一块内存，并自行决定存储空间的分配算法（如B+树、伙伴算法等等）。

mmap和munmap的使用方式可参考示例代码的init函数。

注意：你的程序中的所有内存均应直接来自mmap分配的内存，包括文件的元数据、链表指针等均不可采用malloc分配内存。

*程序中每次mmap调用的size应相同且大于16MiB，并在空间全部用完前不能再次调用mmap，在空间存在空余时应该调用munmap释放内存。禁止以使用malloc的方式使用mmap。*


选做内容
--------

请将你实现的功能在README中详细进行描述，我们会参考实际情况予以加分。

包括但不限于以下内容：实现目录操作、修改文件的各种元数据、健壮的错误处理等。


评分细则
--------

待定。

*本次实验将采用人工批改与计算机自动批改相结合的方式，凡确认的抄袭行为将导致本次实验0分，请不要复制他人的代码。*
