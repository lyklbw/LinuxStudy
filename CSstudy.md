# CSSTUDY

### 序言：关于系统

windows中常见的磁盘格式有fat16、fat32和ntfs。windows是一个封闭的系统。无法打开ext3或者mac 日志式。

在ubuntu中其文件系统广泛使用ext3(ext4是ext3的扩展)的文件格式，从而实现了将整个硬盘的写入动作完整的记录在磁盘的某个区域上。而且在ubuntu中可以实现主动挂载windows的文件系统，并以只读的方式访问磁盘中windows系统上的文件。

在ubuntu中磁盘文件系统、网络文件系统都可以非常方便的使用，而屏蔽了网络和本地之间的差异。在ubuntu中所有的文件都是基于目录的方式存储的。一切都是目录，一切都是文件。

/是一切目录的起点，如大树的主干。其它的所有目录都是基于树干的枝条或者枝叶。在ubuntu中硬件设备如光驱、软驱、usb设备都将挂载到这颗繁茂的枝干之下，作为文件来管理。

/bin: bin是Binary的缩写。存放系统中最常用的可执行文件（二进制）。

/boot: 这里存放的是linux内核和系统启动文件，包括Grub、lilo启动器程序。

/dev: dev是Device(设备)的缩写。该目录存放的是Linux的外部设备，如硬盘、分区、键盘、鼠标、usb等。

/etc: 这个目录用来存放所有的系统管理所需要的配置文件和子目录，如passwd、hostname等。

/home: 用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

/lib: 存放共享的库文件，包含许多被/bin和/sbin中程序使用的库文件。

/lost+found: 这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些零散文件。

/media: ubuntu系统自动挂载的光驱、usb设备，存放临时读入的文件。

/mnt: 作为被挂载的文件系统得挂载点。

/opt: 作为可选文件和程序的存放目录，主要被第三方开发者用来简易安装和卸载他们的软件。

/proc: 这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。这里存放所有标志为文件的进程，比较cpuinfo存放cpu当前工作状态的数据。

/root: 该目录为系统管理员，也称作超级权限者的用户主目录。

/sbin: s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序，如系统管理、目录查询等关键命令文件。

/ srv: 存放系统所提供的服务数据。

/sys: 系统设备和文件层次结构，并向用户程序提供详细的内核数据信息。

/tmp: 这个目录是用来存放一些临时文件的，所有用户对此目录都有读写权限。

/usr: 存放与系统用户有关的文件和目录。

/usr 目录具体来说：

/usr/X11R6: 存放X-Windows的目录；

/usr/games: 存放着XteamLinux自带的小游戏；

/usr/bin: 用户和管理员的标准命令；

/usr/sbin: 存放root超级用户使用的管理程序；

/usr/doc: Linux技术文档；

/usr/include: 用来存放Linux下开发和编译应用程序所需要的头文件，for c 或者c++；

/usr/lib: 应用程序和程序包的连接库；

/usr/local: 系统管理员安装的应用程序目录；

/usr/man: 帮助文档所在的目录；

/usr/src: Linux开放的源代码；

/var: 长度可变的文件，尤其是些记录数据，如日志文件和打印机文件。

/var/cache: 应用程序缓存目录；

/var/crash: 系统错误信息；

/var/games: 游戏数据；

/var/log: 日志文件；

/var/mail: 电子邮件；

/var/tmp: 临时文件目录；

### 第一课：shell

* **引入**：如今的计算机有着多种多样的交互接口让我们可以进行指令的的输入，为了充分利用计算机的能力，我们不得不回到最根本的方式，使用文字接口：Shell

```
lyk@LYKdiandong:~/lbwnb/myfile/vacation rise/markdown$ 
```

​		$表示您当前的身份并非超级用户

一些简单的命令：

`date`(打印当前时间)

​		shell 是一个编程环境，所以它具备变量、条件、循环和函数（下一课进行讲解）。当你在 shell 中执行命令时，您实际上是在执行一段  shell 可以解释执行的简短代码。如果你要求 shell 执行某个指令，但是该指令并不是 shell 所了解的编程关键字，那么它会去咨询 *环境变量*  `$PATH`，它会列出当 shell 接到某条指令时，进行程序搜索的路径

`echo`(输出

```
lyk@LYKdiandong:~/lbwnb/myfile/vacation rise/markdown$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
```

​		如果某个路径以 `/` 开头，那么它是一个 *绝对路径*，其他的都是 *相对路径* 。相对路径是指相对于当前工作目录的路径，当前工作目录可以使用 `pwd` 命令来获取。

在程序间创建连接

```
echo hello > hello.txt
cat hello.txt > hello2.txt
cat hello2.txt
输出： hello
```

`super user `

有一件事情是您必须作为根用户才能做的，那就是向 `sysfs` 文件写入内容。系统被挂载在 `/sys` 下，`sysfs` 文件则暴露了一些内核（kernel）参数。 因此，您不需要借助任何专用的工具，就可以轻松地在运行期间配置系统内核

​		系统的屏幕亮度写在

​		`/sys/class/backlight/intel_backlight`中

​		若要改变屏幕亮度：`sudo echo 3 > brightness`

​		这一指令是错误的

​		正确操作为

```
echo 3 | sudo tee brightness
```

作业部分



```
lyk@LYKdiandong:~/lbwnb/myfile/vacation rise/missing$ ls -l
总用量 4
-rw-rw-r-- 1 lyk lyk 61  2月 26 13:51 semester
lyk@LYKdiandong:~/lbwnb/myfile/vacation rise/missing$ chmod 777 semester 
lyk@LYKdiandong:~/lbwnb/myfile/vacation rise/missing$ ls -l
总用量 4
-rwxrwxrwx 1 lyk lyk 61  2月 26 13:51 semester
```

		lyk@LYKdiandong:~/lbwnb/myfile/vacation rise/missing$ ./semester | grep last-modified > ~/last_modified.txt


### 第二课：shell工具与脚本

在bash中为变量赋值的语法是`foo=bar`，访问变量中存储的数值，其语法为 `$foo`。 需要注意的是，`foo = bar` （使用空格隔开）是不能正确工作的，因为解释器会调用程序`foo` 并将 `=` 和 `bar`作为参数。 总的来说，在shell脚本中使用空格会起到分割参数的作用，有时候可能会造成混淆，请务必多加检查。

Bash中的字符串通过`'` 和 `"`分隔符来定义，但是它们的含义并不相同。以`'`定义的字符串为原义字符串，其中的变量不会被转义，而 `"`定义的字符串会将变量值进行替换。

```
foo=bar
echo "$foo"
# 打印 bar
echo '$foo'
# 打印 $foo
```

和其他大多数的编程语言一样，`bash`也支持`if`, `case`, `while` 和 `for` 这些控制流关键字。同样地， `bash` 也支持函数，它可以接受参数并基于参数进行操作。下面这个函数是一个例子，它会创建一个文件夹并使用`cd`进入该文件夹。

```
mcd () {
    mkdir -p "$1"
    cd "$1"
}
```

这里 `$1` 是脚本的第一个参数。与其他脚本语言不同的是，bash使用了很多特殊的变量来表示参数、错误代码和相关变量。下面是列举来其中一些变量，更完整的列表可以参考 [这里](https://www.tldp.org/LDP/abs/html/special-chars.html)。

- `$0` - 脚本名
- `$1` 到 `$9` - 脚本的参数。 `$1` 是第一个参数，依此类推。
- `$@` - 所有参数
- `$#` - 参数个数
- `$?` - 前一个命令的返回值
- `$$` - 当前脚本的进程识别码
- `!!` - 完整的上一条命令，包括参数。常见应用：当你因为权限不足执行命令失败时，可以使用 `sudo !!`再尝试一次。
- `$_` - 上一条命令的最后一个参数。如果你正在使用的是交互式 shell，你可以通过按下 `Esc` 之后键入 . 来获取这个值。

​		
