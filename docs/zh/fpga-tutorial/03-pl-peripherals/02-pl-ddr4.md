# 3.2 PL 端 DDR4 读写实验

[Switch to English](../../../en/fpga-tutorial/03-pl-peripherals/02-pl-ddr4.md)

[返回章节总览](index.md)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-028-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-028-image-02.jpg)

DDR4 SDRAM （ Double-Data-Rate Fourth Generation Synchronous Dynamic
Random Access Memory）是一种高速动态随机存取存储器，它属于 SDRAM 家
族的存储器产品，提供了相较于 DDR3 SDRAM 更高的运行性能与更低的电压。
由于 DR4 的时许非常复杂，如果直接编写 DDR4 的控制器代码，那么工作
量是非常大的，且性能难以得到保证。值得一提的是，Vivado 软件自带了 DDR4
控制器 IP 核，用户可以直接借助 IP 核来实现对 DDR4 的读写操作，从而大大降
低了 DDR4 的开发难度。本次实验将使用 Xilinx 公司的 MIG IP 核来实现 DDR4
的读写操作。
MIG（存储器接口）是一款用于为 AMD FPGA 生成存储器控制器和接口的
免费软件工具。下图是 MIG IP 核结构框图。MIG IP 核对外分出了两组接口，左
侧是用户接口，用户只有充分掌握这些接口才能操作 MIG；右侧为 DDR 物理芯
片接口，负责产生具体的操作时序并直接操作芯片管脚。
图 5 MIG IP 核结构框图
使用这个 IP 核，用户将可以进行 DDR4 的读写操作，而不必熟悉 DDR4 具
体的读写控制时序。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-029-image-01.jpg)

## 3.2.1 硬件设计

RFEVM216 开发板的 PL 端有五颗 16bit DDR4 颗粒，组成 64bit 带 ECC 功
能的 DDR4 通道。
图 6 DDR4 硬件原理图

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-030-image-01.jpg)

图 7 DDR4 管脚分配硬件原理图

## 3.2.2 硬件工程搭建

1. 打开 Vivado 软件
2. 选择 Create Project

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-031-image-01.jpg)

3. 点击 Next
4. 设置工程名称（rfevm216_pl_ddr4）和位置（E:/rfevm216/），点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-032-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-032-image-02.jpg)

5. 选择 RTL 工程，点击 Next
6. 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-033-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-033-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-033-image-03.jpg)

7. 点击 Finish
8. 在 Flow Navigator 窗口，点击 IP Catalog
9. 选择 DDR4 SDRAM(MIG)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-034-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-034-image-02.jpg)

10. 在 Basic 选项卡下，进行如下设置

 Memory Device Interface Speed(ps):750
 Reference Input Clock Speed(ps):8000(125MHz)
 Memory Part:MT40A512M16LY-075
 Data Width:72
 ECC：Enable
其它设置保持默认，点击 OK

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-035-image-01.jpg)

11. 点击 Generate

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-036-image-01.jpg)

12. 等待直到 ddr4_0_synth_1 出现复选标记
13. 添加源代码 Add Sources，选择 Add or create design sources，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-037-image-01.jpg)

14. 点击 Add Files
15. 选择测试文件，点击 Finish

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-038-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-038-image-02.jpg)

16. 点击 IP Catalog

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-039-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-039-image-02.jpg)

17. 添加 ILA(Integrated Logic Analyzer) IP，配置如下

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-040-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-040-image-02.jpg)

18. 点击 Generate

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-041-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-042-image-01.jpg)

19. 点击 Add Sources，选择 Add or create constraints 添加约束文件，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-043-image-01.jpg)

20. 点击 Create Files
21. 设置 xdc 文件的名称，点击 OK

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-044-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-044-image-02.jpg)

22. 添加 DDR4 的管脚约束
23. 点击 Generate Bitstream，生成 bit

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-045-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-045-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-046-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-046-image-02.jpg)

## 3.2.3 下载验证

1. 点击 Open Hardware Manager->Open Target->Auto Connect

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-047-image-01.jpg)

2. 点击 Program device

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-048-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-048-image-02.jpg)

3. 默认即可，点击 Program
4. 下载完成后，会在 MIG_1 窗口会显示 DDR4 校准的信息和校准状态（CAL

PASS）

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-049-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-049-image-02.jpg)

在 hw_ila_0 窗口中可以查看调试信号

## 3.2.3 参考文档

 Zynq UltraScale Memory

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-050-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-050-image-02.jpg)

UltraScale FPGA Memory Interface Solutions Product Guide - PG150
https://docs.xilinx.com/v/u/en-US/pg150-ultrascale-memory-ip
 Vivado Programming and Debugging
Vivado Design Suit Programming and Debugging User Guide - UG908
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/
Introduction
 ILA
Integrated Logic Analyzer Product Guide - PG172
https://docs.xilinx.com/v/u/en-US/pg172-ila
 DDR4-MT40A512M16
https://pdf1.alldatasheet.com/datasheet-pdf/view/928163/MICRON/MT40A512
M16.html
