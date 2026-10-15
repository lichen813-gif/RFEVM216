# 5.4 AXI-DMA 环回测试

[Switch to English](../../../en/fpga-tutorial/05-ps-pl-interconnect/04-axi-dma-loopback.md)

[返回章节总览](index.md)

AXI DMA 提供系统内存和基于总线 AXI4-Stream 目标外设之间的高带宽直
接内存访问。
在系统中，AXI DMA 与处理器等其它设备通过 AXI Interconnect 互联。系
统处理器通过 AXI4-Lite 接口访问 DMA 内部寄存器，向其写入配置信息，然后
根据配置信息，高效的进行数据传输；DMA 也可以启动 S/G 传输模式，通过独
立的 AXI S/G 通道从 DDR 中获取描述符，然后协调外设与内存间的数据传输。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-204-image-01.jpg)

AXI DMA 用到了三种总线：
 AXI-Lite 用于对寄存器进行配置
 AXI4 Memory Map 用于与内存交互，又分为 AXI4 Memory Map Read 和 AXI4
Memory Map Write 两个接口，一个是读，一个是写。
 AXI4 Stream 接口用于对外设的读写，其中 AXI4 Stream Master（MM2S）用
于对外设写，AXI4 Stream Salve（S2MM）用于对外设读。
AXI DMA 提供了 3 中模式，分别是 Direct Register 模式、Scatter/Gather 模
式和 Cyclic DMA 模式 ， 这里我们的介绍下常用的 Direct Register 模式和
Scatter/Gather 模式 。 Direct Register DMA 模式也就是 Simple DMA 。 Direct
Register 模式提供了一种配置，用于在 MM2S 和 S2MM 通道上执行简单的
DMA 传输，这需要更少的 FPGA 资源。Simple DMA 允许应用程序在 DMA 和
Device 之间定义单个事务。它有两个通道：一个从 DMA 到 Device，另一个从
Device 到 DMA。应用程序必须设置缓冲区地址和长度字段以启动相应通道中
的传输。Scatter/Gather DMA 模式允许在单个 DMA 事务中将数据传输到多个存
储区域或从多个存储区域传输数据。它相当于将多个 Simple DMA 请求链接在

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-205-image-01.jpg)

一起。SGDMA 允许应用程序在内存中定义事务列表，硬件将在应用程序没有进
一步干预的情况下处理这些事务。在此期间，应用程序可以继续添加更多工作以
保持硬件工作。用户可以通过轮询或中断来检查事务是否完成。SGDMA 处理整
个数据包（被定义为表示消息的一系列数据字节）并允许将数据包分解为一个或
多个事务。
本章中使用直接寄存器 Direct Register 模式，采用 Vitis 给的 DMA 例子，稍
作修改，在 DMA 工作结束后，发出结束中断，通知 CPU，使 CPU 读取内存数
据。

## 5.4.1 硬件工程搭建

这里我们依然在上篇 IPI 的工程基础上，去搭建硬件工程。

1. 我们按照之前 IPI 的工程去搭建本实验的硬件工程；
2. 双击 mpsoc，使能 HPM0、HP0、PL to PS 中断，点击【OK】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-206-image-01.jpg)

3. 点击“+”，添加 AXI DMA 模块；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-207-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-207-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-208-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-208-image-02.jpg)

4. 设置 axi dma IP 参数
5. 添加 AXI Stream Data FIFO 模块；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-209-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-209-image-02.jpg)

6. 参数设置如下所示

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-210-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-210-image-02.jpg)

7. 添加 ila 模块，并点击自动连接

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-211-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-211-image-02.jpg)

8. 创建 HDL Wrapper，并生成 bitstream；
9. 导出硬件 xsa 文件

点击【Next】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-212-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-212-image-02.jpg)

选择包含 bit，点击【Next】
设置名称和导出路径，点击【Next】
点击【Finish】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-213-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-213-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-213-image-03.jpg)

## 5.4.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录，点击【Launch】
2. 选择创建硬件平台

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-214-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-214-image-02.jpg)

设置名称，点击【Next】
点击【Browse】，选择生成的 xsa 文件；
点击【Finish】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-215-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-215-image-02.jpg)

3. 编译硬件平台
4. 点击【Import Example】导入 axi dma 的参考示例

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-216-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-216-image-02.jpg)

5. 选择 simple_poll 示例
6. 对示例源文件进行修改：设置 MAX_PKT_LEN,就是长度，单位为字节，

TEST_START_VALUE 为起始的数据值，NUMBER_OF_TRANSFERS 为测
试次数；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-217-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-217-image-02.jpg)

打开 S2MM 的 IOC 中断，关闭 MM2S 的所有中断。在 S2MM 接收完数据后会
发出中断。
打开 MM2S 通路和 S2MM 通路

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-218-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-218-image-02.jpg)

## 5.4.3 下载验证

1. 我们在 vitis 里面 debug，应用程序。
2. 等待 bit 下载完成之后，在 vivado 中打开 ila，设置触发条件
3. 在 vitis 的 Debug 界面，不用设置断点，点击 Resume
4. 此时可以看到 ila 已经触发，可以观察采集到的数据。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-219-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-219-image-02.jpg)

在串口调试工具中，可以看到打印信息

5. 我们也可以在 vitis 调试中，设置断点，观察 memory 信息；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-220-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-220-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-220-image-03.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-221-image-01.jpg)
