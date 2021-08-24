>## 程序介绍
>- [工程结构](#工程结构)
>- [EC200S调试](#EC200调试)
>    - [网络状态测试](#网络状态测试)
>    - [阿里云接入测试](#阿里云接入测试)
><br>
>


### 工程结构
drvier文件夹中的源文件一般不改，只做扩展，功能在device中实现
保持底层接口的通用性


（还没写，有时间一定搞完）


### EC200调试
模块调试可以使用测试板直接插USB转串口模块进行测试，其中USB转串口的5V要插到测试板的3V3上为串口电平转换芯片启动电压。
接好后上电网络指示灯开始闪烁以后可以发送指令测试。指令后要带换行
测试设备car_test为例
```Json
  "ProductKey": "a1hxPBnhq2a",
  "DeviceName": "car_test",
  "DeviceSecret": "b564fefb6d6aeb783342c0b9783d997c"
```
#### 网络状态测试
开启命令回显
```ATE1```

查询SIM卡状态
```AT+CPIN?```

查询网络注册状态
```AT+CREG?```

#### 阿里云接入测试
PDP激活检测
```AT+CGATT?```

ACT激活检测
```AT+QIACT?```

关闭当前连接
```AT+QIDEACT=1```

关闭MQTT客户端
```AT+QMTCLOSE=0```

关闭和MQTT服务器的所有连接
```AT+QMTDISC=0```

配置阿里云信息
```AT+QMTCFG=”aliauth”,0,”a1hxPBnhq2a”,”car_test”,”b564fefb6d6aeb783342c0b9783d997c”```

打开阿里云连接
```AT+QMTOPEN=0,”iot-as-mqtt.cn-shanghai.aliyuncs.com”,1883```

连接阿里云设备
```AT+QMTCONN=0,”car_test”```

订阅阿里云消息
```AT+QMTSUB=0,1,”/ a1hxPBnhq2a /car_test/user/get”,0```

发布阿里云消息
```
AT+QMTPUB=0,0,0,0,”/sys/a1hxPBnhq2a/car_test/thing/event/property/post”
```
返回``>``之后发送
```c
{params:{battery:91,loop:1,CarStatus:1}}
```

再次发送字符
```C
'0x1A'
```
需要在阿里云后台定义好要上传的参数与标识符，在MCU中打印为字符串格式即可上传至阿里云。
```c
sprintf(upload, "{params:{power:%d,status:%d}}", power, status);
```




