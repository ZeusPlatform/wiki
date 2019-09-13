## 查看系统版本
lsb_release -a

## ip addr | grep eth0 查看网络ip

## linux 系统组成
* linux内核（linus 团队管理）
* shell：用户与内核交互的接口
* 文件系统：ext3、ext4等。windows 有 fat32 、ntfs
* 第三方应用软件

## shell
Shell是系统的用户界面，提供了用户与内核进行交互操作的一种接口(命令解释器)
* 内部命令
* 应用程序
* shell脚本

## type区分是否内部命令
## shell 可以做什么
* 命令行解释(这是用得最多的！)
* 命令的多种执行顺序
* 通配符（ wild-card characters ）
* 命令补全、别名机制、命令历史
* I/O重定向（ Input/output redirection ）
* 管道（ pipes ）
* 命令替换（ 或$( ) ）
* Shell编程语言（ Shell Script ）