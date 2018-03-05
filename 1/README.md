实验一
======

1.  [安装Linux操作系统](install)
1.  [熟悉Linux操作系统的常用命令](linux)
1.  [学习使用bash](bash)
1.  [学习使用git](git)
1.  [熟悉GitHub使用流程](github)

请大家进行上述学习后，在GitHub上完成[实验一](https://classroom.github.com/a/KL56bHvj)。

你需要在页面中输入学号来将你的GitHub账号和学号绑定，之后GitHub会自动为你创建出一个repo。请务必**使用Linux命令行**`git clone`这个repo，在其中创建名为`hello_linux.sh`的文件，使其功能如下文所述，并使用`git commit`、`git push`等命令将修改后的repo上传到GitHub。

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

参考代码（鼓励大家寻找更简单的写法）：

```Shell
#!/bin/bash
echo Hello Linux
echo -n >output.txt
while read line
do
    echo $line >>output.txt
done
```

提交截止时间为4月1日晚23:00，请注意GitHub将在截止时间到达时锁定你的repo，不再接受变更。

评分要点
--------

- 正确绑定学号并创建了repo
- repo中有`hello_linux.sh`文件
- `hello_linux.sh`是通过Linux命令行创建并提交的
- `hello_linux.sh`是可执行文件
- `hello_linux.sh`功能正确
