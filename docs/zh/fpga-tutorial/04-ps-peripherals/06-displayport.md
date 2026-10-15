# 4.6 PS 端 DiplayPort 的使用

[Switch to English](../../../en/fpga-tutorial/04-ps-peripherals/06-displayport.md)

[返回章节总览](index.md)

## 4.6.1 硬件设计

RFEVM216 底板上有一路 DP 显示接口，可以连接 DP 显示器进行输出。设
计原理框图如下所示：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-137-image-01.jpg)

## 4.6.2 软件设计

1. 双击 platform.spr，选中 Board Support Package
2. 点击 Import Example，然后选中 xdpdma_video_example 示例，点击 OK

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-138-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-138-image-02.jpg)

3. 选中应用工程，右键点击 Build Project

## 4.6.3 下载验证

这里我们需要使用 DP 数据线一端连到带 DP 接口的显示器上，另外一端连
到板卡的 DP 接口。然后给开发板上电。
右键应用工程，选择 Run As->Launch Hardware(Single Application Debug)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-139-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-139-image-02.jpg)

打开串口终端，下载完成后，可以查看串口输出：
同时显示器上输出彩条

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-140-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-140-image-02.jpg)
