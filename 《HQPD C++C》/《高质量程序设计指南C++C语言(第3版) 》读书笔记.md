# 《高质量程序设计指南C++/C语言(第3版) 》读书笔记

#### 质量属性

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710135001.png)

性能：优化的关键任务是找出限制性能的“瓶颈”

#### SPP

作者基于CMMI 3级的软件过程模型，称为“精简并行过程”（SPP）

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710144541.png)

优点：

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710144958.png)

SPP三层模型

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710145034.png)

测试分类

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710150613.png)

### 程序的基本概念

存在于二进制可执行程序中的只是指令、地址和数据，没有别的东西，这就是**“运行时”**的本质。

像标识符（类型名、变量名、函数名等）、类型定义、const关键字、访问限定符public/private/protected、引用等只是存在于源代码中，它们不会被带入二进制可执行程序中，这是**“编译时”**的本质。

### c++/c程序的基本概念

extern "C"

编译时：预编伪指令、类型定义、外部对象声明、函数原型、标识符、各种修饰符号（const, static等）及类成员的访问说明符（private,,,,）和连接规范、调用规范

运行时：容器越界访问、虚函数动态决议、函数动态链接、动态内存分配、异常处理和RTTI

规范

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710170450.png)

关于void* 和 NULL

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710171810.png)

强制类型转化所导致的内存截断或内存扩张

”换行“和”回车“

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710185439.png)

关于&&和||

![](C:\Users\Administrator\Desktop\ReadingNotes\《HQPD C++C》\Screenshot\QQ截图20200710190508.png)

不要将布尔变量直接与TRUE或者-1、0、1等进行比较

关于以行和列遍历数组的效率受影响主要是**大型数组导致的内存页面交换次数以及cache命中率的高低（Operate System），而不是循环的次数**

第五章