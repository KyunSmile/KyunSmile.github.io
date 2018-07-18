title: PID part2
date: 2015-08-07 16:40:43
categories: 
- 凊筠什么的最厌学了
- 单片机
tags: PID
---

# 分类 # 
`位置式PID算法`
- 缺点：当前采样时刻的输出与过去的各个状态有关，计算时要对e(k)进行累加，运算量大，而且控制器的输出u(k)对应的是执行机构的实际位置，如果计算机出现故障，u(k)的大幅度变化会引起执行机构位置的大幅度变化。

<!-- more -->

`增量式PID算法`
- 概念：
增量式PID是指数字控制器的输出只是控制量的增量Δu(k)。
采用增量式算法时，计算机输出的控制量Δu(k)对应的是本次执行机构位置的增量，而不是对应执行机构的实际位置，因此要求执行机构必须具有对控制量增量的累积功能，才能完成对被控对象的控制操作。执行机构的累积功能可以采用硬件的方法实现；也可以采用软件来实现，如利用算式 u(k)=u(k-1)+Δu(k)程序化来完成。

- 优点：
  1. 算式中不需要累加。控制增量Δu(k)的确定仅与最近3次的采样值有关，容易通过加权处理获得比较好的控制效果；
  2. 计算机每次只输出控制增量，即对应执行机构位置的变化量，故机器发生故障时影响范围小、不会严重影响生产过程；
  3. 手动—自动切换时冲击小。当控制从手动向自动切换时，可以作到无扰动切换。

- 注意:
PID的数学模型就应该是位置式，单独的增量式里面那样的式子能算积分吗？显然不是，增量式的提出就是为了解决计算机运算的问题。实际的PID就应该是位置式，如果你的执行机构硬件不具备累加功能，就得用软件把增量式累加上前一次的控制值再送执行机构控制。譬如，电机的调速。PWM1（这次的控制）=PWM0(上一次的控制量)+ ⊿PWM（增量）。


# PID算法流程图 #

```flow
st=>start: 入口
e=>end: 返回
op1=>operation: 读取给定值r(k)
op2=>operation: 读取反馈值c(k)
op3=>operation: 计算偏差e(k)=r(k)-c(k)
op4=>operation: 计算△u(k)=a0e(k)+a1e(k-1)+a2e(k-2)
op5=>operation: 存△u(k)以备输出
op6=>operation: 参数序号e(k-1)->e(k-2)调整e(k)->e(k-1)
st->op1->op2->op3->op4->op4->op6->e
```

# PD算法程序 #
```
#include "pdi.h"    
#include "stm32f10x.h"

#define  Kp 130//PID 调节的比例常数
#define Ti 0.005 //PID 调节的积分常数
#define Td 30//PID 调节的微分时间常数
#define T 0.01 //采样周期		

//基本上用PD就行了。
int ek=1; //偏差e[k]
int ek1=1; //偏差e[k-1]
int ek2=1; //偏差e[k-2]
int uk=0; //u[k]
int adjust=0; //最终输出的调整量

int a0=Kp*(1+T/Ti+Td/T);
int a1=-Kp*(1+2*Td/T);
int a2=Kp*Td/T;


// Ki=KpT/Ti=0.8，微分系数Kd=KpTd/T=0.8,Td=0.0002,根据实验调得的结果确定这些参数

int pid(int ek)
{
		uk=a0*ek+a1*ek1+a2*ek2;
		ek2=ek1;
		ek1=ek;
		adjust=uk;
		return adjust;
}
```

# PID算法C语言√ #
```
//定义变量
float Kp;                       //PID调节的比例常数
float Ti;                       //PID调节的积分常数
float T;                        //采样周期
float Td;                       //PID调节的微分时间常数
float a0;
float a1;
float a2;

float ek;                       //偏差e[k]
float ek1;                      //偏差e[k-1]
float ek2;                      //偏差e[k-2]
float uk;                       //u[k]
int uk1;                      //对uk四舍五入求整
int adjust;                   //最终输出的调整量

//变量初始化，根据【实际情况】初始化
    Kp=;
    Ti=;
    T=;
    Td=;   

    a0=Kp*(1+T/Ti+Td/T);
    a1=-Kp*(1+2*Td/T);
    a2=Kp*Td/T;
    
// Ki=KpT/Ti=0.8，微分系数Kd=KpTd/T=0.8,Td=0.0002,根据实验调得的结果确定这些参数

    ek=0;
    ek1=0;
    ek2=0;
    uk=0;
    uk1=0;
    adjust=0;


int pid(float ek)
{
    if(gabs(ek)<ee) //ee 为误差的阀值，小于这个数值的时候，不做PID调整，避免误差较小时频繁调节引起震荡。ee的值可自己设
        {
                adjust=0;
        }
    else
        {
                uk=a0*ek+a1*ek1+a2*ek2;
                ek2=ek1;
                ek1=ek;
            uk1=(int)uk;
        
            if(uk>0)
                {
           if(uk-uk1>=0.5)
                   {
              uk1=uk1+1;
                   }
                }
       if(uk<0)
           {
          if(uk1-uk>=0.5)
                  {
             uk1=uk1-1;
                  }
           }
         
           adjust=uk1;    
    }
        return adjust;
    
}

float gabs(float ek)
{
        if(ek<0)
        {
                ek=0-ek;
        }
        return ek;
}
```

# PID算法程序(好长好长看不懂版) #
```
//================================================================ 
// pid.H 
// Operation about PID algorithm procedure  
// C51编译器  Keil 7.08 
//================================================================ 
// 作者:zhoufeng 
// Date :2007-08-06 
// All rights reserved. 
//================================================================ 

#include <reg52.h> 
#include <intrins.h> 
typedef   unsigned   char        uint8;        
typedef   unsigned   int         uint16;   
typedef   unsigned   long int    uint32;  
/**********函数声明************/ 
void     PIDOutput (); 
void     PIDOperation ();  
/*****************************/ 
typedef struct PIDValue 
{ 
uint32      Ek_Uint32[3];                  //差值保存，给定和反馈的差值 
uint8       EkFlag_Uint8[3];              //符号，1则对应的为负数，0为对应的为正数      
uint8       KP_Uint8; 
uint8       KI_Uint8; 
uint8       KD_Uint8; 
uint16      Uk_Uint16;                 //上一时刻的控制电压 
uint16      RK_Uint16;                //设定值 
uint16      CK_Uint16;               //实际值  
}PIDValueStr; 
PIDValueStr  PID; 
uint8        out ;                 // 加热输出 
uint8        count;               // 输出时间单位计数器 
/********************************* 
PID = Uk + KP*[E(k)-E(k-1)]+KI*E(k)+KD*[E(k)-2E(k-1)+E(k-2)];(增量型PID算式) 
函数入口: RK(设定值),CK(实际值),KP,KI,KD 
函数出口: U(K) 
//PID运算函数 
********************************/ 
void     PIDOperation (void)   
{  
uint32       Temp[3];                                        //中间临时变量 
uint32       PostSum;                                       //正数和 
uint32       NegSum;                                       //负数和 
Temp[0] = 0; 
Temp[1] = 0; 
Temp[2] = 0; 
PostSum = 0; 
NegSum  = 0; 
if( PID.RK_Uint16 > PID.RK_Uint16 )                    //设定值大于实际值否？ 
{ 
  if( PID.RK_Uint16 - PID.RK_Uint16 >10 )            //偏差大于10否？ 
  { 
   PID.Uk_Uint16 = 100;    }                        //偏差大于10为上限幅值输出(全速加热) 
  else 
  { 
   Temp[0] = PID.RK_Uint16 - PID.CK_Uint16;       //偏差<=10,计算E(k) 
   PID.EkFlag_Uint8[1]=0;                        //E(k)为正数 
   //数值移位 
      PID.Ek_Uint32[2] = PID.Ek_Uint32[1]; 
      PID.Ek_Uint32[1] = PID.Ek_Uint32[0]; 
      PID.Ek_Uint32[0] = Temp[0]; 
/****************************************/ 
      if( PID.Ek_Uint32[0] >PID.Ek_Uint32[1] )                            //E(k)>E(k-1)否？ 
      { 
  Temp[0]=PID.Ek_Uint32[0] - PID.Ek_Uint32[1];           //E(k)>E(k-1) 
        PID.EkFlag_Uint8[0]=0;  }                                       //E(k)-E(k-1)为正数 
   else 
{ 
  Temp[0]=PID.Ek_Uint32[0] - PID.Ek_Uint32[1];        //E(k)<E(k-1) 
        PID.EkFlag_Uint8[0]=1;  }                                               //E(k)-E(k-1)为负数 
/****************************************/ 
      Temp[2]=PID.Ek_Uint32[1]*2 ;                                             // 2E(k-1) 
if( (PID.Ek_Uint32[0]+ PID.Ek_Uint32[2])>Temp[2] )            //E(k-2)+E(k)>2E(k-1)否？ 
      { 
  Temp[2]=(PID.Ek_Uint32[0]+ PID.Ek_Uint32[2])-Temp[2];     //E(k-2)+E(k)>2E(k-1) 
        PID.EkFlag_Uint8[2]=0;  }                                          //E(k-2)+E(k)-2E(k-1)为正数 
   else 
{ 
  Temp[2]=Temp[2]-(PID.Ek_Uint32[0]+ PID.Ek_Uint32[2]);  //E(k-2)+E(k)<2E(k-1) 
        PID.EkFlag_Uint8[2]=1;  }                                       //E(k-2)+E(k)-2E(k-1)为负数 
/****************************************/        
      Temp[0] = (uint32)PID.KP_Uint8 * Temp[0];                        // KP*[E(k)-E(k-1)] 
      Temp[1] = (uint32)PID.KI_Uint8 * PID.Ek_Uint32[0];              // KI*E(k) 
      Temp[2] = (uint32)PID.KD_Uint8 * Temp[2];                      // KD*[E(k-2)+E(k)-2E(k-1)] 

/*以下部分代码是讲所有的正数项叠加，负数项叠加*/      
/**********KP*[E(k)-E(k-1)]**********/ 
if(PID.EkFlag_Uint8[0]==0) 
  PostSum += Temp[0];                                    //正数和 
else                                               
  NegSum += Temp[0];                                    //负数和 
/********* KI*E(k)****************/  
if(PID.EkFlag_Uint8[1]==0)       
  PostSum += Temp[1];                                 //正数和 
else 
   ;                                                 //空操作，E(K)>0 
/****KD*[E(k-2)+E(k)-2E(k-1)]****/                            
if(PID.EkFlag_Uint8[2]==0) 
PostSum += Temp[2];                               //正数和 
else 
  NegSum += Temp[2];                             //负数和 
/***************U(K)***************/                              
PostSum += (uint32)PID.Uk_Uint16;     
         
if(PostSum > NegSum )                         // 是否控制量为正数 
{ Temp[0] = PostSum - NegSum; 
if( Temp[0] < 100 )                         //小于上限幅值则为计算值输出 
PID.Uk_Uint16 = (uint16)Temp[0]; 
else 
  PID.Uk_Uint16 = 100;                     //否则为上限幅值输出 
} 
else                                     //控制量输出为负数，则输出0(下限幅值输出) 
   PID.Uk_Uint16 = 0; 
} 
} 
else  
{ PID.Uk_Uint16 = 0;  }  

} 

/********************************* 
函数入口: U(K) 
函数出口: out(加热输出) 
//PID运算植输出函数 
********************************/ 
void     PIDOutput (void)   
{  
static  int i; 
i=PID.Uk_Uint16; 
if(i==0) 
  out=1; 
else out=0; 
if((count++)==5)//如定时中断为40MS,40MS*5=0.2S(输出时间单位),加热周期20S(100等份) 
{              //每20S PID运算一次 
  count=0; 
  i--; 
} 
}
```




http://wenku.baidu.com/link?url=uPkcvhMb4Cp4ddupz3xps7EFIM1wFLvjwfFQD0EVkSzQuueBix2CmwMWcdDuCioNEEzxKFP9siAFdrsVmqcZScvvHKZ6BjGvCQ0DQhbl_au