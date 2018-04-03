# 写在前面

本小节主要针对文档进行一些说明，方便大家理解。

## 提示符

```
$ echo "Hello World!" > some-file.txt
$ cat some-file.txt
# chown root:root some-file.txt
```

对于类似上文的命令块，每行为一条命令，行首的提示符`$`表示该条命令可以以普通用户权限执行，提示符`#`表示该条命令需要以管理员权限（即`root`用户）执行。 

P.S.执行命令时不需要输入提示符

## whoami

以下命令可以获得当前用户：

```
$ whoami
```

屏幕将打印当前登录的用户的用户名。

## sudo

如果需要临时提升为管理员权限，可以使用sudo命令。如需要以管理员权限执行：

```
# touch something
```

那么，则可以临时提权为管理员：

```
$ sudo touch something
```

在大多数情况下，以上两条命令的效果是等价的。

如果需要执行大量管理员权限的命令，可以打开一个root shell：

```
$ sudo -s
```

该命令将返回一个root终端，随后执行的命令都将应用管理员权限。执行`exit`可以退出root终端。

## 文本编辑器

本实验需要在命令行模式下编辑少量文本，因此需要大家掌握至少一种文本编辑器的用法。`nano`比较适合初学者，`vim`和`emacs`十分强大，但学习起来有一定难度，请大家根据自身情况选择。参考资料见文末。

## 参考资料

1. [nano命令](http://man.linuxde.net/nano)
2. [简明 VIM 练级攻略](http://coolshell.cn/articles/5426.html)
