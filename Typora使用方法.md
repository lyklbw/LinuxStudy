# Typora使用方法

## 1.基础使用

### 1.1 标题

* #一级标题 ##二级标题 ###三级 并以此类推

  补充一句两次回车有奇效

### 1.2 列表

* 无序列表使用(*)(+)(-)进行标记
* 有序列表加1. 2. 3. 等来表示 
* 列表嵌套：（在子列表之前添加四个空格）
  1. 第一项：    
        *  第一元素
        *  第二元素
  2. 第二项：
        *  老二的第一元素
        *  第二

###  1.3 区块

*  Markdown区块引用是在段落开头使用>符号，然后后面紧跟一个空格符号：

> 区块化使用markdown真爽 

* 区块化可嵌套（几个“>"就几层）

  > 最外层

  > > 第一层(累退)

* 列表使用区块化，区块使用列表都可以哈哈哈

  > * 第一级别
  >       * 第二级别1
  >       * 第二级别2

下面这个好像和区块关系不紧密细细

* 三个-效果如下：(分割线)

---



### 1.4 代码框框

* 一个函数或者片段代码使用前后两个`（有点坑，这东西在1的旁边）

  `BubbleSort`函数

* 整段代码区块(使用三个` 加Enter+编程语言)

  ```c++
  #include<iostream>
  using namespace std;
  int main(){
      cout<<"helloworld"<<endl;
      return 0;
  }
  ```



### 1.5 链接

* 有两种方法：
      1. [百度](hhtp://www.baidu.com/)[文字]括号里面为链接地址
          1. <链接地址>

* 链接可以打开本地文件(注意路径)
* 也可实现页面跳转[标题](###1.1 标题)(Ctrl并点击触发)

### 1.6 图片(imp)

1. 网页图片显示：

   开头一个感叹号! 接着一个方括号，里面放上图片的代替文字，接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上选择性的'title'属性文字。(此方法快捷键为 shift+ctrl+i)

实例

`![有问题上知乎 图标](https://pic4.zhimg.com/80/v2-a47051e92cf74930bedd7469978e6c08_hd.png)`

图片显示：

![有问题上知乎 图标](https://pic4.zhimg.com/80/v2-a47051e92cf74930bedd7469978e6c08_hd.png)

2. 本地图片显示：

   `![image-20230101160358608](/home/lyk/.config/Typora/typora-user-images/image-20230101160358608.png)`

![image-20230101160358608](/home/lyk/.config/Typora/typora-user-images/image-20230101160358608.png)

3. 牛刀小试

   下面为所显示的图片

![learning](/home/lyk/lbwnb/myfile/vacation rise/images/learning.png)

​    成功嘻嘻嘻

### 1.7 表格

* 不上废话 Ctrl+t yyds , 第一行为列说明 会自动加粗
* shift + ctrl + Backspace 删除所在行
* ctrl + enter 添加末尾行

|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |

### 1.8 字体使用

* 快捷方式会讲斜体粗体

* 文字颜色

  模板：

  `<span style="color:文字颜色;background:背景颜色;font-size:文字大小;font-family:字体;">你要改色的文字</span>`	

  简单版本：

  ```
  <font color='red'>红色</font>
  ```
  
  <font color='red'>红色</font>
  
  实例	
  
  `<span style="color:blue;background:pink;">蓝色字体 </span>`					
  
  <span style="color:blue;background:pink;">蓝色字体 </span>
  
  <span style="color :red;background:pink;">Jordan</span>

### 1.9 其他说明

* 删除线 

​		`~~文本～～`

​		~~卢本位~~

* 下划线

​		`<u>文本</u>`

​		<u>伞兵一号</u>

* 反斜杠来帮助插入普通符号 \\

  \###

* `:`加英文 表情包

  :walking:

  :sun_with_face:

## 2.快捷方式

| Ctrl+I       | *斜体文本*        |
| ------------ | ----------------- |
| Ctrl+B       | **粗体文本**      |
| Ctrl+SHIFT+I | 插入图片(insert)  |
| Ctrl+U       | 下划线(underline) |
| Ctrl+H       | 全文替代          |
| Ctrl+S       | 保存              |
| Ctrl+Shift+S | 另存为            |
| Ctrl+N       | 新建              |
|              |                   |
|              |                   |

to be continued
