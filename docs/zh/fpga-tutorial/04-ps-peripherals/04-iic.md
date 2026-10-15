# 4.4 PS 端 IIC 的使用

[Switch to English](../../../en/fpga-tutorial/04-ps-peripherals/04-iic.md)

[返回章节总览](index.md)

## 4.4.1 硬件设计

PS 端 IIC 接了一个外设 EEPROM，本节介绍如何利用 IIC 读写外设。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-119-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-119-image-02.jpg)

## 4.4.2 软件设计

1. 登录 Vitis，切换到之前的工作目录，然后双击 platform.spr，选中 Board Support

Package，可以看到 psu_i2c_1 的文档链接和导入示例。

2. 点击 Import Example，然后选中 xiicps_eeprom_polled_example 示例，点击

OK

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-120-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-120-image-02.jpg)

3. 可以看到导入的示例应用工程
4. EEPROM 的设备地址在程序的前面做了定义，这个地址就是系统访问外部

IIC 外设的设备地址，这里 EEPROM 地址修改为 0x50，然后保存。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-121-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-121-image-02.jpg)

EEPROM 的设备地址可以在 AT24CM01 的芯片手册上找到。
其中 A1、A2 硬件里面直接接地，为 0；
程序流程如下：
ReadBuffer 清 0，WriteBuffer 赋递增数据->写 32 个字节到 EEPROM->读
EEPROM 的 16 个字节到 ReadBuffer->检验是否正确->返回。

5. 选中应用工程，右键点击 Build Project

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-122-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-122-image-02.jpg)

编译信息可以在 Console 窗口中看到

## 4.4.3 下载验证

首先我们将下载线（USB 转 Type-C 线缆）与开发板的 JTAG 接口连接，另

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-123-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-123-image-02.jpg)

外一端与电脑连接。最后打开开发板的电源开关。
右键应用工程，选择 Run As->Launch Hardware(Single Application Debug)
打开串口终端，下载完成后，可以查看串口输出：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-124-image-01.jpg)
