2020年新工科联盟-Xilinx暑期学校团队项目设计文档
设计文稿提交格式
(Project Paper Submission Template)







作品名称	A13_摇摇乐（陀螺仪+AWS）
板卡型号	                      xc7s15ftgb196-1
所在班级	             西南交通大学暑期学校A1班(通信一班)
成员姓名、学号、学校	
邱渝-2018112815-西南交通大学


Github链接	https://github.com/Doll216/High-Level-Synthesis-2018112815.git



第一部分
设计概述 /Design Introduction
（1.请概括地描述一下你的设计，可包括本设计目的、学习到的知识点、应用方向或者设想的应用场景等；2. 经组内成员讨论后以表格的形式描述项目中各成员在项目中发挥的作用或者贡献百分比；3.作品的展示照片）
1.
设计目的：通过ESP32连接AWS_IoT云平台，可以直接在AWS_IoT监测云平台中读取板载陀螺仪中的数据。既是为了学习一种新技能，也是为了增加AWS_IOT云平台的应用领域。

应用领域与适用范围：充分发挥AWS云平台智能化的功能。可应用于智能化自动检测物理上的振动频率，也可以应用与高精度仪器震动的测量。

2.
成员为1人，故均由一人独立完成（邱渝）。

3.
成果为摇动开发板，从陀螺仪中读取数据并传送到AWS平台上，作品结果由串口监视器演示。















第二部分
系统组成及功能说明 /System Construction & Function Description
（请对作品的1. 计划实现及已实现的功能；2. 项目系统框图；3. 使用的技术方向做说明）
1.计划实现的功能：在ESP32的WIFI联网后，晃动开发板，可以从AWS IoT平台得到晃动开发板的次数。
   已实现的功能：在ESP32的WIFI联网后，晃动开发板，可以从AWS IoT平台得到晃动开发板时板载陀螺仪的数据。

2.项目系统框图


3.使用的技术方案
技术方案：如上图的系统结构框图所示，该项目的主要技术过程为：在FPGA中完成对板载陀螺仪的数据读取，并将传感器数据简单处理后存储。 ESP32读取FPGA存储的陀螺仪数据，发送至AWS IoT服务器中。
其中FPGA中主要含有4个模块：
1.IIC driver模块主要负责解析IIC信号，从板载陀螺仪中获取陀螺仪数据；
2.Gyro driver模块负责解析原始的陀螺仪数据，并将数据一串转并，存放在RAM中；
3.QSPI Slave模块负责解析QSPI信号，对ESP32的QSPI信号进行响应；
4.ESP32通过QSPI的接口，读取FPGA中存放的陀螺仪数据，最终通过wife将数据
传输至AWS IoT的数据平台中。

   FPGA中的四个模块首先在vivado软件中分模块编写，分别为Clk_Division, Driver_IIC, Driver_Gyro,
Gyro2ram, qspi_slave, Gyro_Demo，调用所需要的IP核 clk_wiz, blk_mem_gen并根据代码里所需求的接口调整参数；并编写constraints。

调试完成后，下载bit文件至SD卡中，将SD卡插入开发板；
在Arduino中编写完成开发板与AWS_IoT平台的连接的工程，注册AWS账户并调试获取AWS链接，









并在MQTT中测试，

接下来，便是在arduino上编写好与AWS_IoT连接的相关编程代码与调试，下载至开发板中，在串口监视器中观察读取到的数据








第三部分
完成情况及性能参数 /Final Design & Performance Parameters
（作品已实现的功能及性能指标）

FPGA中主要含有4个模块：
1.已完成IIC driver模块，可以做到解析IIC信号，从板载陀螺仪中获取陀螺仪数据；
2.已完成Gyro driver模块，可以做到解析原始的陀螺仪数据，并将数据一串转并，存放在RAM中；
3.已完成QSPI Slave模块，可以做到解析QSPI信号，对ESP32的QSPI信号进行响应；
4.已完成ESP32通过QSPI的接口，读取FPGA中存放的陀螺仪数据，最终通过wife将数据
传输至AWS IoT的数据平台中。



第四部分
总结 /Conclusions
（谈一谈完成暑期学校课程后的收获与感想。请每位组员分开写。）

邱渝：

该项目涉及到的知识点广，综合性高，牵涉到学会和掌握FPGA的开发；学会和掌握ESP32的开发；学会使用SEA-Board板载ESP32与FPGA协同工作的机理；学会使用SEA-Board板载FPGA读取板载陀螺仪的相关数据；学会使用SEA-Board板载ESP32建立与PC和AWS IoT平台的连接。
且该项目是与广泛而深入地渗透到我们日常生活中的AWS云平台的一次尝试，对深入了解AWS云平台的功能，并以AWS云平台为基础去开发更多的全新应用具有显著的启迪意义。
