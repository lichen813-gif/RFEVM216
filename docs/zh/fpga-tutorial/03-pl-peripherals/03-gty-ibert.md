# 3.3 GTY 收发器误码率测试 IBERT 实验

[Switch to English](../../../en/fpga-tutorial/03-pl-peripherals/03-gty-ibert.md)

[返回章节总览](index.md)

IBERT（集成式比特误码率测试仪）是 Xilinx 面向 UltraScaleTM/UltraScale+TM
架构 GTY 收发器专门设计的，用于评估和监控 GTY 收发器。IBERT 包括采用
FPGA 逻辑实现的模式生成器和检查器，并能够接入 GTY 收发器的端口和动态
重配置端口属性。还包括了通信逻辑，可通过 JTAG 在运行时进行访问。
IBERT 工具用于对 Xilinx FPGA 芯片的高速串行收发器进行板级硬件测试。
通过 IBERT 可以获取误码率，观察眼图，调节串行收发器的参数，从而有助于
判断可能存在的问题，便于验证硬件的稳定性和信号完整性。

## 3.3.1 硬件介绍

使用 IBERT 测试误码率和眼图必须有个收发环通的硬件，开发板上有两路
QSFP28 光纤接口。本实验可以将两路 QSFP28 光纤接口通过 100G 光纤连接起
来形成收发环通链路。
图 8 QSFP 硬件原理图

## 3.3.2 硬件工程搭建

1. 打开 vivado
2. 选择 Create Project

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-052-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-052-image-02.jpg)

3. 点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-053-image-01.jpg)

4. 设置工程名称（ibert_bank_all）和位置（E:/rfevm216/），点击 Next
5. 选择 RTL 工程，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-054-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-054-image-02.jpg)

6. 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next
7. 点击 Finish

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-055-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-055-image-02.jpg)

8. 点击 IP Catalog

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-056-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-056-image-02.jpg)

9. 选择 IBERT UltraScale GTY

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-057-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-057-image-02.jpg)

10. 双击 IBERT UltraScale GTY
11. 设置模块名称：ibert_bank_all

 在“Protocol Definition”选项卡下
Protocol Custom 1: LineRate 25, Refclk:156.25, Quad Count:2
 在“Protocol Selection”选项卡下
QUAD_130: Custom 1/25 Gbps, MGTREFCLK1 130
QUAD_131: Custom 1/25 Gbps, MGTREFCLK1 131
 在“Clock Settings”选项卡下，设置时钟

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-058-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-058-image-02.jpg)

 查看摘要，并点击“OK”

12. 点击“Skip”

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-059-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-059-image-02.jpg)

 生成的 IBERT IP 出现在 Design Sources

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-060-image-01.jpg)

13. 右键 ibert_bank_all，选择 Open IP Example Design ...

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-061-image-01.jpg)

14. 选择位置并点击 OK
15. 创建一个新的工程

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-062-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-062-image-02.jpg)

16. 点击 Generate Bitstream
17. 点击【OK】，等待生成 bit

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-063-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-063-image-02.jpg)

18. 生成 bit 完成之后，选择【View Reports】，点击 OK

## 3.3.3 下载验证

1. 点击 Open Hardware Manager->Open Target->Auto Connect

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-064-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-064-image-02.jpg)

2. 选择 Program device
3. Bitstream file 和 LTX 文件默认，点击 Program

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-065-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-065-image-02.jpg)

4. 点击 Create links
5. 依次选择 MGTX0Y12~MGTX0Y19，点击添加按钮，然后点击 OK

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-066-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-066-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-067-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-068-image-01.jpg)

6. Links 会出现在 Serial I/O Links 选项卡下
7. 点击 BERT Reset，复位 link error 计数器，links 显示 no errors

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-069-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-069-image-02.jpg)

## 3.3.4 参考文档

 IBERT IP
IBERT for UltraScale GTY Transceivers - PG196
https://docs.xilinx.com/v/u/en-US/pg196-ibert-ultrascale-gty
 Vivado Programming and Debugging
Vivado Design Suit Programming and Debugging User Guide - UG908
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/
Introduction

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-070-image-01.jpg)
