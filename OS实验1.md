 

**操作系统课程设计实验报告**

 

 

 

<center>实验题目：  实验1 Linux内核编译及添加系统调用        






<center>姓   名：               

<center>学   号：              


<center>组  号：                 
<center>专   业：              

<center>班   级：             

<center>老师姓名：               






<center>日   期：     







<center>目   录


[TOC]

# 一 题目介绍

​	本实验通过修改Linux内核源码，添加新的Linux系统调用，替换编译后内核，并测试结果，了解Linux内核源码的编译方法和内核的安装方法，系统调用的概念、编写步骤和调用方法。

# 二 实验思路

![image-20240428231317130](D:\Markdown txt\OS实验1.assets\image-20240428231317130.png)

# 三 遇到问题及解决方法

1.缺少openssll  Fatal error: openssl/opensslv.h: No such file or directory

解决方法：sudo apt install libssl-dev

2.缺少bison

解决方法：sudo apt intall bison

3.缺少flex

解决方法：sudo apt install flex

# 四 核心代码及实验结果展示

1.使用`uname -r`检查当前版本的内核

**![img](D:\Markdown txt\assets\clip_image002.gif)**

<center>图表 1Linux内核-旧

使用`wget https://kernel.org/pub/linux/kernel/v6.x/linux-6.6.28.tar.xz`

`tar -xvf linux-6.6.28`解压

`cd linux-6.6.28`进入内核文件夹

`make clean`

`make menuconfig`

`make -j8`

`make modules_install`

`make install`

重启即可

![img](D:\Markdown txt\assets\clip_image004.gif)



<center>图表 2Linux内核-新
添加系统调用：

2.1分配系统调用号，修改系统调用表

查看系统调用表(/usr/src/linux-6.6.28/arch/x86/entry/syscalls/syscall_64.tbl)

![img](D:\Markdown txt\assets\clip_image006.gif)

<center>图表 3添加系统调用1
2.2申明系统调用服务例程原型

原型申明在文件 (./include/linux/syscalls.h) 中

![img](D:\Markdown txt\assets\clip_image008.gif)

<center>图表 4添加系统调用2
2.3实现系统调用服务

sys.c文件在(/usr/src/linux-6.6.28/kernel/sys.c)中

![img](D:\Markdown txt\assets\clip_image010.gif)

<center>图表 5添加系统调用3
2.4重新编译内核，方法同上

2.5编写测试代码，调用添加的系统调用

![img](D:\Markdown txt\assets\clip_image012.jpg)

<center>图表 6编写程序调用系统调用
2.6使用sudo dmesg命令，查看输出

![img](D:\Markdown txt\assets\clip_image014.gif)

<center>图表 7系统调用输出学号

3.修改或返回指定进程的优先级（nice值和prio值）
3.1分配系统调用号，修改系统调用表

![image-20240427001149579](D:\Markdown txt\OS实验1.assets\image-20240427001149579.png)

3.2申明系统调用服务例程原型

![image-20240427001336108](D:\Markdown txt\OS实验1.assets\image-20240427001336108.png)

3.3实现系统调用服务

![image-20240427001600393](D:\Markdown txt\OS实验1.assets\image-20240427001600393.png)

3.4编写测试代码，实现调用

![image-20240427001706658](D:\Markdown txt\OS实验1.assets\image-20240427001706658.png)

3.5测试截图

![image-20240428184332213](D:\Markdown txt\OS实验1.assets\image-20240428184332213.png)

4.1分配系统调用号，修改系统调用表（如3.1图所示）

4.2申明系统调用服务例程原型

![image-20240428225034029](D:\Markdown txt\OS实验1.assets\image-20240428225034029.png)

4.3实现系统调用服务

![image-20240428225154851](D:\Markdown txt\OS实验1.assets\image-20240428225154851.png)

4.5测试截图

![image-20240428225225441](D:\Markdown txt\OS实验1.assets\image-20240428225225441.png)



# 五 个人实验改进与总结

## 5.1 个人实验改进

1.	提高编译效率：在编译Linux内核时，可以通过使用多线程编译来提高编译效率。例如，使用make -j4命令可以利用4个CPU核心进行编译，从而加快编译速度。
2.	优化系统调用的实现：在添加系统调用时，可以考虑优化系统调用的实现。例如，可以通过深入阅读相关函数源码来理解和优化系统调用的功能，以及如何更有效地使用内核函数。
3.	增强错误处理：在编译过程中，可能会遇到一些错误，这些错误可能是由于缺少某个库或其他原因导致的。通过优化错误处理机制，可以更快地识别和解决这些问题，从而提高编译成功率。
4.	使用最新的内核版本：为了避免遇到不必要的兼容性问题，可以使用最新的内核版本进行编译。这样可以确保编译过程中使用的是最新的功能和修复，从而提高编译的稳定性和成功率。
5.	测试系统调用的兼容性：在添加系统调用后，应该对其进行充分的测试，以确保其在不同的硬件和操作系统环境下都能正常工作。这包括测试系统调用的功能正确性，以及对各种边界条件和错误情况的处理能力。

## 5.2 个人实验总结

在完成Linux内核编译和添加系统调用后，我有以下几点感受：

1. 深入理解Linux内核：通过编译Linux内核，我对Linux内核有了更深入的理解。我了解到内核的构建过程涉及到多个步骤，包括下载源代码、配置、编译、安装和更新引导加载器。这个过程让我对Linux内核的组织和运行机制有了更清晰的认识。

2. 系统调用的实现：添加一个系统调用，让我对Linux系统调用的工作原理有了更深入的理解。我了解到系统调用是用户空间与内核空间交互的一种方式，通过系统调用，用户空间的程序可以请求内核提供服务。我还学习了如何分配系统调用号，修改系统调用表，以及实现系统调用服务例程。这个过程让我对系统调用的实现有了更深入的理解。

3. 编程和系统级编程的区别：在编写用户态程序测试系统调用时，我体验到了编程和系统级编程的区别。系统级编程需要更深入地理解硬件和操作系统的工作原理，而且需要处理更多的边界条件和错误情况。这个过程让我对编程的复杂性有了更深的认识。

4. 实践的重要性：通过实际操作，我深刻体验到了实践的重要性。理论知识虽然重要，但是只有通过实践，才能真正理解和掌握知识。这个过程让我更加坚信实践的重要性。

5. 挑战和成就感：编译Linux内核和添加系统调用是一个挑战，但也是一个成就感的过程。我通过这个过程，不仅学到了很多知识，也提升了自己的技术能力和解决问题的能力。

   总的来说，完成Linux内核编译和添加系统调用后，我对Linux内核和系统调用有了更深入的理解，也提升了自己的技术能力和解决问题的能力。这个过程让我体验到了实践的重要性，也让我对编程有了更深的认识。

# 六 参考文献

* [菜鸟教程](https://www.runoob.com/)

* [OS 实验一 | Linux内核编译及添加系统调用](https://zhuanlan.zhihu.com/p/31342840)

* [给 Linux 内核添加自己定义的系统调用](https://zhuanlan.zhihu.com/p/487648323)

* [Ubuntu内核编译完成后重启无法进入系统解决方法](https://blog.51cto.com/u_15352922/3743865)

* [《杭州电子科技大学操作系统实验一：linux 内核编译及添加系统调用》](https://zhuanlan.zhihu.com/p/363014797)

 