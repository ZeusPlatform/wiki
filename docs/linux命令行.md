## 获取帮助
### help command
适用于内部命令
```
type cd
# cd is a shell builtin
help cd
```

### Command --help/-h
适用于外部命令
```
ls -h
ls --help
```

### man Command
manual 手册，是分章节；man # Command （#表示章节号）

### info Command
有超链接稳文档，info是信息页，提供作者、版本，什么时候发布等更详细信息，man是手册告诉你怎么用

### README google

> 内部命令实际上是shell程序的一部分，其中包含的是一些比较简单的linux系统命令，这些命令由shell程序识别并在shell程序内部完成运行，通常在linux系统加载运行时shell就被加载并驻留在系统内存中。内部命令是写在bashy源码里面的，其执行速度比外部命令快，因为解析内部命令shell不需要创建子进程。比如：exit，history，cd，echo等。
> 外部命令是linux系统中的实用程序部分，因为实用程序的功能通常都比较强大，所以其包含的程序量也会很大，在系统加载时并不随系统一起被加载到内存中，而是在需要时才将其调用内存。通常外部命令的实体并不包含在shell中，但是其命令执行过程是由shell程序控制的。shell程序管理外部命令执行的路径查找、加载存放，并控制命令的执行。外部命令是在bash之外额外安装的，通常放在/bin，/usr/bin，/sbin，/usr/sbin......等等。可通过“echo $PATH”命令查看外部命令的存储路径，比如：ls、vi等。
> 使用type区分命令类型


## chmod
chmod - change file mode bits

> -R, --recursive
  change files and directories recursively

read (4), write (2), and execute
(1)

`chmod -R 755 ./dist`
