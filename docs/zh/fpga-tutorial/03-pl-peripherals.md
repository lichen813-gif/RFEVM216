# 3. PL 端外设

[Switch to English](../../en/fpga-tutorial/03-pl-peripherals.md)

## 3.1 LED 呼吸灯实验

呼吸灯是在微处理器的控制下，由暗渐渐、亮、然后再由亮渐暗，模仿人呼
吸方式方式的 LED 灯。
FPGA 的引脚电平只有“0”和“1”两个等级，因此通过改变引脚单位时间
内高电平的输出时间来实现呼吸灯，也就是让 FPGA 引脚输出一系列 PWM 波信
号并不断改变 PWM 波的占空比来控制 LED 灯亮度的变化。
PWM 占空比调节示意图如下图所示：
图 3 呼吸灯 PWM 占空比示意图

### 3.1.1 硬件设计

RFEVM216 开发板上有 4 个用户可可控制的 LED 灯。其原理图如下图所示：

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-011-image-01.jpg)

图 4 LED 灯硬件原理图

### 3.1.2 硬件工程搭建

1. 在 PC 端，打开 Vivado
2. 点击 Create Project

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-012-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-012-image-02.jpg)

3. 点击 Next
4. 设定工程名称和位置，点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-013-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-013-image-02.jpg)

5. 点击 Next
6. 选择 FPGA 型号 xczu49dr-fsvf1760-2-i，点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-014-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-014-image-02.jpg)

7. 点击 Finish

这里我们能看到建立的工程

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-015-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-015-image-02.jpg)

8. 在 Flow Navigator 窗口，点击 Add Source
9. 选中添加设计文件，点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-016-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-016-image-02.jpg)

10. 点击 Create Files
11. 设置名称，点击 OK

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-017-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-017-image-02.jpg)

12. 点击 Finish
13. 暂时不添加端口，点击 OK

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-018-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-018-image-02.jpg)

点击 Yes

14. 完成后，可以看到我们新创建的.v 文件

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-019-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-019-image-02.jpg)

15. 双击 breath_led，然后输入以下代码

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-020-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-020-image-02.jpg)

16. 点击 Add Source

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-021-image-01.jpg)

17. 选择添加或创建约束文件，点击 Next
18. 点击 Create File

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-022-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-022-image-02.jpg)

19. 设置名称，点击 OK
20. 点击 Finish

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-023-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-023-image-02.jpg)

21. 这里可以看到新创建的约束文件

双击 rfevm_led.xdc，输入以下约束：

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-024-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-024-image-02.jpg)

22. 在 Flow Navigator，点击 Generate Bitstream
23. 点击 OK，等待生成 bit

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-025-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-025-image-02.jpg)

24. 生成 bit 完成之后，选择【View Reports】，点击 OK

### 3.1.3 下载验证

用 USB 转 Type-C 线缆，一端连接板卡，一端连到 PC 上，然后给板卡上电。
在 Vivado 界面，点击 Open Hardware Manager->Open Target->Auto Connect

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-026-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-026-image-02.jpg)

在器件上，右键选择 Program device

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-027-image-01.jpg)

点击 Program
下载完成后，可以看到底板上的 LEDs 灯由暗慢慢变量，再由亮慢慢变暗，
即出现“呼吸”的效果。

## 3.2 PL 端 DDR4 读写实验

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-028-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-028-image-02.jpg)

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

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-029-image-01.jpg)

### 3.2.1 硬件设计

RFEVM216 开发板的 PL 端有五颗 16bit DDR4 颗粒，组成 64bit 带 ECC 功
能的 DDR4 通道。
图 6 DDR4 硬件原理图

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-030-image-01.jpg)

图 7 DDR4 管脚分配硬件原理图

### 3.2.2 硬件工程搭建

1. 打开 Vivado 软件
2. 选择 Create Project

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-031-image-01.jpg)

3. 点击 Next
4. 设置工程名称（rfevm216_pl_ddr4）和位置（E:/rfevm216/），点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-032-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-032-image-02.jpg)

5. 选择 RTL 工程，点击 Next
6. 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-033-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-033-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-033-image-03.jpg)

7. 点击 Finish
8. 在 Flow Navigator 窗口，点击 IP Catalog
9. 选择 DDR4 SDRAM(MIG)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-034-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-034-image-02.jpg)

10. 在 Basic 选项卡下，进行如下设置

 Memory Device Interface Speed(ps):750
 Reference Input Clock Speed(ps):8000(125MHz)
 Memory Part:MT40A512M16LY-075
 Data Width:72
 ECC：Enable
其它设置保持默认，点击 OK

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-035-image-01.jpg)

11. 点击 Generate

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-036-image-01.jpg)

12. 等待直到 ddr4_0_synth_1 出现复选标记
13. 添加源代码 Add Sources，选择 Add or create design sources，点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-037-image-01.jpg)

14. 点击 Add Files
15. 选择测试文件，点击 Finish

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-038-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-038-image-02.jpg)

16. 点击 IP Catalog

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-039-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-039-image-02.jpg)

17. 添加 ILA(Integrated Logic Analyzer) IP，配置如下

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-040-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-040-image-02.jpg)

18. 点击 Generate

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-041-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-042-image-01.jpg)

19. 点击 Add Sources，选择 Add or create constraints 添加约束文件，点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-043-image-01.jpg)

20. 点击 Create Files
21. 设置 xdc 文件的名称，点击 OK

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-044-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-044-image-02.jpg)

22. 添加 DDR4 的管脚约束
23. 点击 Generate Bitstream，生成 bit

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-045-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-045-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-046-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-046-image-02.jpg)

### 3.2.3 下载验证

1. 点击 Open Hardware Manager->Open Target->Auto Connect

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-047-image-01.jpg)

2. 点击 Program device

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-048-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-048-image-02.jpg)

3. 默认即可，点击 Program
4. 下载完成后，会在 MIG_1 窗口会显示 DDR4 校准的信息和校准状态（CAL

PASS）

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-049-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-049-image-02.jpg)

在 hw_ila_0 窗口中可以查看调试信号

### 3.2.3 参考文档

 Zynq UltraScale Memory

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-050-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-050-image-02.jpg)

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

## 3.3 GTY 收发器误码率测试 IBERT 实验

IBERT（集成式比特误码率测试仪）是 Xilinx 面向 UltraScaleTM/UltraScale+TM
架构 GTY 收发器专门设计的，用于评估和监控 GTY 收发器。IBERT 包括采用
FPGA 逻辑实现的模式生成器和检查器，并能够接入 GTY 收发器的端口和动态
重配置端口属性。还包括了通信逻辑，可通过 JTAG 在运行时进行访问。
IBERT 工具用于对 Xilinx FPGA 芯片的高速串行收发器进行板级硬件测试。
通过 IBERT 可以获取误码率，观察眼图，调节串行收发器的参数，从而有助于
判断可能存在的问题，便于验证硬件的稳定性和信号完整性。

### 3.3.1 硬件介绍

使用 IBERT 测试误码率和眼图必须有个收发环通的硬件，开发板上有两路
QSFP28 光纤接口。本实验可以将两路 QSFP28 光纤接口通过 100G 光纤连接起
来形成收发环通链路。
图 8 QSFP 硬件原理图

### 3.3.2 硬件工程搭建

1. 打开 vivado
2. 选择 Create Project

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-052-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-052-image-02.jpg)

3. 点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-053-image-01.jpg)

4. 设置工程名称（ibert_bank_all）和位置（E:/rfevm216/），点击 Next
5. 选择 RTL 工程，点击 Next

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-054-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-054-image-02.jpg)

6. 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next
7. 点击 Finish

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-055-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-055-image-02.jpg)

8. 点击 IP Catalog

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-056-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-056-image-02.jpg)

9. 选择 IBERT UltraScale GTY

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-057-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-057-image-02.jpg)

10. 双击 IBERT UltraScale GTY
11. 设置模块名称：ibert_bank_all

 在“Protocol Definition”选项卡下
Protocol Custom 1: LineRate 25, Refclk:156.25, Quad Count:2
 在“Protocol Selection”选项卡下
QUAD_130: Custom 1/25 Gbps, MGTREFCLK1 130
QUAD_131: Custom 1/25 Gbps, MGTREFCLK1 131
 在“Clock Settings”选项卡下，设置时钟

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-058-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-058-image-02.jpg)

 查看摘要，并点击“OK”

12. 点击“Skip”

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-059-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-059-image-02.jpg)

 生成的 IBERT IP 出现在 Design Sources

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-060-image-01.jpg)

13. 右键 ibert_bank_all，选择 Open IP Example Design ...

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-061-image-01.jpg)

14. 选择位置并点击 OK
15. 创建一个新的工程

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-062-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-062-image-02.jpg)

16. 点击 Generate Bitstream
17. 点击【OK】，等待生成 bit

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-063-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-063-image-02.jpg)

18. 生成 bit 完成之后，选择【View Reports】，点击 OK

### 3.3.3 下载验证

1. 点击 Open Hardware Manager->Open Target->Auto Connect

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-064-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-064-image-02.jpg)

2. 选择 Program device
3. Bitstream file 和 LTX 文件默认，点击 Program

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-065-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-065-image-02.jpg)

4. 点击 Create links
5. 依次选择 MGTX0Y12~MGTX0Y19，点击添加按钮，然后点击 OK

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-066-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-066-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-067-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-068-image-01.jpg)

6. Links 会出现在 Serial I/O Links 选项卡下
7. 点击 BERT Reset，复位 link error 计数器，links 显示 no errors

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-069-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-069-image-02.jpg)

### 3.3.4 参考文档

 IBERT IP
IBERT for UltraScale GTY Transceivers - PG196
https://docs.xilinx.com/v/u/en-US/pg196-ibert-ultrascale-gty
 Vivado Programming and Debugging
Vivado Design Suit Programming and Debugging User Guide - UG908
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/
Introduction

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-070-image-01.jpg)
