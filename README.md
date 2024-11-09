
**一、介绍**　　　　今天是这个系列《C\+\+之 Opencv 入门到提高》得第四篇文章。这篇文章很简单，介绍如何使用 Mat 对象来实例化图像实例，了解它的构造函数和常用的方法，这是基础，为以后的学习做好铺垫。虽然操作很简单，但是背后有很多东西需要我们深究，才能做到知其然知其所以然。OpenCV 具体的简介内容，我就不多说了，网上很多，大家可以自行脑补。　　　　OpenCV 的官网地址：[https://opencv.org/](https://github.com)，组件下载地址：[https://opencv.org/releases/](https://github.com):[悠兔机场](https://xinnongbo.com)。　　　　OpenCV 官网学习网站：[https://docs.opencv.ac.cn/4\.10\.0/index.html](https://github.com)　　　　我需要进行说明，以防大家不清楚，具体情况我已经罗列出来。　　　　　　　　操作系统：Windows Professional 10（64位）　　　　　　　　开发组件：OpenCV – 4\.10\.0　　　　　　　　开发工具：Microsoft Visual Studio Community 2022 (64 位) \- Current版本 17\.8\.3　　　　　　　　开发语言：C\+\+（VC16）**二、知识学习**　　　　如果我们想学习或者使用 OpenCV，它的图像对象 Mat 是绕不过去的。我们对它越熟悉，使用的越灵活。俗话说得好，欲善其事必先利其器。内容很简单，直接上代码，代码里面有注释。废话不说了。


```
  1 #include 
  2 #include 
  3 #include 
  4 
  5 using namespace std;
  6 using namespace cv;
  7 
  8 int main()
  9 {
 10     //1、Mat 对象与 IplImage 对象
 11     // 1.1、IplImage 对象是从 2001 年 OpenCV 发布之后就一直存在的，它是一个具有 C 语言风格的数据结构，需要开发者自己分配和管理内存，在大型项目中容易导致内存泄漏。
 12     // 1.2、Mat 对象是在 OpenCV 2.0 之后才引进的图像数据结构，自动分配内存，不存在内存泄漏的问题，是下面向对象的数据结构。该 Mat 对象分成两部分，头部和数据部分。
 13     // 1.3、 Mat 类型构造函数和常用方法。
 14     // 
 15     // 1.3.1、构造函数
 16     // 1.3.1.1、Mat()
 17     // 1.3.1.2、Mat(int rows, int cols, int type);
 18     // 1.3.1.3、Mat(Size size, int type);
 19     // 1.3.1.4、Mat(int rows, int cols, int type, const Scalar& s);
 20     // 1.3.1.5、Mat(Size size, int type, const Scalar& s);
 21     // 1.3.1.6、Mat(int ndims, const int* sizes, int type);
 22     // 1.3.1.7、Mat(int ndims, const int* sizes, int type, const Scalar& s);
 23     // 还有很多，就不列举了
 24     // 
 25     // 1.3.2、常用方法
 26     // 1.3.2.1、void copyTo( OutputArray m ) const;
 27     // 1.3.2.2、void convertTo( OutputArray m, int rtype, double alpha=1, double beta=0 ) const;
 28     // 1.3.2.3、Mat clone() const; 是完全拷贝，可以得到一个全新的 Mat 对象。
 29     // 1.3.2.4、int channels() const;
 30     // 1.3.2.5、int depth() const;
 31     // 1.3.2.6、bool empty() const;
 32     // 1.3.2.7、uchar* ptr(int i0=0);
 33     // 还有很多，就不列举了
 34     // 
 35     // 
 36     //2、Mat 对象使用
 37     // 2.1、部分复制：一般情况下只会复制 Mat 对象的头部和指针部分，数据部分是不会复制的。
 38     //        Mat a=imread(imagefilePath);
 39     //        Mat b(a); 通过拷贝构造就不会数据部分。
 40     // 2.2、完全复制：如果想把 Mat 对象的头部和数据部分一起复制，可以通过 Mat 的 clone() 或者 copyTo() 方法。
 41     // 2.3、使用 Mat 对象的四个要点
 42     //        A、输出图像的内存是自动分配的。
 43     //        B、使用OpenCV的 C++ 接口，不需要考虑内存分配的问题。
 44     //        C、赋值操作和拷贝构造函数只会复制头部和指针部分，数据部分不会复制。
 45     //        D、使用 clone 和 copyTo 两个函数可以实现完全复制。
 46     // 
 47     //3、Mat 定义数组
 48     //创建多维数据 Mat::create
 49     // int sz[3]={2,2,2};
 50     // Mat a(3,sz,CV_8UC1,Scalar::all(0));
 51 
 52 
 53     Mat src;
 54     src = imread("F:\\TestImage\\ZZImage\\psb14.jpg", IMREAD_UNCHANGED);
 55     if (src.empty())
 56     {
 57         cout << "加载图像有错误！！" << endl;
 58         return -1;
 59     }
 60 
 61     namedWindow("DemoWindow", WINDOW_AUTOSIZE);
 62     imshow("DemoWindow", src);
 63 
 64 
 65 
 66     /*Mat dst;
 67     dst = Mat(src.size(),src.type());
 68     dst = Scalar(0,255,0);*/
 69 
 70 
 71     //Mat dst;
 72     //dst = Mat(src.size(), src.type());//此语句可省略
 73     //dst = src.clone();
 74 
 75     /*Mat dst;
 76     src.convertTo(dst,src.type());*/
 77 
 78     /*Mat dst;
 79     src.copyTo(dst);*/
 80 
 81     /*Mat dst;
 82 
 83     cvtColor(src, dst, COLOR_BGR2GRAY);
 84     cout << "原图通道：" << src.channels() << endl;
 85     cout << "目标图通道：" << dst.channels() << endl;
 86 
 87     int height = dst.rows;
 88     int width = dst.cols;
 89     cout << "行数：" << height << endl;
 90     cout << "列数：" << width << endl;
 91 
 92     const uchar* firstRow = dst.ptr(0);
 93     cout << "第一行的值：" << *firstRow << endl;*/
 94 
 95     /*Mat dst(3, 3, CV_8UC1, Scalar(0));
 96 
 97     cout << "dst=" << endl << dst << endl;*/
 98 
 99     //Mat dst;
100     //dst.create(src.size(),src.type());
101     ////通过 create 方法不能直接复制。
102     //dst = Scalar(0,0,255);
103 
104 
105     /*Mat dst = Mat::zeros(src.size(),src.type());*/
106 
107     Mat dst = Mat::eye(2,2,CV_8UC1);
108     cout << "dst=" << endl << dst << endl;
109 
110     namedWindow("DemoWindow2", WINDOW_AUTOSIZE);
111     imshow("DemoWindow2", dst);
112 
113     waitKey(0);
114 
115     return 0;
116 }
```


　　　　内容很简单，就不多说了。


**三、总结**　　　　这是 C\+\+ 使用 OpenCV 的第四篇文章，其实也没那么难，感觉是不是还是很好入门的，那就继续。初见成效，继续努力。皇天不负有心人，不忘初心，继续努力，做自己喜欢做的，开心就好。
