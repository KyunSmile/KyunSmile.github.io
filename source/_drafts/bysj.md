title: 毕业设计（未完...
date: 2017-03-24 20:29:34
categories: 
- 凊筠什么的最厌学了
tags:
---

- [ ] **毕业设计**
    - [ ] 投入式液位变送器
        - [X] 原理
        - [ ] 电路
        - [ ] 控制
    - [ ] 温度控制
        -  [ ] DS18B20
        -  [ ] 加热棒
            -  [ ] 电路
            -  [ ] 控制
<!-- more -->

# 投入式液位变送器

## 介绍

投入式液位传感器是一种测量液位的**压力传感器**，是基于**所测液体静压与该液体高度成正比**的原理，采用扩散硅或陶瓷敏感元件的压阻效应，将静压转成电信号。经过温度补偿和线性校正,转换成4-20mADC标准电流信号输出。投入式液位变送器的传感器部分可直接投入到液体中，变送器部分可用法兰或支架固定，安装使用极为方便。

## 参数

* 供电：24VDC
* 输出：4-10mA

> AC~alternating current~交流电
DC~direct current~直流电

## 电路连接

### 电路模块图

```graphLR
    A(液位变送器)--> B(I/V变换电路)
    B --> D(单片机ADC引脚)
```

### 输出变换

**[4-20ma电流转电压电路](http://wenku.baidu.com/link?url=fi081M2exx6bvJQp1sGABOZaKogI8teElHSsQEIKtEfHwbmrPZPE2oYB9yRCUgX2xs6fj3bWKEn6OtBCt_Pq5Ykvo7gpFgcfJruh4_96oUK)**
        
**[4～20mA输入0～5V输出的IV转换电路](http://wenku.baidu.com/link?url=96oL1id4O406unWdcIjx13Rkz5pZG9Zdk59nbWYdeLTOw84zeBLpdNFNqJMhxKF1-evvs9dIc5l1HGKvJn2q_7dFBMchvE4knyllstyqtYa)**

**[液位变送器输出的变换电路图](http://www.ybzhan.cn/Tech_news/Detail/107229.html)**

> **利用BB公司的RCV420的变换电路**
    RCV420是 BB公司的产品。它能将4～20mA变换为0～5V。它的电源电压额定值为±15V，静态电流为3mA，工作温度范围-55～125℃。虽然说明书中给出的电源是双电源，但也可以应用于单电源0～24V的场合，这就十分方便，应用时不加任何外部元件。
    ![](http://www.chinabaike.com/uploads/allimg/130825/1302106160-4.jpg)
    
---

# 加热棒

[TB连接：低压直流/交流加热棒](https://item.taobao.com/item.htm?spm=a230r.1.14.36.vtF7O3&id=36796812189&ns=1&abbucket=11#detail)

---

# DS18B20

[TB连接：DS18B20防水封装](https://detail.tmall.com/item.htm?spm=a230r.1.14.26.vPVTU6&id=41284364687&ns=1&abbucket=11)

---

# 晶闸管/可控硅

> [参考资料：可控硅工作原理及应用](http://wenku.baidu.com/link?url=mCbrnPSwCu0CJ_2iFwrGrGmg8sbzoXippVqDF5BgxcBOiJ-OAgD8YQtiy7OENbJkYGzOGWj_mLBeSEbsGuoNq9Zk4RDx0k5taMo9FG1pXCy)

## 简介

可控硅，是可控硅整流元件的简称，是一种具有三个PN结的四层结构的大功率半导体器件，亦称为晶闸管。具有体积小、结构相对简单、功能强等特点，是比较常用的半导体器件之一。该器件被广泛应用于各种电子设备和电子产品中，多用来作可控整流、逆变、变频、调压、无触点开关等。

> 整流（交流->直流）
逆变（直流->交流）
变频（交流->交流）
斩波（直流->直流）

## 工作原理

* 结构

   ![](https://imgsa.baidu.com/baike/w%3D268/sign=69c93d9a62d9f2d3201123e991ec8a53/6a63f6246b600c339579dcb31a4c510fd9f9a14c.jpg)
    
    晶闸管是由四层半导体材料组成的，有三个PN结，对外有三个电极：
    
    * 第一层P型半导体引出的电极叫阳极A
    * 第三层P型半导体引出的电极叫控制极G
    * 第四层N型半导体引出的电极叫阴极K。
    
    从晶闸管的电路符号可以看到，它和二极管一样是一种单方向导电的器件，关键是多了一个控制极G，这就使它具有与二极管完全不同的工作特性。

* 工作原理

    * **晶闸管具有单向导电性**
    正向导通条件：A、K间加正向电压，G、K间加触发信号。
    * **晶闸管一旦导通，控制极失去作用**
    若使其关断，必须降低 UAK或加大回路电阻，把阳极电流减小到维持电流以下。

## 应用

### 可控整流电路

### 触发电路

### 单结管触发的可控整流电路

### 晶闸管的其他应用
