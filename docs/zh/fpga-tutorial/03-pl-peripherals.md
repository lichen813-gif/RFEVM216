# 3. PL 端外设

[Switch to English](../../en/fpga-tutorial/03-pl-peripherals.md)

> 本章内容来自中文原始 PDF。图示和软件界面截图保留原标签，以便与硬件和软件实际界面对应。  
> Source PDF: `RFEVM216开发平台FPGA教程.pdf`  
> Source pages: 11-70

<a id="page-11"></a>
## 原 PDF 第 11 页

9 / 223  
3 PL 端外设  
3.1 LED 呼吸灯实验  
呼吸灯是在微处理器的控制下，由暗渐渐、亮、然后再由亮渐暗，模仿人呼  
吸方式方式的 LED 灯。  
FPGA 的引脚电平只有“0”和“1”两个等级，因此通过改变引脚单位时间  
内高电平的输出时间来实现呼吸灯，也就是让 FPGA 引脚输出一系列 PWM 波信  
号并不断改变 PWM 波的占空比来控制 LED 灯亮度的变化。  
PWM 占空比调节示意图如下图所示：  
图 3 呼吸灯 PWM 占空比示意图  
3.1.1 硬件设计  
RFEVM216 开发板上有 4 个用户可可控制的 LED 灯。其原理图如下图所示：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 11, figure 1](../../assets/fpga-tutorial/page-011-image-01.jpg)

---

<a id="page-12"></a>
## 原 PDF 第 12 页

10 / 223  
图 4 LED 灯硬件原理图  
3.1.2 硬件工程搭建  
1) 在 PC 端，打开 Vivado  
2) 点击 Create Project

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 12, figure 1](../../assets/fpga-tutorial/page-012-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 12, figure 2](../../assets/fpga-tutorial/page-012-image-02.jpg)

---

<a id="page-13"></a>
## 原 PDF 第 13 页

11 / 223  
3) 点击 Next  
4) 设定工程名称和位置，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 13, figure 1](../../assets/fpga-tutorial/page-013-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 13, figure 2](../../assets/fpga-tutorial/page-013-image-02.jpg)

---

<a id="page-14"></a>
## 原 PDF 第 14 页

12 / 223  
5) 点击 Next  
6) 选择 FPGA 型号 xczu49dr-fsvf1760-2-i，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 14, figure 1](../../assets/fpga-tutorial/page-014-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 14, figure 2](../../assets/fpga-tutorial/page-014-image-02.jpg)

---

<a id="page-15"></a>
## 原 PDF 第 15 页

13 / 223  
7) 点击 Finish  
这里我们能看到建立的工程

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 15, figure 1](../../assets/fpga-tutorial/page-015-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 15, figure 2](../../assets/fpga-tutorial/page-015-image-02.jpg)

---

<a id="page-16"></a>
## 原 PDF 第 16 页

14 / 223  
8) 在 Flow Navigator 窗口，点击 Add Source  
9) 选中添加设计文件，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 16, figure 1](../../assets/fpga-tutorial/page-016-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 16, figure 2](../../assets/fpga-tutorial/page-016-image-02.jpg)

---

<a id="page-17"></a>
## 原 PDF 第 17 页

15 / 223  
10) 点击 Create Files  
11) 设置名称，点击 OK

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 17, figure 1](../../assets/fpga-tutorial/page-017-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 17, figure 2](../../assets/fpga-tutorial/page-017-image-02.jpg)

---

<a id="page-18"></a>
## 原 PDF 第 18 页

16 / 223  
12) 点击 Finish  
13) 暂时不添加端口，点击 OK

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 18, figure 1](../../assets/fpga-tutorial/page-018-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 18, figure 2](../../assets/fpga-tutorial/page-018-image-02.jpg)

---

<a id="page-19"></a>
## 原 PDF 第 19 页

17 / 223  
点击 Yes  
14) 完成后，可以看到我们新创建的.v 文件

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 19, figure 1](../../assets/fpga-tutorial/page-019-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 19, figure 2](../../assets/fpga-tutorial/page-019-image-02.jpg)

---

<a id="page-20"></a>
## 原 PDF 第 20 页

18 / 223  
15) 双击 breath_led，然后输入以下代码

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 20, figure 1](../../assets/fpga-tutorial/page-020-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 20, figure 2](../../assets/fpga-tutorial/page-020-image-02.jpg)

---

<a id="page-21"></a>
## 原 PDF 第 21 页

19 / 223  
16) 点击 Add Source

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 21, figure 1](../../assets/fpga-tutorial/page-021-image-01.jpg)

---

<a id="page-22"></a>
## 原 PDF 第 22 页

20 / 223  
17) 选择添加或创建约束文件，点击 Next  
18) 点击 Create File

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 22, figure 1](../../assets/fpga-tutorial/page-022-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 22, figure 2](../../assets/fpga-tutorial/page-022-image-02.jpg)

---

<a id="page-23"></a>
## 原 PDF 第 23 页

21 / 223  
19) 设置名称，点击 OK  
20) 点击 Finish

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 23, figure 1](../../assets/fpga-tutorial/page-023-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 23, figure 2](../../assets/fpga-tutorial/page-023-image-02.jpg)

---

<a id="page-24"></a>
## 原 PDF 第 24 页

22 / 223  
21) 这里可以看到新创建的约束文件  
双击 rfevm_led.xdc，输入以下约束：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 24, figure 1](../../assets/fpga-tutorial/page-024-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 24, figure 2](../../assets/fpga-tutorial/page-024-image-02.jpg)

---

<a id="page-25"></a>
## 原 PDF 第 25 页

23 / 223  
22) 在 Flow Navigator，点击 Generate Bitstream  
23) 点击 OK，等待生成 bit

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 25, figure 1](../../assets/fpga-tutorial/page-025-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 25, figure 2](../../assets/fpga-tutorial/page-025-image-02.jpg)

---

<a id="page-26"></a>
## 原 PDF 第 26 页

24 / 223  
24) 生成 bit 完成之后，选择【View Reports】，点击 OK  
3.1.3 下载验证  
用 USB 转 Type-C 线缆，一端连接板卡，一端连到 PC 上，然后给板卡上电。  
在 Vivado 界面，点击 Open Hardware Manager->Open Target->Auto Connect

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 26, figure 1](../../assets/fpga-tutorial/page-026-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 26, figure 2](../../assets/fpga-tutorial/page-026-image-02.jpg)

---

<a id="page-27"></a>
## 原 PDF 第 27 页

25 / 223  
在器件上，右键选择 Program device

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 27, figure 1](../../assets/fpga-tutorial/page-027-image-01.jpg)

---

<a id="page-28"></a>
## 原 PDF 第 28 页

26 / 223  
点击 Program  
下载完成后，可以看到底板上的 LEDs 灯由暗慢慢变量，再由亮慢慢变暗，  
即出现“呼吸”的效果。  
3.2 PL 端 DDR4 读写实验

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 28, figure 1](../../assets/fpga-tutorial/page-028-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 28, figure 2](../../assets/fpga-tutorial/page-028-image-02.jpg)

---

<a id="page-29"></a>
## 原 PDF 第 29 页

27 / 223  
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

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 29, figure 1](../../assets/fpga-tutorial/page-029-image-01.jpg)

---

<a id="page-30"></a>
## 原 PDF 第 30 页

28 / 223  
3.2.1 硬件设计  
RFEVM216 开发板的 PL 端有五颗 16bit DDR4 颗粒，组成 64bit 带 ECC 功  
能的 DDR4 通道。  
图 6 DDR4 硬件原理图

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 30, figure 1](../../assets/fpga-tutorial/page-030-image-01.jpg)

---

<a id="page-31"></a>
## 原 PDF 第 31 页

29 / 223  
图 7 DDR4 管脚分配硬件原理图  
3.2.2 硬件工程搭建  
1) 打开 Vivado 软件  
2) 选择 Create Project

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 31, figure 1](../../assets/fpga-tutorial/page-031-image-01.jpg)

---

<a id="page-32"></a>
## 原 PDF 第 32 页

30 / 223  
3) 点击 Next  
4) 设置工程名称（rfevm216_pl_ddr4）和位置（E:/rfevm216/），点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 32, figure 1](../../assets/fpga-tutorial/page-032-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 32, figure 2](../../assets/fpga-tutorial/page-032-image-02.jpg)

---

<a id="page-33"></a>
## 原 PDF 第 33 页

31 / 223  
5) 选择 RTL 工程，点击 Next  
6) 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 33, figure 1](../../assets/fpga-tutorial/page-033-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 33, figure 2](../../assets/fpga-tutorial/page-033-image-02.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 33, figure 3](../../assets/fpga-tutorial/page-033-image-03.jpg)

---

<a id="page-34"></a>
## 原 PDF 第 34 页

32 / 223  
7) 点击 Finish  
8) 在 Flow Navigator 窗口，点击 IP Catalog  
9) 选择 DDR4 SDRAM(MIG)

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 34, figure 1](../../assets/fpga-tutorial/page-034-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 34, figure 2](../../assets/fpga-tutorial/page-034-image-02.jpg)

---

<a id="page-35"></a>
## 原 PDF 第 35 页

33 / 223  
10) 在 Basic 选项卡下，进行如下设置  
 Memory Device Interface Speed(ps):750  
 Reference Input Clock Speed(ps):8000(125MHz)  
 Memory Part:MT40A512M16LY-075  
 Data Width:72  
 ECC：Enable  
其它设置保持默认，点击 OK

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 35, figure 1](../../assets/fpga-tutorial/page-035-image-01.jpg)

---

<a id="page-36"></a>
## 原 PDF 第 36 页

34 / 223  
11) 点击 Generate

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 36, figure 1](../../assets/fpga-tutorial/page-036-image-01.jpg)

---

<a id="page-37"></a>
## 原 PDF 第 37 页

35 / 223  
12) 等待直到 ddr4_0_synth_1 出现复选标记  
13) 添加源代码 Add Sources，选择 Add or create design sources，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 37, figure 1](../../assets/fpga-tutorial/page-037-image-01.jpg)

---

<a id="page-38"></a>
## 原 PDF 第 38 页

36 / 223  
14) 点击 Add Files  
15) 选择测试文件，点击 Finish

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 38, figure 1](../../assets/fpga-tutorial/page-038-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 38, figure 2](../../assets/fpga-tutorial/page-038-image-02.jpg)

---

<a id="page-39"></a>
## 原 PDF 第 39 页

37 / 223  
16) 点击 IP Catalog

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 39, figure 1](../../assets/fpga-tutorial/page-039-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 39, figure 2](../../assets/fpga-tutorial/page-039-image-02.jpg)

---

<a id="page-40"></a>
## 原 PDF 第 40 页

38 / 223  
17) 添加 ILA(Integrated Logic Analyzer) IP，配置如下

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 40, figure 1](../../assets/fpga-tutorial/page-040-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 40, figure 2](../../assets/fpga-tutorial/page-040-image-02.jpg)

---

<a id="page-41"></a>
## 原 PDF 第 41 页

39 / 223  
18) 点击 Generate

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 41, figure 1](../../assets/fpga-tutorial/page-041-image-01.jpg)

---

<a id="page-42"></a>
## 原 PDF 第 42 页

40 / 223

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 42, figure 1](../../assets/fpga-tutorial/page-042-image-01.jpg)

---

<a id="page-43"></a>
## 原 PDF 第 43 页

41 / 223  
19) 点击 Add Sources，选择 Add or create constraints 添加约束文件，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 43, figure 1](../../assets/fpga-tutorial/page-043-image-01.jpg)

---

<a id="page-44"></a>
## 原 PDF 第 44 页

42 / 223  
20) 点击 Create Files  
21) 设置 xdc 文件的名称，点击 OK

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 44, figure 1](../../assets/fpga-tutorial/page-044-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 44, figure 2](../../assets/fpga-tutorial/page-044-image-02.jpg)

---

<a id="page-45"></a>
## 原 PDF 第 45 页

43 / 223  
22) 添加 DDR4 的管脚约束  
23) 点击 Generate Bitstream，生成 bit

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 45, figure 1](../../assets/fpga-tutorial/page-045-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 45, figure 2](../../assets/fpga-tutorial/page-045-image-02.jpg)

---

<a id="page-46"></a>
## 原 PDF 第 46 页

44 / 223

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 46, figure 1](../../assets/fpga-tutorial/page-046-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 46, figure 2](../../assets/fpga-tutorial/page-046-image-02.jpg)

---

<a id="page-47"></a>
## 原 PDF 第 47 页

45 / 223  
3.2.3 下载验证  
1) 点击 Open Hardware Manager->Open Target->Auto Connect

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 47, figure 1](../../assets/fpga-tutorial/page-047-image-01.jpg)

---

<a id="page-48"></a>
## 原 PDF 第 48 页

46 / 223  
2) 点击 Program device

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 48, figure 1](../../assets/fpga-tutorial/page-048-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 48, figure 2](../../assets/fpga-tutorial/page-048-image-02.jpg)

---

<a id="page-49"></a>
## 原 PDF 第 49 页

47 / 223  
3) 默认即可，点击 Program  
4) 下载完成后，会在 MIG_1 窗口会显示 DDR4 校准的信息和校准状态（CAL  
PASS）

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 49, figure 1](../../assets/fpga-tutorial/page-049-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 49, figure 2](../../assets/fpga-tutorial/page-049-image-02.jpg)

---

<a id="page-50"></a>
## 原 PDF 第 50 页

48 / 223  
在 hw_ila_0 窗口中可以查看调试信号  
3.2.3 参考文档  
 Zynq UltraScale Memory

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 50, figure 1](../../assets/fpga-tutorial/page-050-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 50, figure 2](../../assets/fpga-tutorial/page-050-image-02.jpg)

---

<a id="page-51"></a>
## 原 PDF 第 51 页

49 / 223  
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
3.3 GTY 收发器误码率测试 IBERT 实验  
IBERT（集成式比特误码率测试仪）是 Xilinx 面向 UltraScaleTM/UltraScale+TM  
架构 GTY 收发器专门设计的，用于评估和监控 GTY 收发器。IBERT 包括采用  
FPGA 逻辑实现的模式生成器和检查器，并能够接入 GTY 收发器的端口和动态  
重配置端口属性。还包括了通信逻辑，可通过 JTAG 在运行时进行访问。  
IBERT 工具用于对 Xilinx FPGA 芯片的高速串行收发器进行板级硬件测试。  
通过 IBERT 可以获取误码率，观察眼图，调节串行收发器的参数，从而有助于  
判断可能存在的问题，便于验证硬件的稳定性和信号完整性。  
3.3.1 硬件介绍  
使用 IBERT 测试误码率和眼图必须有个收发环通的硬件，开发板上有两路  
QSFP28 光纤接口。本实验可以将两路 QSFP28 光纤接口通过 100G 光纤连接起  
来形成收发环通链路。

---

<a id="page-52"></a>
## 原 PDF 第 52 页

50 / 223  
图 8 QSFP 硬件原理图  
3.3.2 硬件工程搭建  
1) 打开 vivado  
2) 选择 Create Project

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 52, figure 1](../../assets/fpga-tutorial/page-052-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 52, figure 2](../../assets/fpga-tutorial/page-052-image-02.jpg)

---

<a id="page-53"></a>
## 原 PDF 第 53 页

51 / 223  
3) 点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 53, figure 1](../../assets/fpga-tutorial/page-053-image-01.jpg)

---

<a id="page-54"></a>
## 原 PDF 第 54 页

52 / 223  
4) 设置工程名称（ibert_bank_all）和位置（E:/rfevm216/），点击 Next  
5) 选择 RTL 工程，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 54, figure 1](../../assets/fpga-tutorial/page-054-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 54, figure 2](../../assets/fpga-tutorial/page-054-image-02.jpg)

---

<a id="page-55"></a>
## 原 PDF 第 55 页

53 / 223  
6) 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next  
7) 点击 Finish

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 55, figure 1](../../assets/fpga-tutorial/page-055-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 55, figure 2](../../assets/fpga-tutorial/page-055-image-02.jpg)

---

<a id="page-56"></a>
## 原 PDF 第 56 页

54 / 223  
8) 点击 IP Catalog

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 56, figure 1](../../assets/fpga-tutorial/page-056-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 56, figure 2](../../assets/fpga-tutorial/page-056-image-02.jpg)

---

<a id="page-57"></a>
## 原 PDF 第 57 页

55 / 223  
9) 选择 IBERT UltraScale GTY

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 57, figure 1](../../assets/fpga-tutorial/page-057-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 57, figure 2](../../assets/fpga-tutorial/page-057-image-02.jpg)

---

<a id="page-58"></a>
## 原 PDF 第 58 页

56 / 223  
10) 双击 IBERT UltraScale GTY  
11) 设置模块名称：ibert_bank_all  
 在“Protocol Definition”选项卡下  
Protocol Custom 1: LineRate 25, Refclk:156.25, Quad Count:2  
 在“Protocol Selection”选项卡下  
QUAD_130: Custom 1/25 Gbps, MGTREFCLK1 130  
QUAD_131: Custom 1/25 Gbps, MGTREFCLK1 131  
 在“Clock Settings”选项卡下，设置时钟

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 58, figure 1](../../assets/fpga-tutorial/page-058-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 58, figure 2](../../assets/fpga-tutorial/page-058-image-02.jpg)

---

<a id="page-59"></a>
## 原 PDF 第 59 页

57 / 223  
 查看摘要，并点击“OK”  
12) 点击“Skip”

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 59, figure 1](../../assets/fpga-tutorial/page-059-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 59, figure 2](../../assets/fpga-tutorial/page-059-image-02.jpg)

---

<a id="page-60"></a>
## 原 PDF 第 60 页

58 / 223  
 生成的 IBERT IP 出现在 Design Sources

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 60, figure 1](../../assets/fpga-tutorial/page-060-image-01.jpg)

---

<a id="page-61"></a>
## 原 PDF 第 61 页

59 / 223  
13) 右键 ibert_bank_all，选择 Open IP Example Design ...

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 61, figure 1](../../assets/fpga-tutorial/page-061-image-01.jpg)

---

<a id="page-62"></a>
## 原 PDF 第 62 页

60 / 223  
14) 选择位置并点击 OK  
15) 创建一个新的工程

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 62, figure 1](../../assets/fpga-tutorial/page-062-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 62, figure 2](../../assets/fpga-tutorial/page-062-image-02.jpg)

---

<a id="page-63"></a>
## 原 PDF 第 63 页

61 / 223  
16) 点击 Generate Bitstream  
17) 点击【OK】，等待生成 bit

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 63, figure 1](../../assets/fpga-tutorial/page-063-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 63, figure 2](../../assets/fpga-tutorial/page-063-image-02.jpg)

---

<a id="page-64"></a>
## 原 PDF 第 64 页

62 / 223  
18) 生成 bit 完成之后，选择【View Reports】，点击 OK  
3.3.3 下载验证  
1) 点击 Open Hardware Manager->Open Target->Auto Connect

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 64, figure 1](../../assets/fpga-tutorial/page-064-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 64, figure 2](../../assets/fpga-tutorial/page-064-image-02.jpg)

---

<a id="page-65"></a>
## 原 PDF 第 65 页

63 / 223  
2) 选择 Program device  
3) Bitstream file 和 LTX 文件默认，点击 Program

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 65, figure 1](../../assets/fpga-tutorial/page-065-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 65, figure 2](../../assets/fpga-tutorial/page-065-image-02.jpg)

---

<a id="page-66"></a>
## 原 PDF 第 66 页

64 / 223  
4) 点击 Create links  
5) 依次选择 MGTX0Y12~MGTX0Y19，点击添加按钮，然后点击 OK

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 66, figure 1](../../assets/fpga-tutorial/page-066-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 66, figure 2](../../assets/fpga-tutorial/page-066-image-02.jpg)

---

<a id="page-67"></a>
## 原 PDF 第 67 页

65 / 223

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 67, figure 1](../../assets/fpga-tutorial/page-067-image-01.jpg)

---

<a id="page-68"></a>
## 原 PDF 第 68 页

66 / 223

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 68, figure 1](../../assets/fpga-tutorial/page-068-image-01.jpg)

---

<a id="page-69"></a>
## 原 PDF 第 69 页

67 / 223  
6) Links 会出现在 Serial I/O Links 选项卡下  
7) 点击 BERT Reset，复位 link error 计数器，links 显示 no errors

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 69, figure 1](../../assets/fpga-tutorial/page-069-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 69, figure 2](../../assets/fpga-tutorial/page-069-image-02.jpg)

---

<a id="page-70"></a>
## 原 PDF 第 70 页

68 / 223  
3.3.4 参考文档  
 IBERT IP  
IBERT for UltraScale GTY Transceivers - PG196  
https://docs.xilinx.com/v/u/en-US/pg196-ibert-ultrascale-gty  
 Vivado Programming and Debugging  
Vivado Design Suit Programming and Debugging User Guide - UG908  
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/  
Introduction

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 70, figure 1](../../assets/fpga-tutorial/page-070-image-01.jpg)
