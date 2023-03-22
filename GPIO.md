

# GPIO

stm芯片：是基于ARM设计的Cortex-M4内核，st公司进行设计整体架构，使得内核与各功能部分通过总线矩阵链接。

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/weread_image_250737957074252.jpeg" alt="weread_image_250737957074252" style="zoom: 33%;" />

总线：各种功能部件之间传递信息的公共通信干线，是由导线组成的传输线束。

封装总结：
TO封装 用于晶体管 
SOT封装 贴片晶体管 常见：SOT-23三极管封装
DIP封装 双列直插 方便插拔 易损坏 
SIP封装 单列直插
SOP封装 最常见的贴片封装 方便焊接
QFP封装 用于引脚较多的芯片 缩小体积 焊接困难
TQFP封装 降低芯片的高度，缩小板子的高度
PQFP封装 管脚密集 适用于管脚更多的芯片
TSOP封装 封装更薄 适用于高频
PLCC封装 引脚内收 不易损坏 需要专业设备焊接
BGA封装 引脚在芯片下方 为球形引脚 多用于内存和手机SOC和基带芯片 可以提高存储容量和传输效率 需要借助热风枪等设备进行焊接 拆除再焊接的话需要进行植球
CSP封装 最先进的封装 



驱动单元：

ICode总线：I指instruction，连接内核和Flash（存指令），用于取指令

DCode总线：D指Data，连接Flash和SRAM，存取Flash中的常量和SRAM中的变量、

System总线：访问外部寄存器

DMA总线：传输数据，连接了Flash，SRAM,寄存器，使用总线矩阵仲裁存取顺序

被动单元：

内部的闪存存储器：FLASH,内核通过Icode访问

内部的SRAM：内核通过DCode访问

内部的FSMC：指Flexible static memory controller，用来扩展外部的静态内存，例如SRAM,NORFlash。。。

AHB到APB的桥：AHB是系统总线，APB是外围总线

#### 寄存器：

存储器映射：给存储器分配地址，再分配一次就是存储器的重映射。如下![weread_image_252175759126722](C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/weread_image_252175759126722.jpeg)

Block2 ：片上外设是APB1,APB2,AHB。

则根据各单元功能不同，**以功能为名给各个单元取一个别名就是寄存器，所以寄存器就是外设的一个地址**。这个过程就是寄存器映射。

不同的外设有不同的地址，根据地址找到外设才能使用他。**查看参考手册-存储器和总线架构**



##### GPIO：general purpose I/O ports。是通用输入/输出端口。是stm32可以控制的引脚，可以实现与外部通讯，控制，以及数据采集的功能。实际上是我们通过控制GPIO引脚的电平变化从而达到我们的各种目的。

最小系统：电源，晶振IO，下载IO，BOOT IO，复位IO。

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/weread_image_282519521459915.jpeg" alt="weread_image_282519521459915" style="zoom:33%;" />

内部工作原理：

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/C4EA7EB71E937A99E265C65063F2BD5E.png" alt="img" style="zoom: 50%;" />

输入部分：电平的读入

输入数据寄存器：读取外界电平

复用功能输入

模拟输入：对连续的模拟信号进行连续的读取

ttl肖特基触发器：把连续的信号变成离散的信号，正弦波变矩形波，是间断的

输出部分：电平的输出

两个保护二极管使得电压在一定的区间内部。vdd为最高电压，vss为最低电压，若高于最高电压则沿着二极管的方向导出电流，实现保护电路的作用。**数据手册的电气特性-工作条件-I/O端口特性能找到合理的电压范围**。

两个mos管组成推挽，开漏和关闭三种形态

推挽：连接高电平时，使得vdd直接推出；连接低电平时，相当于把out拉到地上，就是相当于输出低电平。功能比较强。

开漏：输入高电平开关管截止，输出端口上拉和高电压连接；连接低电平的话，同样是接地，间接输出了低电平。能够实现线与。双向通信。

输出数据寄存器

复用功能输出



**点亮LED灯**

看原理图知晓原理：控制GPIO引脚输出一个低电平

###### 新建工程模板

编写代码，勾选arm5和use micro lb选项便于操作

构建按钮：f7

关于堆栈内容，需要自己配置或者使用别人的运行环境管理工具或者从库包中添加

1.在manage run time environment 中选择CMSIS的CORE和device中的setup选项构建环境

2.新建库包放入CMSIS文件，使用魔法棒添加头文件路径。

build aborted是指版本不支持，可以通过修改版本型号来调试

###### 通过寄存器编写GPIO的驱动程序

总线矩阵：包含四个主动单元和四个被动单元。协调内核系统总线和DMA主控总线之间的访问仲裁，采用的是轮换算法，

通过总线的形式把各种外设分离开来，达到独立将各种外设来控制其的使能与否就是控制时钟，节能。

参考手册：GPIO由APB2总线来控制

使能GPIOB 的时钟

查询APB2的外设时钟地址：0x4002 1000 到 0x4002 13FF

外设基地址：0x4001 0c00

CRL偏移：0x00

ODR偏移：0x0c

偏倚地址 0x18

再选择输出方式：配置推挽输出 0

速度：

01：10hz 

11：50hz

10：2hz

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/D68FDB24D067010B08352C9E1CB26D5D.png" alt="D68FDB24D067010B08352C9E1CB26D5D" style="zoom: 25%;" />

配置寄存器地址

### GPIO的8种工作模式详解

##### 输入模式：

浮空输入IN_FLOATING
上拉输入IPU
下拉输入_IPD
模拟输入_AIN

##### 输出模式：

开漏输出_OUT_OD
推挽输出_OUT_PP
开漏复用输出_AF_OD
推挽复用输出AF_PP



###### 推挽输出（push pull）

高电平时是直接让单片机与VDD相接

低电平时是让单片机接地VSS（0v）

让输出控制变为VDD/VSS输出控制，使得输出电流增大，提高了输出引脚的驱动能力，提高了电路的负载能力和开关的动作速度，最常用，能输出较大电流，

###### 开漏输出（open drain）

只连接了VSS（0v）外部接上拉电阻，则输出高电压时断路，输出低电压时通路。

高电平取决于外部上拉的VDD，而不只是3.3v，可以设置其他的，可控而且实现了电平转换。能输出较大电压可以提高芯片的抗干扰能

###### 开漏复用输出_AF_OD/推挽复用输出AF_PP

可选择性的改造，使得这个复用引脚表现为自己想要的作用，但是不能同时发挥两个作用。

###### 上拉输入（input pull up）

外部上拉接着VDD，默认接着高电平，当外界输入时才断开，可以提高芯片的抗干扰能

###### 下拉输入（input pull down）

外部下拉接着VSS，默认接着低电平，可以提高芯片的抗干扰能

###### 浮空输入_IN_FLOATING

没有默认，随着外部的信号改变从而改变

###### 模拟输入AIN

可以读取变化的电平，实现的外界信号的采集，从vss到0

###### 施密特触发器

把模拟信号转化为高低电平

比较器：实时比较电平高低从而决定输入高电平还是低电平，只有一个参考电压。而且电压波动问题可能使得输入不稳，因而加上了一个电阻，构成迟滞比较器也是施密特触发器

有两个参考电压，高于高参考电压则输出低电平，低于低参考电压则输出高电平，处于中间状态时保持上一个状态不变

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/%E5%AD%A6%E4%B9%A0/%7B5()N%7D%5DPS%5D@PD$R71RJ6C.png" alt="img" style="zoom:33%;" />



本质上是一个参考电压，但是由于外界的电压变化超过或者低于某个值时，电路串并联情况会改变，因此导致存在高和低参考电压，可以理解为参考电压自适应的比较器，因为R1和R3的一段连在一起，而另一端同时接VCC，等效就是并联，以此防止输入电平波动导致输出电平频繁跳变。

###### 输出速度

指IO驱动电路的响应速度，并不是信号的输出速度

通常是2mhz，50mhz，10mhz

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/PCQ7F8L3%5BH@2%60I%5D%25U708WD6.png" alt="PCQ7F8L3[H@2`I]%U708WD6" style="zoom: 33%;" />

###### 配置GPIO寄存器

1.先打开时钟先在总线架构查询属于哪个总线，

GPIOB属于APB2总线

找到APB2 外设时钟使能寄存器，并且找到GPIOB 在bit3![img](C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/VPOO3ID46%7BLQJNBWWDXF0B4.png)

偏移地址：0x18     复位值：0x0000 0000   //好像没什么用

复位和时钟控制(RCC) 

**外设基地址：0x4002 1000   地址：0x18 **

![image-20221126004351212](C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/image-20221126004351212.png)

由表可知，通用推挽输出需要ODR寄存器。

2.查询手册，配置推挽或者其他方式功能。通过原理图找到对应的引脚标号。CNF和MODE为一个组。

MODE：是输出速度

00：输入模式(复位后的状态)  

01：输出模式，最大速度10MHz 

10：输出模式，最大速度2MHz  

11：输出模式，最大速度50MHz

CNF：是输出或者输入模式

配置方法

00：通用推挽输出模式 

01：通用开漏输出模式

10：复用功能推挽输出模式 

11：复用功能开漏输出模式

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/1669394203429.png" alt="1669394203429" style="zoom: 50%;" />

1.先对待设置位清零，再设置相应的值

2.先将寄存器的值读出来，修改完成后，再写回去

```c
volatile unsigned int * GPIOB_CLK=(volatile unsigned int *)(0x40021000 + 0x18);
volatile unsigned int * GPIOB_CRL=(volatile unsigned int *)(0x40010c00 + 0x00);
volatile unsigned int * GPIOB_ODR=(volatile unsigned int *)(0x40010c00 + 0x0c);
int main(void)
{
    
  *GPIOB_CLK |= (1<<3);//使能GPIO的外设时钟;
	//GPIOB配置推挽输出;
  *GPIOB_CRL &= (~(0xf<<(4*1)));//清除低四位寄存器，0xf指十进制数15也就是二进制1111
  * GPIOB_CRL |= (2<<(4*1));//写入0010
  *GPIOB_ODR &= (~(0xf<<(4*1)));//清除低四位寄存器
  *GPIOB_ODR |= (0x1<<(1*1));//写入0001
}

```

```c
#define GPIOB_CLK (*(volatile unsigned int *)(0x40021000 + 0x18))
#define GPIOB_CRL (*(volatile unsigned int *)(0x40010c00 + 0x00))
#define GPIOB_ODR (*(volatile unsigned int *)(0x40010c00 + 0x0c))
int main(void)
{
 
  GPIOB_CLK |= (1<<3);//使能GPIO的外设时钟;
	//GPIOB配置推挽输出;
  GPIOB_CRL &= (~(0xf<<(4*1)));//清除低四位寄存器，0xf指十进制数15也就是二进制1111
  GPIOB_CRL |= (2<<(4*1));//写入0010
  GPIOB_ODR &= (~(0xf<<(4*1)));//清除低四位寄存器
  GPIOB_ODR |= (0x1<<(1*1));//写入0001
	
}
```

犯错：地址中加了空格！！！

&位逻辑与

|位逻辑

^位逻辑异或：当位置上数不同时则为真1，相同为假0

~位逻辑反

(<<)右移：可以被移出存储单元，然后用0补齐

(>>)右移

###### 如何实现清除寄存器中原有数据（按位与）

```c
例如：GPIOB_CRL &= ~(3<<(4*0));
```

3用32进制表示：0000 0000 0000 0000 0000 0000 0000 0011

左移四位：0000 0000 0000 0000 0000 0000 0011 0000

取反：1111 1111 1111 1111 1111 1111 1100 1111

寄存器中原有代码：XXXX XXXX XXXX XXXX XXXX XXXX XXXX XXXX 

再进行位逻辑与：XXXX XXXX XXXX XXXX XXXX XXXX XX00 XXXX 

这样实现了对bit4和bit5位的清零

###### 如何实现改写寄存器中原有数据为1（按位或）

```c
例如：GPIOB_CRL |= (3<<(4*0));
```

3用32进制表示：0000 0000 0000 0000 0000 0000 0000 0011

左移四位：0000 0000 0000 0000 0000 0000 0011 0000

寄存器中原有代码：XXXX XXXX XXXX XXXX XXXX XXXX XXXX XXXX 

再进行位逻辑或：XXXX XXXX XXXX XXXX XXXX XXXX XX11 XXXX 

这样实现了对bit4和bit5位的书写为1

![image_看图王](C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/image_%E7%9C%8B%E5%9B%BE%E7%8E%8B.jpg)
