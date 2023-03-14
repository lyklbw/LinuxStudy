# cmake!

### 1.opencv的CMakeLists.txt（new）

我们知道makefile是在Linux编译c或者c++代码的时候的一种脚本文件，但是每一个功能都要写一个makefile文件，这样如果这个工程很大，而且相关性比较强的话，makefile的书写就会变得相对繁琐，更要命的是如果以后需要添加新的功能或者是新人需要修改功能的话，看起来就会特别麻烦。那么此时`**CMakeLists.txt`以及其配套的`cmake`应运而生

下面是我在上学期使用的：的`CMakeLists`

```
cmake_minimum_required(VERSION 2.8)
project(untitled1 )
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS} )
add_executable( main main.cpp )
target_link_libraries(main ${OpenCV_LIBS} )
```

网上的`cmake`的`CMakeLists`教程：

```
cmake_minimum_required(VERSION 2.8)

Project(Test1)

find_package(OpenCV REQUIRED)

##下面是输出信息
message(STATUS "Opnecv ;ibrary status: ")
message(STATUS "> version: ${OpenCV_VERSION} ")
message(STATUS "libraries: ${OpenCV_LIBS} ")
message(STATUS "> include: ${OpenCV_INCLUDE_DIRS}  ")


include_directories(${OpenCV_INCLUDE_DIRS}) 


add_executable(Test2 test.cpp)

target_link_libraries(Test2 ${OpenCV_LIBS})
```

第一行`cmake_minimum_required(VERSION 2.8)：`

该命令指定了编译该工程对`cmake`的最高、最低版本要求，如果 `CMake `的运行版本低于所需版本，它将停止处理项目并报告错误。

第二行`project`不是强制性的，最好加上，这会引入两个变量：`Test1_BINARY_DIR, Test1_SOURCE_DIR`，同时也会定义两个等价的变量：`PROJECT_BINARY_DIR,  PROJECT_SOURCE_DIR`，外部编译要时刻区分这两个变量对应的目录。可以通过message进行输出，message(${PROJECT_SOURCE_DIR})

第三行f`ind_package： `

`CMake`本身不提供任何关于搜索库的便捷方法，也不会对库本身的环境变量进行设置。它仅仅是按照优先级顺序在指定的搜索路径进行查找   `Findxxx.cmake  ` 文件和`xxxConfig.cmake`文件(其中`xxx`代表库的名字，特别注意的是有大小写之分)，这两个文件大体上是没有区别的，`CMake`   能够找到这两个文件中的任何一个，我们都能成功使用该库，当我们在终端键入 `make.. `命令之后，`CMake `会读取并执行  `CMakeLists.txt` 中的代码，当执行  find_package() 这条命令后，`CMake` 就会从某些路径中找这  `Findxxx.cmake `文件或者`xxxConfig.cmake  `文件，`CMake ` 找到任意一个之后就会执行这个文件，然后这个文件执行后就会设置好一些 `CMake` 变量。比如下面的变量（NAME 表示库的名字 比如可以用  `Opencv `代表 `Opencv`库）

第八行`include_directories`：

将指定目录添加到编译器的头文件搜索路径之下，指定的目录被解释成当前源码路径的相对路径，也就是告诉`cpp`它的各种include的搜索路径为`${OpenCV_INCLUDE_DIRS}`

第九行`add_executable(Test2 test.cpp)`：

使用指定的源文件来生成目标可执行文件。注意这里的名字可以和项目名字不一样，为做区分我写为`Test2`

第十行：`target_link_libraries(Test2 ${OpenCV_LIBS})`：

该指令的作用为将目标文件与库文件进行链接，一些动态连接库需要在程序运行阶段才被调用（我个人理解），因此这里也是`Test2`，需要和可执行文件名称一样

### ps1

1.问题：`CV_GRAY2BGR`参数未定义

`CV_GRAY2BGR`参数改为`COLOR_GRAY2BGR`参数即可解决报错

2.问题：`CV_WINDOW_AUTOSIZE’ was not declared in this scope`

`#include <opencv2/highgui/highgui_c.h>`头文件添加即可

### 2.cmake深入学习

`SET(SRC_LIST  main.c  t1.c  t2.c)`

显式的定义变量(此处将所有源文件以变量代替)

之后的` ADD_EXECUTABLE(hello ${SRC_LIST})`

使用${}来引用变量

IF 是直接使用变量名



指令不分大小，变量参数大小相关



运行make clean 可以对构建结果清理

(可以重新make)



build

所谓的 out-of-source 外部编译，一个最大的好处是，对于原有的工程没有任何影响，所有动作全部发生在编译目录。通过这一点，也足以说服我们全部采用外部编译方式构建工程。



```python
aux_source_directory(. DIR_SRCS)
```



```
SET（SRC_LST main.c other.c)
```

用SRC_LST代替后面的字符串



```
add_libreary(MathFunction ${DIR_SRCS})
```

添加源文件



```
add_executable(main main.c)
target_link_libraries(main MathFunction)
```





```
TARGET_INCLUDE_DIRECTORIES(caculate ${OPencv _Include_dir})
```

指定目标包含的头文件路径



外部构建

任何一个子目录都需要一个CMakeLists.txt

```
.
├── build
│   ├── bin
│   │   ├── CMakeFiles...
│   │   ├── cmake_install.cmake
│   │   ├── Makefile
│   │   └── t2
│   ├── CMakeCache.txt
│   ├── CMakeFiles
│   │   ├── 3.22.1
│   ├── cmake_install.cmake
│   └── Makefile...
├── CMakeLists.txt
└── src
    ├── CMakeLists.txt
    └── main.c
```

ADD_SUBDIRECTORY(source_dir [binary_dir])

添加源文件子目录 并指定输出路径

> 如果不进行 bin 目录的指定，那么编译结果(包括中间结果)都将存放于  build/src  目录(这个目录跟原有的 src 目录对应)
>
> 指定 bin 目录后，相当于在编译时
> 将 src 重命名为 bin，所有的中间结果和目标二进制都将存放在 bin 目录

不论是 SUBDIRS 还是 ADD_SUBDIRECTORY 指令(不论是否指定编译输出目录)，我们都可以通过 SET 指令重新定义 EXECUTABLE_OUTPUT_PATH 和 LIBRARY_OUTPUT_PATH 变量
来指定最终的目标二进制的位置(指最终生成的 hello 或者最终的共享库，不包含编译生成的中间文件)
SET(EXECUTABLE_OUTPUT_PATH${PROJECT_BINARY_DIR}/bin)
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
在第一节我们提到了<pro_name>_BINARY_DIR 和 PROJECT_BINARY_DIR 变量，他们指的**<u>编译发生的当前目录</u>**，如果是内部编译，就相当于 PROJECT_SOURCE_DIR 也就是
工程代码所在目录，如果是外部编译，指的是外部编译所在目录，也就是本例中的 build目录

> 本例不用讨论第二个指令



()
