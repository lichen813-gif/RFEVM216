# 4.3 PS 端 RTC 中断实验

[Switch to English](../../../en/fpga-tutorial/04-ps-peripherals/03-rtc-interrupt.md)

[返回章节总览](index.md)

RTC（Real Time Clock）实时时钟单元为系统和应用软件提供精确的时间基

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-112-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-112-image-02.jpg)

准。为了满足高精度的需要，RTC 还包括校准电路以抵消温度和电压波动。RTC
由 VCC-PSAUX 或 VCC-PSBATT 电源供电。当辅助电源可用时，RTC 使用它保
持计数器工作。当辅助电源 VCC PSAUX 不可用时，RTC 自动切换到电池电源
VCC PSBATT 电源。
RTC 具有以下特点：

- 既可以使用辅助电源工作也可以使用电池电源工作，当系统掉电时，RTC

会自动切换至电池供电保持持续工作。

- 报警设置和周期性中断（定时中断）。
- 用于高精度计时的复杂校准电路。
- 32 位秒计数器，可计数约 136 年的时间。
- 三个计数器： 32 位秒计数器

16 位滴答计数器，用于测量基于 32KHz 晶振的秒数。
用于校准的 4 位小数计数器
图 11 RTC 控制器结构图

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-113-image-01.jpg)

图 12 RTC 功能图

## 4.3.1 软件设计

1. 登录 Vitis，切换到之前的工作目录，然后双击 platform.spr，选中 Board Support

Package，可以看到 psu_rtc 的文档和导入示例。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-114-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-114-image-02.jpg)

2. 点击 Import Example，会弹出如下图所示的导入示例界面；
3. 这里我们选中第三个官方示例 RTC 中断周期报警的示例

（xrtcpsu_periodic_alarm_interrupt_example），点击 OK

4. 这里我们就导入了 example 工程

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-115-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-115-image-02.jpg)

5. 选中应用工程，右键后选中 Build Project 对工程进行编译

编译进度可以在工具下方的控制台面板（Console）中进行查看，如下图十
所：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-116-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-116-image-02.jpg)

## 4.3.2 下载验证

首先我们将 USB 转 Type-C 线缆的 Type-C 端与 RFEVM2116 开发板上的
JTAG 接口连接，USB 转 Type-C 线缆的另外一端与电脑连接。连接开发板电源，
给开发板上电。
下载程序，右键点击应用工程，选择 Run As->Run Configuration...

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-117-image-01.jpg)

双击 Single Application Debug 一项
选中 Target Setup 标签页，默认配置，点击 Run

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-118-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-118-image-02.jpg)

下载完成后，在串口调试终端可以看到串口的要打印信息：
