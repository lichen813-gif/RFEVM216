# 5. PS 与 PL 互联

[Switch to English](../../en/fpga-tutorial/05-ps-pl-interconnect.md)

本章主要介绍 PS 与 PL 之间的互联，在开始之前，首先简要介绍 PS/PL 之
间的数据通路，具体请参考《ug1085 Zynq UltraScale+ Device Technical Reference
Manual》。
PS/PL 之间的数据通路主要是通用的 AXI Memory 接口，其中 PS 作为主设
备的接口有 128-bit 位宽的 HPM0/HPM1，64-bit 位宽的 LPD_PL；PL 作为主设
备的接口有 ACP/ACE/HPC0/HPC1/HP0/HP1/HP2/HP3。所有 AXI Memory 接口

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-160-image-01.jpg)

的位宽最高都可以支持到 128-bit。
Interface Name Abbreviation
FIFO
Interface
Master
S_AXI_HP{0:3}_FPD HP{0:3} AFI_{2:5} PL
S_AXI_LPD PL_LPD AFI_6 PL
S_AXI_ACE_FPD ACE None PL
S_AXI_ACP_FPD ACP None PL
S_AXI_HPC{0,1}_FPD HPC{0,1} AFI_{0:1} PL
M_AXI_HPM{0,1}_FPD HPM{0,1} None PS
M_AXI_HPM0_LPD LPD_PL None PS
摘自《ug1085》

## 5.1 PS 端 EMIO 的使用

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

### 5.1.1 硬件工程搭建

1. 搭建硬件工程，按照上章 IPI 的工程搭建步骤，添加 MPSOC IP 核
2. 双击 IP，使能 emio 接口，IO 数量选择 4（对应底板上 4 个 led 灯）；
3. 这里我们把 emio 的输出 emio_gpio_o 引出来 Make External。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-162-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-162-image-02.jpg)

4. 检查设计是否有误

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-163-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-163-image-02.jpg)

5. 创建 HDL Wrapper...

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-164-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-164-image-02.jpg)

6. 创建约束文件
7. 编译生成 bit 文件

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-165-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-165-image-02.jpg)

8. 编译完成后，导出硬件工程，给后面 vitis 软件开发使用；

这里我们选择包含 bitstream，点击【Next】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-166-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-166-image-02.jpg)

设置 xsa 的名称和路径

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-167-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-167-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-167-image-03.jpg)

点击【Finish】后，可以在工程路径下面看到新生成的 xsa 文件。

### 5.1.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-168-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-168-image-02.jpg)

2. 选择【Create Platform Project】

设置平台名称，点击【Next】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-169-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-169-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-170-image-01.jpg)

这里点击 Browse，选择生成的 xsa 文件

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-171-image-01.jpg)

点击【Finish】，生成硬件平台

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-172-image-01.jpg)

3. 编译 plafform
4. 编译完成之后，新建应用工程

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-173-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-173-image-02.jpg)

点击【Next】
点击【Next】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-174-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-174-image-02.jpg)

设置应用工程名称，并点击【Next】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-175-image-01.jpg)

点击【Next】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-176-image-01.jpg)

选择“Hello World”模板，点击【Finish】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-177-image-01.jpg)

5. 这里，我们修改 hello world 源文件，添加 GPIO 控制代码

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-178-image-01.jpg)

注意：mpsoc 有 78 个 MIO，EMIO 的序号，从 78 开始；

### 5.1.3 下载验证

这里我们在 vitis 里面下载 bit 文件和 elf 文件，下载步骤请参考之前介绍，
可以看到的底板上的四了 led 灯一直闪烁。

## 5.2 PL 端 AXI GPIO 的使用

AXI GPIO 是一种特定的 GPIO（通用输入/输出）控制器，它使用 AXI（高
级扩展接口）总线协议进行通信。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-179-image-01.jpg)

AXI GPIO 用于控制和读取 GPIO 引脚的状态。广泛应用于嵌入式系统中，
用于与处理器或其它外设进行通信，以控制和读取 GPIO 引脚的状态。它可以用
于连接各种外设，如 LED、按钮、传感器等，实现与外部环境的交互。
这里我们使用 AXI GPIO 去控制底板上 led 灯的明灭变化。

### 5.2.1 硬件工程搭建

1. 按照上章 IPI 的工程搭建步骤，搭建本实验的硬件工程
2. 在 IPI 界面上，右键添加 AXI GPIO 的 IP 核

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-180-image-01.jpg)

3. 这里我们只使能 GPIO 1，我们只控制 LED 的输出，所以使能全部输出，位

宽 4bit，然后点击【OK】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-181-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-181-image-02.jpg)

4. 我们在 MPSoC 中，使能 LPD 接口，然后点击自动连接【Run Connection

Automation】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-182-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-182-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-183-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-183-image-02.jpg)

5. 检查设计是否有误

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-184-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-184-image-02.jpg)

6. 创建 HDL wrapper，然后生成 bit。
7. 添加 xdc 约束文件，约束 led 的管脚，并生成 bit。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-185-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-185-image-02.jpg)

8. 导出硬件工程 xsa 文件（包含 bit 流）。

### 5.2.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录
2. 创建硬件平台，具体步骤可参考上节；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-186-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-186-image-02.jpg)

3. 在右下角，axi_gpio_0 里面，选 Import Example

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-187-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-187-image-02.jpg)

4. 选择“xgpio_example”
5. 打开源文件

这里我们修改宏定义 LED 的值为 0xF，对应 4 个 led 灯。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-188-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-188-image-02.jpg)

6. 编译应用程序，生成 elf 文件

### 5.2.3 下载验证

这里我们在 vitis 里面下载 bit 文件和 elf 文件，下载步骤请参考之前介绍，

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-189-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-189-image-02.jpg)

下载成功后可以看到的底板上的四了 led 灯一直闪烁。

## 5.3 PS 端读写 PL 端的寄存器

很多时候，PS/PL 之间只需要简单的数据通路。PS 只需要下发有限的参数
给 PL，PL 只需要向 PS 反馈有限的状态数据。这种情况下，PL 内部只需要实现
AXI-Lite 接口就可以，PS 通过 AXI 接口去访问寄存器，即向 PL 提供参数，也
可以读回 PL 的状态。

### 5.3.1 硬件工程搭建

这里我们依然在上篇 IPI 的工程基础上，去搭建硬件工程。

1. 我们按照之前 IPI 的工程去搭建本实验的硬件工程；
2. 双击 IP，使能 AXI HPM0 LPD 接口；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-190-image-01.jpg)

3. 我们在工程里面添加 up_axi.v 源文件（up_axi 模块实现了 AXI-Lite 协议，这

是 adi 的开源代码，我们只需要关注和使用用户侧信号即可）

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-191-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-191-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-192-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-192-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-192-image-03.jpg)

4. 添加完成之后，我们在 IPI 界面里面右键，添加模块

选择我们刚添加的 up_axi.v 模块

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-193-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-193-image-02.jpg)

点击【OK】

5. 我们选择自动连接【Run Connection Automation】

点击【OK】

6. 我们引出 up_axi 的用户接口信号和时钟复位信号

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-194-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-194-image-02.jpg)

7. Validate 设计

这里提示以下错误，提示时钟频率不一致
我们选中 up_axi，修改 up_axi 总线的频率，重新 validate 即可；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-195-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-195-image-02.jpg)

8. 我们新建顶层文件，例化 bd 文件，和寄存器读写模块；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-196-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-196-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-196-image-03.jpg)

9. 生成 bit，导出硬件工程 xsa 文件；

### 5.3.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录，点击【Launch】
2. 编译硬件平台
3. 新建应用程序

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-197-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-197-image-02.jpg)

中间部分步骤省略，设置应用程序名称
最后选择“Hello World”模板，点击【Finish】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-198-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-198-image-02.jpg)

4. 修改 helloworld.c 文件，添加寄存器读写代码，我们在硬件工程里面使能了 3

个寄存器，这里我们对这三个寄存器进行读写测试；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-199-image-01.jpg)

5. 编译应用程序

### 5.3.3 下载验证

我们在 vitis 里面 debug，应用程序。

1. 在应用程序上面右键，选择【Debug As】->【Debug configurations...】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-200-image-01.jpg)

2. 这里我们 Step Over 单步运行程序

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-201-image-01.jpg)

同时打开 chipscope，观测寄存器的读写信号，我们分别设置读写请求为触发信
号，然后单步运行 c 程序，查看 chipscope 信号变化

3. 我们在 vitis 里面执行代码，可以看到 ila 里面信号变化

往寄存器偏移地址 0 里面写 0x01020304

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-202-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-202-image-02.jpg)

往寄存器偏移地址 4 里面写 0x05060708
往寄存器偏移地址 8 里面写 0x090a0b0c
从寄存器偏移地址 0 里面读回 0x01020304

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-203-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-203-image-02.jpg)

## 5.4 AXI-DMA 环回测试

AXI DMA 提供系统内存和基于总线 AXI4-Stream 目标外设之间的高带宽直
接内存访问。
在系统中，AXI DMA 与处理器等其它设备通过 AXI Interconnect 互联。系
统处理器通过 AXI4-Lite 接口访问 DMA 内部寄存器，向其写入配置信息，然后
根据配置信息，高效的进行数据传输；DMA 也可以启动 S/G 传输模式，通过独
立的 AXI S/G 通道从 DDR 中获取描述符，然后协调外设与内存间的数据传输。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-204-image-01.jpg)

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

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-205-image-01.jpg)

一起。SGDMA 允许应用程序在内存中定义事务列表，硬件将在应用程序没有进
一步干预的情况下处理这些事务。在此期间，应用程序可以继续添加更多工作以
保持硬件工作。用户可以通过轮询或中断来检查事务是否完成。SGDMA 处理整
个数据包（被定义为表示消息的一系列数据字节）并允许将数据包分解为一个或
多个事务。
本章中使用直接寄存器 Direct Register 模式，采用 Vitis 给的 DMA 例子，稍
作修改，在 DMA 工作结束后，发出结束中断，通知 CPU，使 CPU 读取内存数
据。

### 5.4.1 硬件工程搭建

这里我们依然在上篇 IPI 的工程基础上，去搭建硬件工程。

1. 我们按照之前 IPI 的工程去搭建本实验的硬件工程；
2. 双击 mpsoc，使能 HPM0、HP0、PL to PS 中断，点击【OK】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-206-image-01.jpg)

3. 点击“+”，添加 AXI DMA 模块；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-207-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-207-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-208-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-208-image-02.jpg)

4. 设置 axi dma IP 参数
5. 添加 AXI Stream Data FIFO 模块；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-209-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-209-image-02.jpg)

6. 参数设置如下所示

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-210-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-210-image-02.jpg)

7. 添加 ila 模块，并点击自动连接

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-211-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-211-image-02.jpg)

8. 创建 HDL Wrapper，并生成 bitstream；
9. 导出硬件 xsa 文件

点击【Next】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-212-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-212-image-02.jpg)

选择包含 bit，点击【Next】
设置名称和导出路径，点击【Next】
点击【Finish】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-213-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-213-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-213-image-03.jpg)

### 5.4.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录，点击【Launch】
2. 选择创建硬件平台

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-214-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-214-image-02.jpg)

设置名称，点击【Next】
点击【Browse】，选择生成的 xsa 文件；
点击【Finish】

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-215-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-215-image-02.jpg)

3. 编译硬件平台
4. 点击【Import Example】导入 axi dma 的参考示例

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-216-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-216-image-02.jpg)

5. 选择 simple_poll 示例
6. 对示例源文件进行修改：设置 MAX_PKT_LEN,就是长度，单位为字节，

TEST_START_VALUE 为起始的数据值，NUMBER_OF_TRANSFERS 为测
试次数；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-217-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-217-image-02.jpg)

打开 S2MM 的 IOC 中断，关闭 MM2S 的所有中断。在 S2MM 接收完数据后会
发出中断。
打开 MM2S 通路和 S2MM 通路

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-218-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-218-image-02.jpg)

### 5.4.3 下载验证

1. 我们在 vitis 里面 debug，应用程序。
2. 等待 bit 下载完成之后，在 vivado 中打开 ila，设置触发条件
3. 在 vitis 的 Debug 界面，不用设置断点，点击 Resume
4. 此时可以看到 ila 已经触发，可以观察采集到的数据。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-219-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-219-image-02.jpg)

在串口调试工具中，可以看到打印信息

5. 我们也可以在 vitis 调试中，设置断点，观察 memory 信息；

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-220-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-220-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-220-image-03.jpg)

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-221-image-01.jpg)
