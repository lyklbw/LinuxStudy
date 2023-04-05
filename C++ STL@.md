# C++ STL

### 1.vector

> 动态数组
>
> 定义的vector数组可以随时添加数值和删除元素.

##### 1.1**头文件**

```c++
#include<vector>
```

##### 1.2初始化

* 一维

  ```c++
  vector<int>num;//定义了一个名为num的存int数据的一维数组
  vector<node>num;//node是结构体类型
  ```

  指定**长度**和**初始值**的初始化

  ```cpp
  vector<int> v(n);//定义一个长度为n的数组，动态定义，不指定初值默认初值为0
  vector<int> v(n, 0);//所有的元素均为0
  ```

  注意：指定长度后的数组就相当于正常的数组了

  初始化中有**多个元素**

  ```
  vector<int> a{1, 2, 3, 4, 5};// 数组a中有五个元素
  ```

  拷贝初始化

  ```cpp
  vector<int> a(n + 1, 0);
  vector<int> b(a);//两个数组中的类型必须相同
  ```

* 二维

  定义第一维固定长度为`5`，第二维可变化的二维数组

  ```c++
  vector<int>num[5];//定义可变长二维数组
  //注意：行是不可变的（只有5行），而列可变可以在指定行添加元素
  //第一维固定长度为5，第二维长度可以改变
  ```

  行列均可变(多维数组)

  ```
  vector<vector<int>>num;
  ```

##### 1.3访问

```
//方式一：单个访问，假设num数组中已经有了5个元素
cout << num[4] << "\n";  //输出第五个数据
//一二维可变数组和普通数组的访问方法一样

//方式二:遍历
for(int i = 0; i < num.size(); i++)
	cout << num[i] << " ";
```

##### **<u>1.4方法函数</u>**

| 代码                           | 含义               |
| ------------------------------ | ------------------ |
| name.front()                   | 返回第一个数据     |
| name.size()                    | 返回容器中数据数量 |
| name.push_back(element)        | 添加一个数据在最后 |
| name.pop_back()                | 删除最后一个数据   |
| name.begin()                   | 返回s首元素地址    |
| name.insert(name.begin()+2,-1) | 将-1插入c[2]的位置 |
| name.clear()                   | 清除所有数据       |

##### 1.5注意事项

###### 排序

`sort(name.begin,name.end);`

对所有元素进行排序，如果要对指定区间进行排序，可以对sort()里面的参数进行加减改动。

###### 访问

* 下标法：与普通数组一致

* 迭代器：类似指针一样的访问 ，首先需要声明迭代器变量，和声明指针变量一样

  ```
  vector<int> vi; //定义一个vi数组
  vector<int>::iterator it = vi.begin();//声明一个迭代器指向vi的初始位置
  ```

  访问实例

  ```
  //方式一：
  vector<int>::iterator it = vi.begin(); 
  for(int i = 0; i < 5; i++)
  	cout << *(it + i) << " ";
  cout << "\n";
  //方式二：
  vector<int>::iterator it;
  for(it = vi.begin(); it != vi.end();it ++)
  	cout << *it << " ";
  //vi.end()指向尾元素地址的下一个地址
  ```


### 2.queue

| 函数    | 功能                 |
| :------ | -------------------- |
| back()  | 返回最后一个元素     |
| front() | 返回第一个元素       |
| empty() | 如果队列空则返回真   |
| pop()   | 删除第一个元素       |
| push()  | 在末尾加入一个元素   |
| size()  | 返回队列中元素的个数 |



### 3.map

> map提供一对一（其中第一个可以称为关键字，每个关键字只能在map中出现一次，第二个可能称为该关键字的值）的数据 处理能力，由于这个特性，它完全有可能在我们处理一对一数据的时候，在编程上提供快速通道。
>
> 这里说下map内部数据的组织，map内部自建一颗红黑树(一 种非严格意义上的平衡二叉树)，这颗树具有对数据自动排序的功能，所以在map内部所有的数据都是有序的，后边我们会见识到有序的好处。

##### 基本用法

###### 1.头文件

```
#include<map>
```

###### 2.定义及赋值

```c++
map<int,string>student;
/* (1) */
student.insert(pair(001,"lbw"));
student.insert(pair(002,"mff"));
/* (2) */
student[001]="lbw";
student[002]="mff";
```

###### 3.查找

* `name.cout(key)`

  > map变量.count(key) 只返回0或1，0表示map变量中不 包含key这个键，1则表示包括

* `name.find(key)`

  map变量.find(key) 返回一个迭代器，存在key这个元素的时候,该迭代器指向查询到的这个元素，无则返回name.end()

```
map<int,string> ::iterator it=student.find(001);
return it->second;
/*  迭代器名称->first  表示迭代器当前指向的元素的key;   迭代器名称->second 表示迭代器当前指向的元素的value;*/
```

###### 4.删除,清空

```
/* (1) */
map<int,string> ::iterator it=student.find(001);
int ans = student.erase(it);

/* (2) */
int ans =student.erase(001);

//删除
student.clear();
```

###### 5.遍历

```c++
//auto 可以自动识别类型
auto it = student.begin();
while(it != student.end()){
	cout<<it->first<<" "<<it->second<<endl;
	it ++;
}
```

