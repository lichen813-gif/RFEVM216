# 4.5 PS 端以太网使用之 lwip

[Switch to English](../../../en/fpga-tutorial/04-ps-peripherals/05-lwip-ethernet.md)

[返回章节总览](index.md)

LWIP 是瑞典计算机科学院（SICS）的 Adam Dunkels 等开发的一个小型开
源的 TCP/IP 协议栈，是 TCP/IP 的一种实现方式。LWIP 是轻量级 IP 协议，有无
操作系统的支持都可以运行。LWIP 实现的重点是在保持 TCP 协议主要功能的基
础上减少对 RAM 的占用，它只需要十几 KB 的 RAM 和 40K 左右的 ROM 就可
以运行，这使 LWIP 协议栈适合在低端的嵌入式系统中使用。
这里我们使用 Vitis 软件自带的 Lwip Echo Server 模板了解 LWIP 的使用。

## 4.5.1 硬件设计

RFEVM216 开发板上有一个 PS 端的 RJ45 以太网接口，用于连接以太网线，
其原理图如图所示：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-125-image-01.jpg)

图 13 RJ45 接口原理图
以太网的数据传输离不开以太网 PHY（物理层）芯片的支持。RFEVM216
开发板上使用的 PHY 芯片为德州仪器(Texas Instruments)的 DP83867ISRGZ 芯
片，其部分原理图如图所示：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-126-image-01.jpg)

图 14 DP83867ISRGZ 原理图

## 4.5.2 软件设计

BSP 库文件里面添加 lwip 库
双击 platform.spr，选中 Board Support Package，点击 Modify BSP Settings...

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-127-image-01.jpg)

使能 lwip 库，点击 OK
编译 paltform

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-128-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-128-image-02.jpg)

新建应用程序 File->New->Application Project
点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-129-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-129-image-02.jpg)

点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-130-image-01.jpg)

设置 APP 名称，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-131-image-01.jpg)

点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-132-image-01.jpg)

选择 Lwip Echo Server 模板，点击 Finish
我们修改板卡的 ip 和网段，是板卡和 PC 处于同一个网段

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-133-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-133-image-02.jpg)

修改完成之后，保存文件，右键 lwip_echo_server 工程，点击 Build Project

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-134-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-134-image-02.jpg)

## 4.5.3 下载验证

1. 这里我们用千兆网线连接 PC 和 RFEVM 开发板，然后给板卡上电
2. PC 和 RFEVM 的 IP 地址要在同一个网段，才可以相互通信。

RFEVM216 以太网的的默认配置：
mac 地址：00: 0a: 35: 00: 01: 02
IP 地址：192.168.5.10
子网掩码：255.255.255.0
网关：192.168.5.1

3. 右键 lwip_echo_server 工程，选择 Run As->Run Configuration

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-135-image-01.jpg)

4. 我们打开串口调试终端，下载完程序后，终端会显示程序的打印信息
5. 打开 cmd 窗口，ping 板卡 IP

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-136-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-136-image-02.jpg)

## 4.5.4 参考文档

https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842366/Standalone+LWIP+lib
rary
