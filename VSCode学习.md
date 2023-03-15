# VSCode学习

### 前言

> vs的确可以在初期帮助小白偷懒，但是终究是要补过的，接下来记录vscode中C++环境的配置

确切地说，**vscode** 只是一款文本编辑器，它和你电脑上的记事本并没有什么两样，甚至word也是。

但vscode可以扩展为任何你想要的

那既然只是一款文本编辑器，为什么vscode可以用作c/c++，甚至是一切语言的开发环境呢？

1.vscode集成了终端系统，可以在其内部调用命令行终端，而命令行终端可以完成将代码变成程序这个任务。

2.vscode可以设置一些选项，使得能在上条中提到的命令行终端中执行一套命令，调用语言编译器对代码进行编译等，变成程序。

3.vscode可以装一些对应语言的插件，使得开发环境更加完善。

### 幕后——编译器准备

目前主流的C/C++编译器，Linux平台有 `gcc` (我哭死，此时相见竟已物是人非），Windows平台有 `msvc` ，MacOS平台有 `clang` ，但我们选用 `gcc` 作为编译器。

我们选择gcc，因为其较长的历史积淀以及成熟性。

但是， gcc 是 Linux 平台的，怎么用于 Windows 呢？

我们需要用到 MinGW-w64 ，全名Minimalist GNU for Windows，是Linux平台上的一套开发工具，移植到Windows平台。这之中，就有我们需要的gcc。

不管你通过何种方式得到了 *x86_64-12.2.0-release-posix-seh-ucrt-rt_v10-rev2.7z或.zip* 这个压缩包，现在请把它解压到除了C盘以外，不带中文路径不带空格的一片地方，与 vscode 的要求相同。

[(96条消息) mingw64安装和环境变量配置教程_mingw64 环境变量_山水:的博客-CSDN博客](https://blog.csdn.net/woxingzou/article/details/113746142)

这是环境变量设置的步骤（很清晰明了）

### 配置VScode

下载扩展 Better C++ Syntax （语法高光）

C++环境需要 .vscode 文件夹下的 *c_cpp_properties.json,tasks.json,launch.json* 这三个文件共同定义。

补充整体替换操作：
ctrl shift +h









