实验一
======

提交截止时间为4月1日晚23:00，请注意GitHub将在截止时间到达时锁定你的仓库，不再接受变更。

Linux的安装与使用
-----------------

1.  [安装Linux操作系统](install)
1.  [熟悉Linux操作系统的常用命令](linux)
1.  [学习使用bash](bash)
1.  [学习使用git](git)
1.  [熟悉GitHub使用流程](github)

请大家进行上述学习后，在GitHub上完成[实验一](https://classroom.github.com/a/KL56bHvj)。

你需要在页面中输入学号来将你的GitHub账号和学号绑定，之后GitHub会自动为你创建出一个git仓库。请`git clone`这个仓库，在其中创建名为`hello_linux.sh`的文件，使其功能如下文所述，并使用`git commit`、`git push`等命令将修改后的仓库上传到GitHub。

`hello_linux.sh`应为**[可执行文件](http://man.linuxde.net/chmod)**，当以`./hello_linux.sh`这条命令执行它时，它应当向标准输出打印一行文本`Hello Linux`，并将标准输入的文本保存至当前目录下名为`output.txt`的文件。

如果要进行测试，可以运行这条命令：

```Shell
echo -e "It is the time you have wasted for your rose that makes your rose so important.\nAntoine (The Little Prince)" | ./hello_linux.sh
```

屏幕应当输出：

```
Hello Linux
```

之后，`cat output.txt`这条命令应当输出：

```
It is the time you have wasted for your rose that makes your rose so important.
Antoine (The Little Prince)
```

参考代码1（鼓励大家寻找更简单的写法）：

```Shell
#!/bin/bash
echo Hello Linux
echo -n >output.txt
while read line
do
    echo $line >>output.txt
done
```

参考代码2：

```Shell
#!/bin/bash
echo Hello Linux
cat >output.txt
```

调试操作系统的启动过程
----------------------

请使用调试跟踪工具，追踪自己的操作系统（建议Linux）的启动过程，并找出其中至少两个关键事件。

请提交一份纯文本格式或Markdown格式的实验报告，详述调试中使用的工具、步骤和结果。如有自行编写代码或脚本，请一并提交，并在文档中注明编译或解释环境，如有二进制代码，也可一并提供。

选做：自行编写trace工具
-----------------------

针对有Linux基础的同学，可自行编写一个trace工具或函数，并以此来追踪操作系统的启动过程。

评分要点
--------

- 正确绑定学号并创建了仓库
- 仓库中有`hello_linux.sh`文件
- `hello_linux.sh`采用了UNIX/Linux风格换行符（即使用"\n"而非Windows风格的"\r\n"代表换行）
- `hello_linux.sh`是可执行文件
- `hello_linux.sh`功能正确
- 实验过程描述完整
- 实验报告中寻找的关键事件正确
- 加分项：自行编写了trace工具，且功能基本正确
