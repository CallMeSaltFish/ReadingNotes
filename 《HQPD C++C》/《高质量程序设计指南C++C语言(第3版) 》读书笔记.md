# 《高质量程序设计指南C++/C语言(第3版) 》读书笔记

#### 质量属性

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710135001.png)

性能：优化的关键任务是找出限制性能的“瓶颈”

#### SPP

作者基于CMMI 3级的软件过程模型，称为“精简并行过程”（SPP）

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710144541.png)

优点：

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710144958.png)

SPP三层模型

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710145034.png)

测试分类

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710150613.png)

### 程序的基本概念

存在于二进制可执行程序中的只是指令、地址和数据，没有别的东西，这就是**“运行时”**的本质。

像标识符（类型名、变量名、函数名等）、类型定义、const关键字、访问限定符public/private/protected、引用等只是存在于源代码中，它们不会被带入二进制可执行程序中，这是**“编译时”**的本质。

### c++/c程序的基本概念

extern "C"

编译时：预编伪指令、类型定义、外部对象声明、函数原型、标识符、各种修饰符号（const, static等）及类成员的访问说明符（private,,,,）和连接规范、调用规范

运行时：容器越界访问、虚函数动态决议、函数动态链接、动态内存分配、异常处理和RTTI

规范

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710170450.png)

关于void* 和 NULL

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710171810.png)

强制类型转化所导致的内存截断或内存扩张

”换行“和”回车“

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710185439.png)

关于&&和||

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200710190508.png)

不要将布尔变量直接与TRUE或者-1、0、1等进行比较

关于以行和列遍历数组的效率受影响主要是**大型数组导致的内存页面交换次数以及cache命中率的高低（Operate System），而不是循环的次数**

### 常量

注意

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711144208.png)

const与#define的比较

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711145430.png)

非静态的const类成员的初始化只能在的类的构造函数的初始化列表中进行

**5.5节，不是很透彻**

### c++/c函数设计基础

函数堆栈

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711160812.png)

函数传值/传址/传引用

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711163231.png)

类的赋值函数，返回引用

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711173208.png)

String的operator + 

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711173756.png)

return语句的效率

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711174521.png)



尽量避免函数带有“记忆”功能。c++/c中，函数的static局部变量是函数的“记忆”存储器



递归和迭代

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200711181909.png)

断言assert

被const修饰的东西都收到c++/c语言实现的**静态类型安全检查机制**的保护

### ※c++/c指针、数组和字符串

#### 读写周期

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200713193021.png)

指针的危险性:如果访问了非法的或无效的内存单元，就会导致运行时错误

注意：![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200713193851.png)

字面常量保存在符号表

数组和指针的等价关系：

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200713200012.png)

#### 字符数组、字符指针和字符串

#### 引用和指针

引用的创建和销毁不会调用构造和析构函数



![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200714203444.png)



### C++/C高级数据类型

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200714204742.png)

#### 字节对齐

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200714212329.png)

数据成员从大到小排列，只会在对象的末尾追加填充字节

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200714214014.png)

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200714214516.png)

#### 联合

联合的内存大小取决于其中字节数最多的成员、而不是累加

### C++/C编译预处理

#### 头文件包含顺序

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200721152702.png)

### C++/C文件结构和程序版式

### C++/C应用程序命名规则

### C++面向对象程序设计方法概述

**所谓虚函数表（vtable），就是函数指针数组**

协变（override返回参数不同）

c++支持运行时多态特性的手段有两种，这里讲的**虚函数机制**是其中主要的一种，另一种是**RTT1**

**如果确实需要使用*多态数组*，请使用STL容器配合普通指针或智能指针**

#### ※C++对象模型

##### 基本C++对象模型

![](C:\Users\ranqinyuan.than\Desktop\Intership\internshipDairy\PictureQuote\QQ截图20200727191909.png)

![](C:\Users\ranqinyuan.than\Desktop\Intership\internshipDairy\PictureQuote\QQ截图20200727192647.png)

##### 增加了继承和虚函数的类的对象模型

![](C:\Users\ranqinyuan.than\Desktop\Intership\internshipDairy\PictureQuote\QQ截图20200727192725.png)

![](C:\Users\ranqinyuan.than\Desktop\Intership\internshipDairy\PictureQuote\QQ截图20200727192741.png)

![](C:\Users\ranqinyuan.than\Desktop\Intership\internshipDairy\PictureQuote\QQ截图20200727192819.png)

隐含成员

![](C:\Users\ranqinyuan.than\Desktop\Intership\internshipDairy\PictureQuote\QQ截图20200727200138.png)

### 对象的初始化、拷贝和析构

拷贝构造函数第一个参数要是引用而不能是对象值？

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200729170810.png)

#### 派生类的基本函数注意点：

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200801162441.png)

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200801162542.png)

### C++函数的高级特性

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200801163756.png)

#### 类型转换函数

本质：

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200808145600.png)

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200807191535.png)

#### Const成员函数

访问规则

![](C:\Users\ranqinyuan.than\Desktop\Intership\《HQPD C++C》\Screenshot\QQ截图20200807193018.png)

### 15章跳过

### 内存管理

16.15