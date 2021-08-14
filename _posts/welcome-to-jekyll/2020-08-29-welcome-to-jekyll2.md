---
layout: post
title: Welcome to Jekyll!2
date: 2020-08-29 13:00:00 +0800
categories: jekyll update
---
VL53L0X是新一代的飞行时间（ToF）激光测距模块，采用当今市场上最小的封装，与传统技术不同，无论目标反射率如何，都能提供精确的距离测量。 它可以测量高达2m的绝对距离，在性能范围内设定新的基准，为各种新应用打开了大门。

VL53L0X集成了领先的SPAD阵列（单光子雪崩二极管），并嵌入了ST的第二代FlightSenseTM专利技术。

VL53L0X的940 nm VCSEL发射器（垂直腔表面发射激光器）对人眼是完全不可见的，再加上内部物理红外滤光片，它可以实现更长的测距距离，更高的环境光抗扰性和更好的鲁棒性以覆盖玻璃光学串扰 。

**\#\# 注意**

I2C仅允许每个设备一个地址，因此您必须确保每个I2C设备都有一个唯一的地址。 VL53L0X的默认地址为0x29，但是您可以在软件中更改它。

要设置新地址，可以使用以下两种方法之一。 在初始化期间，不调用lox.begin（），而是调用lox.begin（0x30）将地址设置为0x30。 或者，您以后可以随时调用lox.setAddress（0x30）。

**\#\# 硬件设备**

\- ESP8266

\- VL53L0X

**\#\# 物理接线**

\!\[image.png\](https://upload-images.jianshu.io/upload\_images/3246153-2a951a1b34f7f8fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ESP8266 \| VL53L0X

\-\|-

D1\| SCL\|

D2\| SDA\|

Vin \| 5v \|

GND \| GND \|

**\#\# 软件代码**

\`\`\`

\#include "Adafruit\_VL53L0X.h"

Adafruit\_VL53L0X lox = Adafruit\_VL53L0X();

void setup() \{

 Serial.begin(115200);

 // wait until serial port opens for native USB devices

 while (\! Serial) \{

 delay(1);

 \}

 Serial.println("Adafruit VL53L0X test");

 if (\!lox.begin()) \{

 Serial.println(F("Failed to boot VL53L0X"));

 while(1);

 \}

 // power

 Serial.println(F("VL53L0X API Simple Ranging example\\n\\n"));

\}

void loop() \{

 VL53L0X\_RangingMeasurementData\_t measure;

 Serial.print("Reading a measurement… ");

 lox.rangingTest(&measure, false); // pass in 'true' to get debug data printout\!

 if (measure.RangeStatus \!= 4) \{ // phase failures have incorrect data

 Serial.print("Distance (mm): "); Serial.println(measure.RangeMilliMeter);

 \} else \{

 Serial.println(" out of range ");

 \}

 delay(100);

\}

\`\`\`

**\#\# 截图**

\!\[image.png\](https://upload-images.jianshu.io/upload\_images/3246153-6856b8ac60d7f59f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/720)
