本文主要介绍[Ubuntu](https://so.csdn.net/so/search?q=Ubuntu&spm=1001.2101.3001.7020)系统下GCC生成静态库和动态库和两者之间的链接、GCC的常用命令以及GCC编译器的主要工作原理、OpenCV的安装以及简单应用、掌握GitHub的使用方法，上传自己的代码。

**目录**

[一、GCC生成静态库和动态库的应用](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t0)

[1、用GCC生成静态库和动态库](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t1)

[（1）编译生成例子程序hello.c、hello.h、main.c。](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t2)

[（2）第 2 步：将 hello.c 编译成.o 文件](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t3)

[（3）第 3 步：由.o 文件创建静态](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t4)

[（4）第 4 步：在程序中使用静态库](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t5)

[（5）第 5 步：由.o 文件创建动态库文件](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t6)

[（6）第 6 步：在程序中使用动态库](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t7)

[（7）第7部：比较静态库和动态库的使用优先级](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t8)

[2、静态库与动态库的使用](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t9)

[（1）创建新文件并编辑文件](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t10)

[（2）生成静态库并执行文件](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t11)

 [（3）生成动态库文件并使用](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t12)

 [（4）编写程序并生成动态库和静态库，运行程序](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t13)

[（5）生成目标文件后生成静态库并执行文件](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t14)

 [（6）生成动态库并执行文件](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t15)

[二、Linux GCC下常用命令](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t16)

[1、编译指令](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t17)

[2、链接](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t18)

[3、分析生成的文件格式](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t19)

 [三、OpenCV的安装与使用](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t20)

[1、安装准备](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t21)

[2、下载并安装OpenCV](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t22)

[3、OpenCV下的图像处理技术](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t23)

[4、OpenCV下进行视频播放](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t24)

[5、opencv下进行录制视频](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t25)

[四、实验总结](https://blog.csdn.net/Xicun1984/article/details/126865397?spm=1001.2014.3001.5502#t26)

___

## 一、[GCC](https://so.csdn.net/so/search?q=GCC&spm=1001.2101.3001.7020)生成静态库和动态库的应用

## 1、用GCC生成静态库和动态库

### （1）编译生成例子程序hello.c、hello.h、main.c。

在Ubuntu系统下创建一个新的文件夹：test1，进入创建的文件夹，将本次实验的代码存入其中。

![](https://img-blog.csdnimg.cn/04cb8e050e7e4faea2b61cbabc33209b.png)

在当前路径下用vim文本编辑器编辑所需要的三个子程序：

```
程序 1: hello.h#ifndef HELLO_H#define HELLO_Hvoid hello(const char *name);#endif //HELLO_H程序 2: hello.c#include <stdio.h>void hello(const char *name){printf("Hello %s!\n", name);}程序 3: main.c#include "hello.h"int main(){hello("everyone");return 0;}
```

 编译完成并保存，运行ls命令查看是否创建成功：

![](https://img-blog.csdnimg.cn/67a352add9024ab2af2835ef303eb770.png)

### （2）第 2 步：将 hello.c 编译成.o 文件

无论静态库，还是动态库，都是有.o文件创建的。因此，我们必须将源程序hello.c通过GCC编译成.o文件。

输入命令：

```
gcc -c hello.c
```

 ![](https://img-blog.csdnimg.cn/0c54b93ab9f544f4b2b2a852649c1494.png)

 在ls的命令下，我们看到了hello.o文件，本部操作完成。

### （3）第 3 步：由.o 文件创建静态

静态库文件名的命名规范是以 lib 为前缀，紧接着跟静态库名，扩展名为.a。例如：我们将创建的静态库名为 myhello，则静态库文件名就是 libmyhello.a。创建静态库使用ar命令，输入以下命令创建静态库文件libmyhello.a。

```
ar -crv libmyhello.a hello.o
```

创建成功之后，同样输入ls命令查看：

![](https://img-blog.csdnimg.cn/c164111a49c84fe5b0ef7e2d32e3c00a.png)

### （4）第 4 步：在程序中使用静态库

使用静态库内部的函数：只需要在使用到这些公用函数的源程序中包含这些公用函数的原型声明，然后在用 gcc 命令生成目标文件时指明静态库名，gcc 将会从静态库中将公用函数连接到目标文件中。注意，gcc 会在静态库名前加上前缀 lib，然后追加扩展名.a 得到的静态库文件名来查找静态库文件。

先通过main.c文件生成main.o文件：

```
gcc -c main.c
```

再使用静态库生成可执行文件：

```
gcc -o hello main.o libmyhello.a
```

也可以通过一句代码完成静态库的使用，其结果也是一样的：

```
gcc -o hello main.c -L. –lmyhello
```

生成可执行文件之后就可以运行得到结果，具体操作结果如下：

![](https://img-blog.csdnimg.cn/da9b9309946f4608804800c2f2aa2cac.png)

 我们再尝试删除静态库文件试试公用函数 hello 是否真的连接到目标文件 hello 中

![](https://img-blog.csdnimg.cn/39ab946919d24137a020a85c8e8b05e2.png)

 结果显示同样可行，说明静态库中的公用文件已经连接到目标文件中。

### （5）第 5 步：由.o 文件创建动态库文件

动态库文件名命名规范和静态库文件名命名规范类似，也是在动态库名增加前缀 lib，但其文件扩展名为.so。例如：我们将创建的动态库名为 myhello，则动态库文件名就是 libmyhello.so。

输入以下命令创建动态库文件：

```
gcc -shared -fPIC -o libmyhello.so hello.o
```

查看，确定创建成功：

![](https://img-blog.csdnimg.cn/b4112316ecac41c2b44b006101ba600b.png)

### （6）第 6 步：在程序中使用动态库

在程序中使用动态库和使用静态库完全一样，也是在使用到这些公用函数的源程序中包含这些公用函数的原型声明，然后在用 gcc 命令生成目标文件时指明动态库名进行编译。我们先运行 gcc 命令生成目标文件，再运行它看看结果。

```
gcc -o hello main.c -L. -lmyhello
```

 ![](https://img-blog.csdnimg.cn/55292433c458438b9d1361187153546e.png)

可以看到，本次运行结果出现了错误，原来是找不到动态库文件 libmyhello.so。程序在运行时，会在/usr/lib 和/lib 等目录中查找需要的动态库文件。若找到，则载入动态库，否则将提示类似上述错误而终止程序运行。我们将文件 libmyhello.so 复制到目录/usr/lib 中，再试一次。

在超级用户模式下输入命令：

```
mv libmyhello.so /usr/lib
```

再次运行可执行文件，得到以下结果：

![](https://img-blog.csdnimg.cn/6e8e42163928497eafda8c50a28bd860.png)

### （7）第7部：比较静态库和动态库的使用优先级

我们回过头看看，发现使用静态库和使用动态库编译成目标程序使用的 gcc 命令完全一样， 那当静态库和动态库同名时，gcc 命令会使用哪个库文件呢？

先删除除.c 和.h 外的所有文件，恢复成我们刚刚编辑完举例程序状态。

```
rm -f hello hello.o main.o /usr/lib/libmyhello.so
```

![](https://img-blog.csdnimg.cn/838798031c2641f4ae6406006a2558c2.png)

 注：删除 libmyhello.so 文件时，同样要切换到超级用户模式下操作。

恢复到刚刚编辑举例程序状态时，再来创建静态库文件 libmyhello.a 和动态库文件 libmyhello.so：

```
gcc -c hello.car -crv libmyhello.a hello.ogcc -shared -fPIC -o libmyhello.so hello.o
```

逐条输入创建成功之后，输入 ls 命令查看：

![](https://img-blog.csdnimg.cn/d69290ca0998413f981cb590c554ccce.png)

 然后，我们运行gcc命令来使用函数库myhello生成目标文件 hello，并运行程序 hello。

```
gcc -o hello main.c -L. -lmyhello
```

![](https://img-blog.csdnimg.cn/f31ff40ff48841dbb7e00f91b920562a.png)

从程序 hello 运行的结果中很容易知道，当静态库和动态库同名时，gcc 命令将优先使用动态库，默认去连/usr/lib 和/lib 等目录中的动态库，只需将文件 libmyhello.so 复制到目录/usr/lib 中即可。

## 2、静态库与动态库的使用

### （1）创建新文件并编辑文件

![](https://img-blog.csdnimg.cn/63c348c914684e44a09b1875db06d4d5.png)

```
#include<stdio.h>void print1(int arg){printf("1 print arg:%d\n",arg);}
```

```
#include<stdio.h>void print2(char *arg){printf("2 print arg:%s\n",arg);}
```

```
#ifndef _3_H_#define _3_H_#include<stdio.h>void print1(int);void print2(char *);#endif
```

```
#include<stdio.h>#include"3.h"int main(){print1(1);print2("test");return 0;}
```

### （2）生成静态库并执行文件

![](https://img-blog.csdnimg.cn/e0f354396c32451384678302e1364736.png)

![](https://img-blog.csdnimg.cn/bc5db2ec2ab64b9c8eb85dc153835315.png)

###  （3）生成动态库文件并使用

![](https://img-blog.csdnimg.cn/c902e67ef97b42549518e0096d15ea4e.png)

![](https://img-blog.csdnimg.cn/12b48b89dc7247bebed372188c8cba01.png)

###  （4）编写程序并生成动态库和静态库，运行程序

![](https://img-blog.csdnimg.cn/d4900e0163c74b7d81e4c1892f32c788.png)

```
#include<stdio.h>#include"1.h"int main(){int x=4,y=2;float t=x2x(x,y);float s=x2y(x,y);printf("%f\n",t);printf("%f\n",s);}
```

```
#include<stdio.h>float x2x(int x,int y){float n=(float)x/y;return n;}
```

```
#include<stdio.h>float x2y(int a,int b){float z=a+b;return z;}
```

```
#ifndef _1_H_#define _1_H_#include<stdio.h>float x2x(int x,int y);float x2y(int x,int y);#endif
```

### （5）生成目标文件后生成静态库并执行文件

![](https://img-blog.csdnimg.cn/91f6f60fadfa402a9db8722b3468aa36.png)

###  （6）生成动态库并执行文件

![](https://img-blog.csdnimg.cn/ff1f40b4e6704f61ad071bb088b53e4a.png)

## 二、Linux GCC下常用命令

## 1、编译指令

一步到位的编译指令是：gcc test.c -o test  
1）预处理  
gcc -E test.c -o test.i 或 gcc -E test.c  
2）编译  
gcc -S test.i -o test.s  
3）汇编  
gcc -c test.s -o test.o  
4）连接  
gcc test.o -o test

##   
2、链接

① 静态链接是指在编译阶段直接把静态库加入到可执行文件中去，这样可执行文件会比较大。链接器将函数的代码从其所在地（不同的目标文件或静态链接库中）拷贝到最终的可执行程序中。为创建可执行文件，链接器必须要完成的主要任务是：符号解析（把目标文件中符号的定义和引用联系起来）和重定位（把符号定义和内存地址对应起来然后修改所有对符号的引用）。  
② 动态链接则是指链接阶段仅仅只加入一些描述信息，而程序执行时再从系统中把相应动态库加载到内存中去。  
在 Linux 系统中，gcc 编译链接时的动态库搜索路径的顺序通常为：首先从 gcc命令的参数-L 指定的路径寻找；再从环境变量 LIBRARY\_PATH 指定的路径寻址；再从默认路径/lib、/usr/lib、/usr/local/lib 寻找 。  
在 Linux 系统中，执行二进制文件时的动态库搜索路径的顺序通常为：首先搜索编译目标代码时指定的动态库搜索路径；再从环境变量LD\_LIBRARY\_PATH指定的路径寻址；再从配置文件/etc/ld.so.conf中指定的动态库搜索路径；再从默认路径/lib  
和/usr/lib寻找 。  
在 Linux 系统中，可以用ldd命令查看一个可执行程序依赖的共享库。

```
gcc Hello.c -o Hello size Hello ldd Hellogcc -static Hello.c -o Hello size Hello ldd Hello链接器链接后生成的最终文件为 ELF 格式可执行文件一个 ELF 可执行文件通常被链接为不同的段，常见的段譬如.text、.data、.rodata、.bss 等段.
```

![](https://img-blog.csdnimg.cn/7c26cd86925340468311ae19663d1db1.png)

## 3、分析生成的文件格式

输入命令：

```
readelf -S hello
```

![](https://img-blog.csdnimg.cn/ce991ce5a08a4912964783b52eedb0c2.png)

反汇编ELF，使用相关指令将其反汇编，输入以下代码：

```
objdump -D hello
```

![](https://img-blog.csdnimg.cn/010a65f954db4e63bf578320c13b282d.png)

##  三、[OpenCV](https://so.csdn.net/so/search?q=OpenCV&spm=1001.2101.3001.7020)的安装与使用

## 1、安装准备

安装cmake:

```
sudo apt-get install cmake
```

依赖环境：

```
sudo apt-get install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-devsudo apt-get install libgtk2.0-devsudo apt-get install pkg-config
```

![](https://img-blog.csdnimg.cn/544fedc3ecfc40d9902aa4c210f77471.png)

## 2、下载并安装OpenCV

下载地址：[Releases - OpenCV](https://opencv.org/releases/ "Releases - OpenCV")  可以直接用虚拟机自带的Firefox浏览器打开  
点击Sources进行下载自己需要的版本

![](https://img-blog.csdnimg.cn/f094a6661de247b79c1b854de9de67ff.png)

下载完成之后，打开文件所在文件夹，解压到当前文件夹并在该文件夹下新建build文件夹

![](https://img-blog.csdnimg.cn/4048f223c59a42fe91d45822108b3537.png)

输入命令：

```
sudo cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
```

![](https://img-blog.csdnimg.cn/42f64b4da3a14131a7fd8992a569a955.png)

进行编译，这一步花费的时间较多，慢慢等待就好，耐心点......

输入以下代码：

```
sudo make -j 8
```

![](https://img-blog.csdnimg.cn/c138688ec15f4e63a4940a4a137ddc9f.png)

接下来就可以进行安装了，输入以下代码：

```
sudo make install
```

![](https://img-blog.csdnimg.cn/005f8a3e0b544e90b69b65c0edfef1d7.png)

 安装完成之后就可以配制环境了

用gedit打开/etc/ld.so.conf  
在文件中加上一行 /usr/loacal/lib  
其中/user/loacal是opencv安装路径也就是makefile中指定的安装路径

输入命令：

```
sudo gedit /etc/ld.so.conf
```

![](https://img-blog.csdnimg.cn/302df0f4f85044b38904dfde985e8a6e.png)

 修改bash.bashrc文件

输入命令：

```
sudo gedit /etc/bash.bashrc 
```

 进入文件之后，在文件末尾添加以下代码：

```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfigexport PKG_CONFIG_PATH
```

然后在命令行输入代码：

```
source /etc/bash.bashrc
```

检验OpenCV是否安装完成，输入代码：

```
pkg-config opencv --modversion
```

![](https://img-blog.csdnimg.cn/b31f05b09eea4749bcd8b8f41eb36db5.png)

 结果显示安装成功！！

## 3、OpenCV下的图像处理技术

创建目录创建文本文件代码如下  
在编译代码时要在同一个目录下要保存一张图片为lena.jpg格式

代码逐条如下：

```
mkdir ecd etouch codegedit code.cppg++ code.cpp -o test1 `pkg-config --cflags --libs opencv`./test1ls
```

 code.cpp.代码如下：

```
#include <opencv2/highgui.hpp>#include <opencv2/opencv.hpp>using namespace cv;using namespace std;int main(int argc, char** argv){CvPoint center;double scale = -3; IplImage* image = cvLoadImage("lena.jpg");argc == 2? cvLoadImage(argv[1]) : 0;cvShowImage("Image", image);if (!image) return -1; center = cvPoint(image->width / 2, image->height / 2);for (int i = 0;i<image->height;i++)for (int j = 0;j<image->width;j++) {double dx = (double)(j - center.x) / center.x;double dy = (double)(i - center.y) / center.y;double weight = exp((dx*dx + dy*dy)*scale);uchar* ptr = &CV_IMAGE_ELEM(image, uchar, i, j * 3);ptr[0] = cvRound(ptr[0] * weight);ptr[1] = cvRound(ptr[1] * weight);ptr[2] = cvRound(ptr[2] * weight);}Mat src;Mat dst;src = cvarrToMat(image);cv::imwrite("test.png", src);cvNamedWindow("test",1);  imshow("test", src);cvWaitKey();return 0;}
```

运行结果如下:

![](https://img-blog.csdnimg.cn/0f83110a6e4449e1a5bc19415666150f.png)

## 4、OpenCV下进行视频播放

创建新的.c文件test2.cpp

```
#include <opencv2/opencv.hpp>using namespace cv;int main(){VideoCapture capture("man.mp4");while(1){Mat frame;capture >> frame;if(frame.empty())break;imshow("读取视频帧",frame);waitKey(30);}system("pause");return 0;}
```

将准备好的视频文件同样放在这个路径之下，运行以下代码：

```
g++ test2.cpp -o test2 `pkg-config --cflags --libs opencv`
```

运行可执行文件。

## 5、opencv下进行录制视频

创建test3.cpp文件

```
vim test3.cpp
```

源码如下：

```
#include<iostream>#include <opencv2/opencv.hpp>#include<opencv2/core/core.hpp>#include<opencv2/highgui/highgui.hpp>using namespace cv;using namespace std;int main(){VideoCapture cap(0);if (!cap.isOpened()){cout << "error" << endl;waitKey(0);return 0;}int w = static_cast<int>(cap.get(CV_CAP_PROP_FRAME_WIDTH));int h = static_cast<int>(cap.get(CV_CAP_PROP_FRAME_HEIGHT));Size videoSize(w, h);VideoWriter writer("RecordVideo.avi", CV_FOURCC('M', 'J', 'P', 'G'), 25, videoSize);Mat frame;int key;char startOrStop = 1;char flag = 0;while (1){cap >> frame;key = waitKey(100);if (key == 32){startOrStop = 1 - startOrStop;if (startOrStop == 0){flag = 1;}}if (key == 27){break;}if (startOrStop == 0 && flag==1){writer << frame;cout << "recording" << endl;}else if (startOrStop == 1){flag = 0;cout << "end recording" << endl;}imshow("picture", frame);}cap.release();writer.release();destroyAllWindows();return 0;}
```

编译test3.cpp文件：

```
g++ test3.cpp -o test3 `pkg-config --cflags --libs opencv`
```

运行可执行文件，结果如下：

![](https://img-blog.csdnimg.cn/e323bc8b2a7d4c9d8c8ff80fee402957.png)

 ![](https://img-blog.csdnimg.cn/ed5546e331b34b76a79d07b3e455f348.png)

## 四、实验总结

前面的静态库和动态库学习在老师发的PDF帮助下，还是很容易完成的，不过在OpenCV的安装过程中，发生了很多错误，在查询了网上的资料之后，最终还是将OpenCV安装成功了。后面跟着的图像处理和视频录制就可以按部就班的完成了，总之，本次实验课我的收获很大，不过后面还有很长的路要走，也希望有更大的进步。