STM32

c/c++固件库配置宏定义

~~~c
STM32F10X_HD,USE_STDPERIPH_DRIVER
~~~

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/MEGD9SW$GWF3C6A8Q%60Z%5D2H7.png" style="zoom: 80%;" />

配置设置之后可以在全局查找宏定义和标识符和函数



<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/UE46_B%7DC78BWNB%7DOY1N%25PJ.png" style="zoom:50%;" />

配置时注意波特率，左下角的电位调节，先编译后下载的选项

波特率：串口传输的波特率即为每秒钟传输二进制的位数。

内核中断

可屏蔽中断

外部中断

中断优先级分组：寄存器SCB—>AIRCR中进行配置

抢占优先级：优先级高的中断可以抢占正在进行的低级中断，1>2

响应优先级：抢占优先级相同的中断，高响应能打断低响应,1>2

都相等时按照先后顺序

一般只是设置一次中断优先级的分组

```c
void NVIC_PriorityGroupConfig (uint32_tNVIC_PriorityGroup)//设置优先级分组
    void NVIC_Init(NVIC_InitTypeDef*NVIC_InitStruct)//设置中断优先级和响应级
    NVIC_IRQChannelCmd （）//配置中断使能寄存器
    NVIC_INLINE void NVIC_SetPendingRQ()//配置中断失能寄存器
    
```

<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/@%7B0C%25AU91%7D%258B%5B%7B4%7D4M%5DZ7.png" alt="~@{0C%AU91}%8B[{4}4M]Z7" style="zoom:50%;" />

类比配置GPIO

串口通讯：

[<img src="C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/3IBPXQ@FUP%60@L6I%5D806F7G.png" style="zoom:50%;" />]()

串口异步通讯：
1.起始位

2.数据位（8位）

3.奇偶校验位（第九位）

4.停止位（1，15，2位）

5.波特率设置

接受移位寄存器->接受数据寄存器

发送数据寄存器->发送移位寄存器

USART—SR状态寄存器

USART—DR数据寄存器

USART—BRR波特率寄存器

USART_CR寄存器：发送和收发使能，以及中断使能

波特率=fPCLKx/（16*USARTDIV）

串口操作常用库函数：

```c
void USART_Init()//串口初始化，以及相关使能
void USART_Cmd()//串口使能    
void USART_ITConfig()//使能相关中断    
void USART_SendData()//发送数据到串口
uint_tUSART_ReceiveData()    //接受数据
FlagStatus USART_GetFlagStatus()   //获取状态标志位 
void USART_ClearFlag()    //清除状态标志位
ITStatus USART_GetITSatus()    //获取中断状态标志位
void USART_ClearITPendingBit()    //清除中断状态标志位
    
    
```

#### **配置流程**

![](C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/Y$XE68%7BI%7BZ0YQ_YB5NN@TP.png)
