title: I2C总线
date: 2015-05-14 22:36:37
categories:
- 凊筠什么的最厌学了
- 单片机
tags: STM32
---

#简介#
I²C（Inter-Integrated Circuit）是内部集成电路的称呼，是一种**串列通信总线**，使用多主从架构，由飞利浦公司在1980年代为了让主板、嵌入式系统或手机用以连接低速周边设备而发展。

#协议#
1. 使用两条串行（数据线SDA&时钟线SCL），并利用电阻将电位上拉；
2. 可在CPU与被控IC之间，IC与IC之前都可以进行双向传送；
<!-- more -->
3. 支持多主控(multimastering)，任何时间点只能有一个主控；
4. 在主从通信中，可以有多个I2C总线器件同时接到I2C总线上，所有与I2C兼容的器件都具有标准的接口，通过地址来识别通信对象；
<img src="http://kyunsmile.qiniudn.com/20150514-300px-I2C.svg.png"/>
5. 控制信号分为地址码和数据码两部分：地址那用来选址，即接通需要控制的电路；数据码是通信的内容。

#应用#
1. 为了保存用户的设置而访问NVRAM芯片。
2. 访问低速的数字模拟转换器（DAC）。
3. 访问低速的模拟数字转换器（ADC）。
4. 改变监视器的对比度、色调及色彩平衡设置（视频数据通道）。
5. 改变音量大小。
6. 获取硬件监视及诊断数据，例如中央处理器的温度及风扇转速。
7. 读取实时时钟（Real-time clock）。
8. 在系统设备中用来打开或关闭电源供应。

#操作#
<img src="http://kyunsmile.qiniudn.com/20150514-600px-I2C_data_transfer.svg.png"/>

<img src="http://kyunsmile.qiniudn.com/20150514-24148050_1297772233n55u.jpg"/>

##初始化##
将SDA和SCL都变成高电平
```
void init() //初始化  
{  
    SDA=1;  
    delay();  
    SCL=1;  
    delay();      
}  
```

##开始信号##
<img src="http://kyunsmile.qiniudn.com/20150514-24148050_1297772090hlSk.jpg"/>

SCL为高电平时，SDA由高电平向低电平跳变，开始传送数据。

```
void start()//起始信号  
{  
    SDA=1;  
    delay();  
    SCL=1;  
    delay();  
    SDA=0;  
    delay();  
}  
```

##地址##
* 发送地址字（芯片的硬件地址），即使确定要对之进行操作的芯片。
* 在I2C总线协议中地址必须是起始条件后作为第一个字节发送。
* 使用I2C总线的芯片地址应包括固定部分和可编程部分。可编程部分必须根据地址引脚来确定。
* 地址字节的最后一位是用于设置以后传输方向的读/写位。
* 不同芯片地址字节的设置可能不同？

##应答##
* Master每发送完8bit（地址/命令字）数据后都要等待Slave的ACK，以确定数据传送是否被对方收到。
* 应答信号由接收设备产生。
* 在第9个clock，若从IC发ACK，SDA会被拉低，则说明数据传输正确；若没有ACK，SDA会被置高，这会引起Master发生RESTART或STOP流程，如下所示：

```
void respons()//应答(相当于一个智能的延时函数  )
{  
    uchar i;  
    SCL=1;  
    delay();  
    while((SDA==1)&&(i<250))//没收到应答则等待
        i++;        
//等了250次没收到就不管他了，就当他收到了
//其实没收到的话可以结束程序的  
//强行将SCL拉低
    SCL=0;  
    delay();  
}  
```

##写数据##
###写寄存器的标准流程###
1. Master发起START
2. Master发送I2C addr（7bit）和w操作0（1bit），等待ACK
3. Slave发送ACK
4. Master发送reg addr（8bit），等待ACK
5. Slave发送ACK
6. Master发送data（8bit），即要写入寄存器中的数据，等待ACK
7. Slave发送ACK
8. 第6步和第7步可以重复多次，即顺序写多个寄存器
9. Master发起STOP

写一个数据
<img src="http://kyunsmile.qiniudn.com/20150514-24148050_1297772295fNrI.jpg"/>
写多个数据
<img src="http://kyunsmile.qiniudn.com/20150514-24148050_1297772325ih8z.jpg"/>

###写时序###
1. 先将SCL置0（只有它为0的时候SDA才允许变化）
2. 改变SDA是数值（就是你当前要穿的一位是0还是1）
3. 把SCL置1（此时芯片就会读取总线上的数据）

```
#define uchar unsigned char  
#define uint unsigned int  
void write_byte(uchar date) //写一字节数据  
{  
    uchar i,temp;  
    temp=date;  
    for(i=0;i<8;i++)  
    {  
        temp=temp<<1; //左移一位 移出的一位在CY中  
        SCL=0;          //只有在scl=0时sda能变化值  
        delay();  
        SDA=CY;  
        delay();  
        SCL=1;  
        delay();          
    }     
    SCL=0;  
    delay();  
    SDA=1;  
    delay();  
}  
```

##读数据##
###读寄存器的标准流程###
1.    Master发送I2C addr（7bit）和w操作1（1bit），等待ACK
2.    Slave发送ACK
3.    Master发送reg addr（8bit），等待ACK
4.    Slave发送ACK
5.    Master发起START
6.    Master发送I2C addr（7bit）和r操作1（1bit），等待ACK
7.    Slave发送ACK
8.    Slave发送data（8bit），即寄存器里的值
9.    Master发送ACK
10.    第8步和第9步可以重复多次，即顺序读多个寄存器

读一个数据
<img src="http://kyunsmile.qiniudn.com/20150514-24148050_1297772425TZt2.jpg"/>

读多个数据
<img src="http://kyunsmile.qiniudn.com/20150514-24148050_1297772459j7ru.jpg"/>


```
uchar read_byte()  
{  
    uchar i,k;  
    SCL=0;  
    delay();  
    SDA=1;  
    delay();  
    for(i=0;i<8;i++)  
    {  
        SCL=1;  
        delay();  
        k=(k<<1)|SDA;//先左移一位，再在最低位接受当前位  
        SCL=0;  
        delay();  
    }  
    return k;  
}  
```

##终止信号##
SCL为高电平时，SDA由低电平向高电平跳变，结束传送数据。

```
void stop() //停止信号  
{  
    SDA=0;  
    delay();  
    SCL=1;  
    delay();  
    SDA=1;  
    delay();  
}  
```