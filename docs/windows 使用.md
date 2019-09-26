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
