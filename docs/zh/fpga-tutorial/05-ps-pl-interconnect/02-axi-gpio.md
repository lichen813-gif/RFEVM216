# 5.2 PL 端 AXI GPIO 的使用

[Switch to English](../../../en/fpga-tutorial/05-ps-pl-interconnect/02-axi-gpio.md)

[返回章节总览](index.md)

AXI GPIO 是一种特定的 GPIO（通用输入/输出）控制器，它使用 AXI（高
级扩展接口）总线协议进行通信。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-179-image-01.jpg)

AXI GPIO 用于控制和读取 GPIO 引脚的状态。广泛应用于嵌入式系统中，
用于与处理器或其它外设进行通信，以控制和读取 GPIO 引脚的状态。它可以用
于连接各种外设，如 LED、按钮、传感器等，实现与外部环境的交互。
这里我们使用 AXI GPIO 去控制底板上 led 灯的明灭变化。

## 5.2.1 硬件工程搭建

1. 按照上章 IPI 的工程搭建步骤，搭建本实验的硬件工程
2. 在 IPI 界面上，右键添加 AXI GPIO 的 IP 核

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-180-image-01.jpg)

3. 这里我们只使能 GPIO 1，我们只控制 LED 的输出，所以使能全部输出，位

宽 4bit，然后点击【OK】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-181-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-181-image-02.jpg)

4. 我们在 MPSoC 中，使能 LPD 接口，然后点击自动连接【Run Connection

Automation】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-182-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-182-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-183-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-183-image-02.jpg)

5. 检查设计是否有误

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-184-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-184-image-02.jpg)

6. 创建 HDL wrapper，然后生成 bit。
7. 添加 xdc 约束文件，约束 led 的管脚，并生成 bit。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-185-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-185-image-02.jpg)

8. 导出硬件工程 xsa 文件（包含 bit 流）。

## 5.2.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录
2. 创建硬件平台，具体步骤可参考上节；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-186-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-186-image-02.jpg)

3. 在右下角，axi_gpio_0 里面，选 Import Example

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-187-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-187-image-02.jpg)

4. 选择“xgpio_example”
5. 打开源文件

这里我们修改宏定义 LED 的值为 0xF，对应 4 个 led 灯。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-188-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-188-image-02.jpg)

6. 编译应用程序，生成 elf 文件

## 5.2.3 下载验证

这里我们在 vitis 里面下载 bit 文件和 elf 文件，下载步骤请参考之前介绍，

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-189-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-189-image-02.jpg)

下载成功后可以看到的底板上的四了 led 灯一直闪烁。
