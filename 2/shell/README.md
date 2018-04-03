# 编写shell程序

为了让用户可以控制系统，Linux系统一般会运行一个shell程序。通常来说，shell程序不会是系统启动后运行的第一个进程（也就是init进程），但此次实验中为了简化，我们在系统启动后直接运行自己编写的一个shell程序。

首先，大家可以将本页底部助教编写的一个示例程序拷贝到`/usr/local/mini-os/rootfs`（不在chroot环境中的话，就是`/opt/ubuntu/usr/local/mini-os/rootfs`），命名为`init.c`。然后在该目录下执行：

```Shell
gcc -static -o init init.c
```

这会编译出名为`init`的可执行程序。然后按照[运行操作系统](../run)一节的指引尝试运行，应当就能使用这个非常简陋的shell程序了——在系统开始运行后，按回车键你将会看到`# `这样的提示符，提示你输入命令。你可以输入`pwd`来查看当前所在的目录，或者输入`cd 某目录`来改变所在的目录，也可以调用任何busybox中提供的程序，如`ls`、`cat`等等。

*在此期间，内核可能会不时地将一些日志信息打印到屏幕上，因为系统的若干组件仍在启动。忽略这些信息即可。*

建议你先完全理解这个示例程序的工作原理、查清楚里面用到的各个函数的功能。

*思考一下：为什么cd命令必须做成shell程序的功能，而不能放在busybox，通过调用来运行呢？*

这个示例shell非常简陋，你的任务是在以下几个方面对它进行升级：

## 更健壮（推荐做，但不要求）

目前的示例程序非常脆弱，无法处理不良的输入（如`cd /`可以运行，但将中间的一个空格改成两个就不行），也不检查各种可能的错误（`chdir`、`fork`、`exec`等调用都可能出错）。建议你将它改得更健壮，以方便之后的进一步开发和调试。

## 支持管道

形如`env | wc`这样的命令利用了“管道”语法，将两条不同的命令对接在一起同时运行。`|`的意思是将前面的命令`env`（输出所有环境变量）的输出，作为`wc`（统计行数）的输入（这样就能统计出环境变量的总数）。请你观察并学习这个语法的效果，为你的shell程序实现这一功能。

你可能要用到的函数：`pipe`、`close`、`dup`。你可以执行`man 函数名`来查看系统自带的文档，或者上网搜索更多信息。

## 支持修改环境变量

许多程序和系统功能都依赖于环境变量，比如当你执行`ls`命令时，系统就是通过查询`PATH`环境变量来确定`ls`这个程序到底在哪里的。你可以运行`env`命令来查看当前的所有环境变量，也可以通过`export MY_OWN_VAR=abc`这样的命令来修改环境变量。请为你的shell程序实现这一功能。

你可能要用到的函数：`getenv`、`setenv`。

## 支持文件重定向（选做）

请你查找资料或做实验分析`ls > out.txt`这样的命令和`<`、`>>`等这些语法的含义，为你的shell程序实现这些功能。

你可能要用到的函数：`open`、`close`、`dup`。

## 更多功能（选做）

我们一般使用的shell非常强大，你还可以自行了解下面这些语法的含义：

```Shell
echo $PATH
A=1 env
cat >doc.txt <<EOF
This is some words.
EOF
alias ll='ls -l'
echo ~
(sleep 10; echo aha) &
```

## 示例程序

```C
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>
#include <sys/types.h>

int main() {
    /* 输入的命令行 */
    char cmd[256];
    /* 命令行拆解成的各部分，以空指针结尾 */
    char *args[128];
    while (1) {
        /* 提示符 */
        printf("# ");
        fflush(stdin);
        fgets(cmd, 256, stdin);
        /* 清理结尾的换行符 */
        int i;
        for (i = 0; cmd[i] != '\n'; i++)
            ;
        cmd[i] = '\0';
        /* 拆解命令行 */
        args[0] = cmd;
        for (i = 0; *args[i]; i++)
            for (args[i+1] = args[i] + 1; *args[i+1]; args[i+1]++)
                if (*args[i+1] == ' ') {
                    *args[i+1] = '\0';
                    args[i+1]++;
                    break;
                }
        args[i] = NULL;

        /* 没有输入命令 */
        if (!args[0])
            continue;

        /* 内建命令 */
        if (strcmp(args[0], "cd") == 0) {
            if (args[1])
                chdir(args[1]);
            continue;
        }
        if (strcmp(args[0], "pwd") == 0) {
            char wd[4096];
            puts(getcwd(wd, 4096));
            continue;
        }
        if (strcmp(args[0], "exit") == 0)
            return 0;

        /* 外部命令 */
        pid_t pid = fork();
        if (pid == 0) {
            /* 子进程 */
            execvp(args[0], args);
            /* execvp失败 */
            return 255;
        }
        /* 父进程 */
        wait(NULL);
    }
}
```
