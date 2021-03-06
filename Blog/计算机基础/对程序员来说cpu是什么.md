## 对程序员来说CPU是什么

> 这是《程序是怎么样跑起来的》阅读笔记，这也只是阅读笔记。Hhhhhh

### CPU 内部结构解析

`CPU（Central Processing Unit）`：中央处理器，负责解释和运行最终转换为机器语言的程序内容

`CPU `是许多晶体管组成的电子部件，通常叫做`IC（Integrated Circuit）`集成电路

**`CPU `的组成：**
	
* 寄存器：暂存指令、数据等处理对象，可以将其看成内存的一种
* 控制器：负责把内存中的指令、数据等读入寄存器，并根据指令的结果来控制整个计算机
* 运算器：负责运算从内存读入寄存器的数据
* 时钟：发出` CPU` 开始计时的信号，时钟的频率越高，`CPU`的运行效率越高。有的计算机时钟位于 `CPU ` 外

**内存：**

* 主存储器，主存
* 通过控制芯片与`CPU`相连，主要负责存储指令和数据
* 主存中的数据和指令会在计算机关机时清除

**那么程序的运行机制大致可以这么描述：**

程序启动后，根据时钟信号，控制器从内存中读取数据和指令，通过对这些指令加以解释和运行，运算器会对数据进行运算，控制器根据运算结果控制计算机

### CPU中的寄存器

我们知道不管是汇编这样的低级语言，还是 `java `这样的高级语言，都要转换为机器语言，机器语言级别的程序是通过寄存器来处理的

内存的存储场所通过地址编号来区分，而寄存器的种类则通过名字来区分

不同类型的`CPU`，内部寄存器的数量、种类以及寄存器存储的数值范围都是不同的。不过根据功能的不同，大致可以分为八类

![](http://i2.buimg.com/73023d9c4182551a.jpg)

图中的**基址寄存器**、**变址寄存器**、**通用寄存器**一般都在`CPU`中存在多个，但是其他五个一般都是只有一个寄存器

程序寄存器和标志寄存器比较特殊


### 决定程序流程的程序寄存器

当程序开始启动后，程序会从磁盘中复制到内存中，那么机器语言怎么知道各个地址存储的内容呢？又从那里读取数命令来执行？

地址`0100`是程序运行的起始位置，当程序开始执行时，程序计数器会设定为`0100`。`CPU`每执行一个指令，程序计数器都会增加与指令长度相对应的数值，然后，`CPU`控制器就会参照程序计数器的数值，从内存中读取数据并执行。程序计数器决定着程序的流程。

**示例程序：怎么实现将`123`与`456`相加，并将结果显示出来**

![](http://i4.buimg.com/49325015c654276e.jpg)

### 条件分支和循环机制

程序流程分为顺序执行、条件分支以及循环三种

以条件分支为例：

![](http://7xrn7f.com1.z0.glb.clouddn.com/16-5-31/79292411.jpg)

条件分支和循环中使用的跳转指令，会参照标志寄存器中保存的结果来进行判断。对于上述问题，则是判断当前累加寄存器的数值大小，不管是正数、负数还是零，都会存在标志寄存器中。

怎么存放这三个结果呢？这三个状态是由标志寄存器的三个位来表示的

![](http://7xrn7f.com1.z0.glb.clouddn.com/16-5-31/22753404.jpg)

### 函数调用机制

函数调用机制与单纯的跳转指令有所不同，单纯的跳转指令无法实现函数调用。函数调用需要在完成函数内部的处理后，处理流程再返回到函数调用点（函数调用指令的下一个地址）。因此，如果只是跳转到函数的入口地址，处理流程就不知道该返回到那里去。

那么机器语言，有特定指令来处理这个问题。`call`指令和`return`指令，函数调用使用`call`指令，在将函数入口地址设置到程序计数器之前，`call`指令会把调用函数后要执行的指令地址（函数调用指令的下一个地址）存放到名为栈的内存中。函数处理完毕之后，再通过函数的出口来执行`return`指令，`return`指令就是把栈中的地址设置到程序计数器，这样就可以流畅的执行。

![](http://7xrn7f.com1.z0.glb.clouddn.com/16-5-31/36805430.jpg)

### 基址寄存器与变址寄存器

通过这两个寄存器可以对主存上特定的内存区域进行划分，达到类似于数组的效果

![](http://7xrn7f.com1.z0.glb.clouddn.com/16-5-31/23770787.jpg)


