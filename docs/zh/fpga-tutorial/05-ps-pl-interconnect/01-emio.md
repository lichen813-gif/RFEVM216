# 5.1 PS 端 EMIO 的使用

[Switch to English](../../../en/fpga-tutorial/05-ps-pl-interconnect/01-emio.md)

[返回章节总览](index.md)

前面介绍了 PL 端 LED 呼吸灯的实验，这里我们使用 PS 端去控制 PL 侧 LED
灯的亮灭。
PL 侧的扩展 IO 也可以用这种方法去控制。
ZYNQ 的 GPIO 分为 MIO（multiplexed I/O）和 EMIO（extended multiplexed
I/O）两种。
MIO 为 PS 端多功能 IO 接口，IO 与 PS 端连接，每个 IO 可根据需求配置为
GPIO、SPI、UART、TIMER、Ethernet、USB 等多种不同功能。由于 MIO 对 PL
端不可见，因此 PL 端无法使用 MIO 引脚。
EMIO 为 MIO 的扩展 IO，IO 与 PL 端连接。由于 EMIO 对 PS 端、PL 端均
可见，因此两者均可使用 EMIO 引脚。一般情况下，如 PS 端 MIO 资源无法满
足需求时，PS 端可通过 EMIO 方式进行接口扩展。EMIO 的使用与 MIO 相似，
区别在于 EMIO 需使用 Vivado 约束文件对管脚进行分配。
MPSoC 为 PL 提供了 96 个 GPIO，通过 EMIO 管脚连接到 PL。这里我们使
用 EMIO 去连接 PL 端的 LED 灯，在 Vitis 里面去控制它的状态。

## 5.1.1 硬件工程搭建

1. 搭建硬件工程，按照上章 IPI 的工程搭建步骤，添加 MPSOC IP 核
2. 双击 IP，使能 emio 接口，IO 数量选择 4（对应底板上 4 个 led 灯）；
3. 这里我们把 emio 的输出 emio_gpio_o 引出来 Make External。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-162-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-162-image-02.jpg)

4. 检查设计是否有误

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-163-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-163-image-02.jpg)

5. 创建 HDL Wrapper...

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-164-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-164-image-02.jpg)

6. 创建约束文件
7. 编译生成 bit 文件

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-165-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-165-image-02.jpg)

8. 编译完成后，导出硬件工程，给后面 vitis 软件开发使用；

这里我们选择包含 bitstream，点击【Next】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-166-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-166-image-02.jpg)

设置 xsa 的名称和路径

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-167-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-167-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-167-image-03.jpg)

点击【Finish】后，可以在工程路径下面看到新生成的 xsa 文件。

## 5.1.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-168-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-168-image-02.jpg)

2. 选择【Create Platform Project】

设置平台名称，点击【Next】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-169-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-169-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-170-image-01.jpg)

这里点击 Browse，选择生成的 xsa 文件

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-171-image-01.jpg)

点击【Finish】，生成硬件平台

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-172-image-01.jpg)

3. 编译 plafform
4. 编译完成之后，新建应用工程

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-173-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-173-image-02.jpg)

点击【Next】
点击【Next】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-174-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-174-image-02.jpg)

设置应用工程名称，并点击【Next】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-175-image-01.jpg)

点击【Next】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-176-image-01.jpg)

选择“Hello World”模板，点击【Finish】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-177-image-01.jpg)

5. 这里，我们修改 hello world 源文件，添加 GPIO 控制代码

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-178-image-01.jpg)

注意：mpsoc 有 78 个 MIO，EMIO 的序号，从 78 开始；

## 5.1.3 下载验证

这里我们在 vitis 里面下载 bit 文件和 elf 文件，下载步骤请参考之前介绍，
可以看到的底板上的四了 led 灯一直闪烁。
