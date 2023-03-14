# OpenCV

> Open Source Computer Vison Library

##### `VideoCapture`

###### 普通读取视频

```
读取
/* (1) */
VideoCapture capture;
capture.open("1.avi");
/* (2) */
VideoCapture capture("1.avi");
while(1){
	Mat frame；
	capture>>frame;//读取当前帧
	imshow("读取"，frame);
	waitKey(30);
}
```

###### 读取摄像头

```
#incldue<opencv2/opencv.hpp>
using namespace cv;
int main(){
	VideoCapture(0);
	while(1){
	Mat frame;
	capture>>frame;
	imshow(0);
	waitKey(30);
	}
}
```

##### `头文件`

`<opencv2/opencv.hpp>`

本身包含了 `core objdetect imgproc photo video features2d objectect calib3d ml highgui contrib`

##### `argc argv`

```
int main(int argc,char* argv[])
```

`argc`用于统计程序运行时发给main的命令参数个数

`argv`用于存放指向字符串参数的指针数组

`argv[0]`:指向程序的全路径名

`argv[n]`:指向第n个字符串(n>0)

##### `Mat`

`cv::Mat picture(320,640,cv::Scalar(100));`

`Mat img=imread("1.jpg");`

##### `namedWindow`

在普通显示图像时并没有司马必要

但是后面滑动条函数会用到

参数:

```
WINDOW_NORMAL// 用户可以改变窗口的带小
WINDOW——AUTOSIZE //自适应，用户无法改变
```

##### `imwrite`

> bool imwrite(const&string& filename,InputArray img,const vector<int>不用管)

##### `createTrackbar`

```
 参数1：滑动条轨迹名
 参数2：滑动条依附的窗口名
 参数3：滑块的位置，创建时，滑块初始位置就是这个变量当前的值
 参数4：轨迹的最大值
 参数5：回调函数
 参数6：默认0，用户传给回调函数的数据，如果第三个值为全局变量，忽略这个值.         
```

#### `图像融合`

##### `Rect()函数`

Rect(x,y,width,height)

##### `Mat(src,rect)`

参数1：给定的Mat类矩阵
 参数2: 指定的矩形区域

##### `addweight`

dst = src1 * alpha + src2 * beta + gamma;

构造函数：addWeight(Inputarray src1, double alpha, Inputarray src2, double beta, double gamma, outputarray dst, int dtype=-1)
参数1：输入的第一个数组。
参数2：alpha值
参数3：输入的第二个数组。
参数4：beta值
参数5：输出计算结果。
参数6：选择输出数组的深度，如果输入的两个数组深度相同，则设置为-1，
