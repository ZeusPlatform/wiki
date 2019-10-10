* what happened in windows software installation
* Differences Between .exe and .msi

## 注册表
HKEY_LOCAL_MACHINE 存放的是这个计算机的设置，

而 HKEY_CURRENT_USER 存放的是有关当前登录的用户的设置，

也就是说，不同的用户登录时 HKEY_CURRENT_USER 的内容是不同的，而 HKEY_LOCAL_MACHINE 是相同的。

还有，假设一个程序只能以管理员身份运行，那么将该程序写入到HKEY_CURRENT_USER时，开机后程序不能正常启动

但是将程序写入到HKEY_LOCAL_MACHINE时，开启会有uac（管理员运行提示）弹窗


## 开机自启动
参考链接： http://blog.sina.com.cn/s/blog_6334b9690100kapw.html
### shell:startup 用户自启动文件夹
C:\Users\yourname\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup

### shell:Common Startup 系统启动文件夹
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp

### RUN注册 RUN once注册
用户级：
计算机\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run

计算机\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce

系统级：
计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce

计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

总结以上就是可用的位置

备注： HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices (RunServicesOnce)
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunServices (RunServicesOnce)
windows10 已经不存在了

HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce\Setup

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\Setup
这两个启动项注册表中不存在，不确定新增的效果

## 自启动代码修改
未验证：参考：https://www.glbwl.com/regedit.html
Windows Registry Editor Version 5.00    [HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run]  "kugou"="C:\\Program Files (x86)\\KuGou\\KGMusic\\KuGou.exe"


## msi 对比 exe
如果要在计算机中放置新软件，则需要通过在线或本地购买或从Internet下载免费软件来获取安装程序。对于安装程序，您需要打开两个公用文件才能开始安装。一种具有MSI扩展名，一种具有EXE扩展名。这两个扩展之间的主要区别是它们的目的。EXE主要用于指示该文件是可执行文件。相比之下，MSI表示该文件是Windows安装程序。

虽然MSI仅与安装程序一起使用，但EXE并非如此。任何应用程序都需要至少具有一个EXE文件，因为它是启动应用程序进程所必需的。即使安装有EXE或MSI的程序也将具有一个或多个EXE文件。

其中一个创建安装包时使用MSI的优点，是一种标准的图形用户界面，可定制的一些可用性程度，但消除了创建自己的接口的复杂性。但是，如果您使用EXE文件，则可以完全自由地了解安装程序与用户的交互方式。在大多数使用EXE作为其安装程序的现代游戏中，这很明显。它们通常具有非常漂亮的交互界面，在等待安装完成的过程中使用户感到愉悦。

MSI的另一个优点是它具有执行安装或需求的能力。使用这种类型的安装，实际上只有链接和其他次要内容才放在计算机上。当用户首次尝试运行该程序时，便完成了实际安装。此时，MSI将打开必要的文件并完成安装过程。EXE文件无法执行此操作。

创建软件安装程序时，在EXE和MSI之间进行选择纯粹是基于您拥有的程序以及要投入安装程序的工作量。EXE为您提供了最大的控制权，但以创建安装程序所需的额外工作为代价。MSI则完全相反，通过符合预设标准简化了任务。

摘要：

1.EXE是可执行文件，而MSI是安装包。
2.MSI是安装程序专有的，而EXE不是。
3.MSI提供标准的GUI，而EXE提供GUI灵活性。
4.MSI可以按需安装，而EXE不能。



Read more: Difference Between MSI and EXE | Difference Between http://www.differencebetween.net/technology/software-technology/difference-between-msi-and-exe/#ixzz60omsVQZq
1. An EXE is an executable file while an MSI is an installation package.
2. MSI is exclusive to installers while EXE is not.
3. An MSI provides a standard GUI while an EXE provides GUI flexibility.
4. An MSI can do installation on demand while an EXE can’t.

Read more: Difference Between MSI and EXE | Difference Between http://www.differencebetween.net/technology/software-technology/difference-between-msi-and-exe/#ixzz60omhChL1
http://www.differencebetween.net/technology/software-technology/difference-between-msi-and-exe/

## Windows wim操作
### 查看
dism /get-wiminfo /wimfile:< path >
### 挂载
dism /mount-image /imagefile:< path > /index:1 /mountdir:< path >

### 查询可升级的版本
dism /image:< path > /get-targeteditions

### 升级版本
dism /Image:< path > /Set-Edition:< 版本名称 >

### commit镜像
dism /unmount-wim /mountdir:< path > /commit


## 杀死占用某端口的进程
netstat -ano | findstr 80 //列出进程极其占用的端口，且包含 80

tasklist | findstr 2000 找到进程名称，任务管理器杀死

taskkill -PID <进程号> -F //强制关闭某个进程
