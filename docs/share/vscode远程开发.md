## [是什么]https://code.visualstudio.com/docs/remote/remote-overview
> P.S: 该功能目前仅支持在 Insider 版本中使用，当然最终也会在 Stable 版本中提供。

这次发布包含了三款核心的全新插件，它们可以帮助开发者在容器、物理机器或虚拟机，以及 Windows Subsystem for Linux (WSL) 中实现无缝的远程开发。通过安装 Remote Development Extension Pack ，你可以快速上手远程开发。

vscode 扩展下载 Remote Development
VS Code远程开发
Visual Studio Code远程开发允许您使用容器，远程计算机或Linux的Windows子系统（WSL）作为功能齐全的开发环境。您可以：

在您部署到的同一操作系统上进行开发，或使用更大或更专业的硬件。
将开发环境沙盒化，以免影响本地计算机配置。
使新贡献者易于上手，并使每个人都保持一致的环境。
使用本地操作系统上不可用的工具或运行时，或管理它们的多个版本。
使用Windows Linux子系统开发部署了Linux的应用程序。
从多台机器或位置访问现有的开发环境。
调试在其他位置（例如客户站点或云中）运行的应用程序。
要获得这些好处，您的本地计算机上不需要任何源代码。Remote Development扩展包中的每个扩展都可以直接在容器中，WSL中或在远程计算机上运行命令和其他扩展，因此一切都像在本地运行时一样。

![](https://code.visualstudio.com/assets/docs/remote/remote-overview/architecture.png)

入门
远程开发扩展包
该远程开发扩展包包括三个扩展。请参阅以下文章，以开始使用它们：

远程-SSH-通过使用SSH打开远程计算机/ VM上的文件夹来连接到任何位置。
远程-容器 -在容器内部（或安装到容器中）使用沙盒工具链或基于容器的应用程序。
远程-WSL-在Windows子系统中获得Linux驱动的Linux开发经验。
教程 -分步教程可帮助您在远程环境中快速运行。
尽管大多数VS Code扩展都应该在远程环境中保持不变，但是扩展作者可以在Supporting Remote Development上了解更多信息。


Remote Development extension pack 包括三个扩展：

Remote - SSH - 通过使用 SSH 打开远程计算机或者VM上的文件夹，来连接到任何位置。

Remote - Containers – 把 Docker 作为你的开发容器。

Remote - WSL - 在 Windows Subsystem for Linux 中，获得 Linux 般的开发体验。

### Remote – SSH

在比本地机器更大、更快或更专业的硬件上进行开发。

在不同的远程开发环境之间快速切换，安全地进行更新，而不必担心影响本地计算机。

调试在其他位置运行的应用程序，例如客户网站或云端。

例如，假设你正在开展深度学习项目。您通常需要一个高GPU性能的虚拟机（例如 Azure Data Science Virtual Machine），配置了训练大数据模型所需的所有工具和框架。

你可以使用 Vim over SSH 或 Jupyter Notebooks 来编辑远程代码，但是你放弃了本地开发工具的丰富功能。相反地，使用 Remote-SSH 扩展，你只需连接到 VM，安装必要的扩展（如 Python 插件），然后你就可以利用VS Code的所有强大功能，如 IntelliSense、代码跳转和调试，就像你在本地开发一样。

使用SSH进行远程开发
在Visual Studio代码远程- SSH扩展允许你打开任何远程计算机，虚拟机或容器上的远程文件夹与正在运行的SSH服务器，并充分利用VS代码的功能集。连接到服务器后，您可以与远程文件系统上任何位置的文件和文件夹进行交互。

由于扩展名直接在远程计算机上运行命令和其他扩展名，因此无需在本地计算机上使用源代码即可获得这些好处。
![](https://code.visualstudio.com/assets/docs/remote/ssh/architecture-ssh.png)

SSH架构

这使得VS Code可以提供本地质量的开发体验 -包括完整的IntelliSense（完成功能），代码导航和调试- 不管代码托管在何处。

### Remote – Containers


您可以在部署的同一操作系统上，使用一致的工具链进行开发。

容器是隔离的，这意味着你可以在不影响本地计算机的情况下在不同的开发环境之间快速切换。

其他人可以轻松地为您的项目做出贡献，因为他们可以在一致的开发环境中轻松开发、构建和测试。

一个 devcontainer.json 文件可以被用来告诉 VS Code 如何配置开发容器，包括使用的 Dockerfile、端口映射以及在容器中安装


### Remote – WSL


使用 Windows 在基于 Linux 的环境中进行开发，使用平台特定的工具链和程序。

编辑位于 WSL 中的文件或挂载的 Windows 文件系统（例如 /mnt/c）。

在 Windows 上运行和调试基于 Linux 的应用程序。

插件直接在 Linux 发行版中运行，因此你不需要担心路径问题、软件兼容性或其他跨平台的问题。你可以像在 Windows 中一样，在 WSL 中无缝地使用 VS Code。 
在WSL中开发
在Visual Studio代码远程- WSL扩展允许您使用的Windows子系统为Linux（WSL）作为直接从VS代码您的全职开发环境。您可以在基于Linux的环境中进行开发，使用特定于Linux的工具链和实用程序，以及在Windows的舒适环境下运行和调试基于Linux的应用程序。

该扩展名直接在WSL中运行命令和其他扩展名，因此您可以编辑WSL或已安装的Windows文件系统中的文件（例如/mnt/c），而不必担心路径问题，二进制兼容性或其他跨OS挑战。

WSL体系结构

这使得VS Code可以提供本地质量的开发体验 -包括完整的IntelliSense（完成功能），代码导航和调试- 不管代码托管在何处。
![](https://code.visualstudio.com/assets/docs/remote/wsl/architecture-wsl.png)

## 背景


## 未来


## dockerfile + vscode 最原始
最初的设想，是为每一个工程搭配使用docker的 dockerfile 将windows本地的代码挂在docker中，然后本地的代码改动也可以同步到docker容器中

缺点：
1. 为每一个工程配置的dockefile 改动过大
2. 跨文件的webpack watch
3. 性能问题

## vscode + wsl

### [安装windows预览版](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewadvanced)
> 直接加入windows预览版计划升级fast ring ，然后升级到预览版可能会使得一些软件不能正常使用



## vscode + docker
### docker 一些技术点

## 总结



