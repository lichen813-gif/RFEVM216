# 4. PS 端外设

[Switch to English](../../en/fpga-tutorial/04-ps-peripherals.md)

> 本章内容来自中文原始 PDF。图示和软件界面截图保留原标签，以便与硬件和软件实际界面对应。  
> Source PDF: `RFEVM216开发平台FPGA教程.pdf`  
> Source pages: 71-159

<a id="page-71"></a>
## 原 PDF 第 71 页

69 / 223  
4 PS 端外设  
本章主要介绍 ZYNQ 核的配置，PS 端外设的应用，如 MIO、UART、以太  
网和 RTC 等的基础实验。  
前面的实验都是在 PL 端进行的，可以看到和普通 FPGA 开发流程没有任何  
区别，ZYNQ 的主要优势就是 FPGA 和 ARM 的合理结合，这对开发人员提出了  
更高的要求。从本章开始，我们开始使用 ARM，也就是我们说的 PS。  
4.1 IPI 设计建立  
Vivado IP 集成器（IPI）是 vivado 集成开发环境提供的 IP 集成设计界面。IP  
集成器是一个图形化，支持脚本配置与连接的设计开发环境。在 IP 集成器不仅  
可使用 IP 进行基于处理器的设计还可以进行非处理器的纯逻辑设计开发。  
这里我们在 IPI 里面使能所有 PS 的外设，后续的 PS 外设实验就只需在 vitis  
下面操作即可。  
4.1.1 硬件工程搭建  
1) 打开 vivado  
2) 选择 Create Project

---

<a id="page-72"></a>
## 原 PDF 第 72 页

70 / 223  
3) 点击 Next  
4) 设置工程名称（rfevm216_ipi）和位置(E:/rfevm216/demo),点击 Next；

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 72, figure 1](../../assets/fpga-tutorial/page-072-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 72, figure 2](../../assets/fpga-tutorial/page-072-image-02.jpg)

---

<a id="page-73"></a>
## 原 PDF 第 73 页

71 / 223  
5) 选择 RTL Project，点击 Next  
6) 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 73, figure 1](../../assets/fpga-tutorial/page-073-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 73, figure 2](../../assets/fpga-tutorial/page-073-image-02.jpg)

---

<a id="page-74"></a>
## 原 PDF 第 74 页

72 / 223  
7) 点击 Finish  
8) 在 IPI（IP INTEGRATOR）下选择 Create Block Design

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 74, figure 1](../../assets/fpga-tutorial/page-074-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 74, figure 2](../../assets/fpga-tutorial/page-074-image-02.jpg)

---

<a id="page-75"></a>
## 原 PDF 第 75 页

73 / 223  
9) 设置设计名称：system，点击 OK  
10) 点击+（Add IP）

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 75, figure 1](../../assets/fpga-tutorial/page-075-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 75, figure 2](../../assets/fpga-tutorial/page-075-image-02.jpg)

---

<a id="page-76"></a>
## 原 PDF 第 76 页

74 / 223  
11) 选择 Zynq UltraScale+ MPSoC  
12) 双击 Zynq UltraScale+ MPSoC 或者右键选择 Customize Block...

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 76, figure 1](../../assets/fpga-tutorial/page-076-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 76, figure 2](../../assets/fpga-tutorial/page-076-image-02.jpg)

---

<a id="page-77"></a>
## 原 PDF 第 77 页

75 / 223  
13) 下面会显示 MPSoC 硬核的架构图  
 在 IO Configuration 窗口  
配置 Bank0、Bank1、Bank2、Bank3 电压为 LVCMOS18

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 77, figure 1](../../assets/fpga-tutorial/page-077-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 77, figure 2](../../assets/fpga-tutorial/page-077-image-02.jpg)

---

<a id="page-78"></a>
## 原 PDF 第 78 页

76 / 223  
 在 Low Speed->Memory Interface 界面，勾选 QSPI 和 SD 0、SD 1；  
QSPI：Dual Parallel、x4

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 78, figure 1](../../assets/fpga-tutorial/page-078-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 78, figure 2](../../assets/fpga-tutorial/page-078-image-02.jpg)

---

<a id="page-79"></a>
## 原 PDF 第 79 页

77 / 223  
SD 0：MIO13..22、eMMC、8Bit、Reset MIO23  
SD 1：MIO46..51、SD 2.0、4Bit、CD MIO45  
 在 Low Speed->I/O Peripherals 界面，勾选 I2C 1、UART 0、UART 1；

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 79, figure 1](../../assets/fpga-tutorial/page-079-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 79, figure 2](../../assets/fpga-tutorial/page-079-image-02.jpg)

---

<a id="page-80"></a>
## 原 PDF 第 80 页

78 / 223  
在 Low Speed->Processing Uint 界面，勾选 TTC 0、TTC1、TTC 2、TTC 3；  
在 High Speed 界面，勾选 GEM 3、USB 0 、USB3.0、PCIe、Display Port；

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 80, figure 1](../../assets/fpga-tutorial/page-080-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 80, figure 2](../../assets/fpga-tutorial/page-080-image-02.jpg)

---

<a id="page-81"></a>
## 原 PDF 第 81 页

79 / 223

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 81, figure 1](../../assets/fpga-tutorial/page-081-image-01.jpg)

---

<a id="page-82"></a>
## 原 PDF 第 82 页

80 / 223  
 在 Clock Configuration 窗口  
按照下图配置输入时钟，其他默认即可；

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 82, figure 1](../../assets/fpga-tutorial/page-082-image-01.jpg)

---

<a id="page-83"></a>
## 原 PDF 第 83 页

81 / 223

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 83, figure 1](../../assets/fpga-tutorial/page-083-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 83, figure 2](../../assets/fpga-tutorial/page-083-image-02.jpg)

---

<a id="page-84"></a>
## 原 PDF 第 84 页

82 / 223  
 在 DDR Configuration 窗口，配置 DDR 的参数，如下图

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 84, figure 1](../../assets/fpga-tutorial/page-084-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 84, figure 2](../../assets/fpga-tutorial/page-084-image-02.jpg)

---

<a id="page-85"></a>
## 原 PDF 第 85 页

83 / 223  
 在 PCIe Configuration 窗口，主要配置设备端口类型和设备 ID，其他默  
认即可；  
 在 PS-PL Configuration 页，配置如下。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 85, figure 1](../../assets/fpga-tutorial/page-085-image-01.jpg)

---

<a id="page-86"></a>
## 原 PDF 第 86 页

84 / 223  
14) 点击 OK  
15) 选择 Tools->Validate Design，检查设置是否有错误  
16) 在 system 上右键选择 Create HDL Wrapper

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 86, figure 1](../../assets/fpga-tutorial/page-086-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 86, figure 2](../../assets/fpga-tutorial/page-086-image-02.jpg)

---

<a id="page-87"></a>
## 原 PDF 第 87 页

85 / 223  
17) 选择 Let Vivado manage wrapper and auto-update  
18) 点击 Run Synthesis（这里我们只使用 PS 的资源，不用产生 bit）

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 87, figure 1](../../assets/fpga-tutorial/page-087-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 87, figure 2](../../assets/fpga-tutorial/page-087-image-02.jpg)

---

<a id="page-88"></a>
## 原 PDF 第 88 页

86 / 223  
19) 综合完成之后，点击 OK  
20) 选择 File->Export->Export Hardware

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 88, figure 1](../../assets/fpga-tutorial/page-088-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 88, figure 2](../../assets/fpga-tutorial/page-088-image-02.jpg)

---

<a id="page-89"></a>
## 原 PDF 第 89 页

87 / 223  
21) 点击 Next  
22) 这里我们没有 bit，默认配置，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 89, figure 1](../../assets/fpga-tutorial/page-089-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 89, figure 2](../../assets/fpga-tutorial/page-089-image-02.jpg)

---

<a id="page-90"></a>
## 原 PDF 第 90 页

88 / 223  
23) 设置名称和路径，点击 Next  
24) 点击 Finish  
这里我们能看到新生成的 xsa 文件：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 90, figure 1](../../assets/fpga-tutorial/page-090-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 90, figure 2](../../assets/fpga-tutorial/page-090-image-02.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 90, figure 3](../../assets/fpga-tutorial/page-090-image-03.jpg)

---

<a id="page-91"></a>
## 原 PDF 第 91 页

89 / 223  
4.1.2 软件工程搭建  
上篇我们在 vivado 下搭建好硬件工程，导出 xsa 文件。这里在工程目录下面  
创建 vitis 文件夹作为 vitis 的工作目录。  
1) 登录 vitis  
2) 选择工作目录，点击 Launch

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 91, figure 1](../../assets/fpga-tutorial/page-091-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 91, figure 2](../../assets/fpga-tutorial/page-091-image-02.jpg)

---

<a id="page-92"></a>
## 原 PDF 第 92 页

90 / 223  
3) 点击 Create Platform Project  
4) 设置工程名称，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 92, figure 1](../../assets/fpga-tutorial/page-092-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 92, figure 2](../../assets/fpga-tutorial/page-092-image-02.jpg)

---

<a id="page-93"></a>
## 原 PDF 第 93 页

91 / 223  
5) 点击 Browse..

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 93, figure 1](../../assets/fpga-tutorial/page-093-image-01.jpg)

---

<a id="page-94"></a>
## 原 PDF 第 94 页

92 / 223  
6) 选择之前生成的 xsa 文件，点击 Finish

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 94, figure 1](../../assets/fpga-tutorial/page-094-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 94, figure 2](../../assets/fpga-tutorial/page-094-image-02.jpg)

---

<a id="page-95"></a>
## 原 PDF 第 95 页

93 / 223  
7) 在生成的 plf 上面右键，点击编译

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 95, figure 1](../../assets/fpga-tutorial/page-095-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 95, figure 2](../../assets/fpga-tutorial/page-095-image-02.jpg)

---

<a id="page-96"></a>
## 原 PDF 第 96 页

94 / 223  
至此我们软件工程搭建完毕，后面在此基础上就可以进行 PS 裸机的实验；  
4.2 体验 ARM，裸机输出”Hello World”  
“Hello World！”是各种编程语言中最简单，也是最经典的入门实验。这里  
我们将串口打印“Hello World”作为嵌入式系统的开篇实验，这也是我们步入  
PS 部分的始发点。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 96, figure 1](../../assets/fpga-tutorial/page-096-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 96, figure 2](../../assets/fpga-tutorial/page-096-image-02.jpg)

---

<a id="page-97"></a>
## 原 PDF 第 97 页

95 / 223  
4.2.1 硬件介绍  
RFEVM216 底板上预留了一个 JTAG&UART 接口，既可以用它下载调试程  
序，也可以通过串口和 PC 通信。  
图 10 JTAG&UART 硬件原理图  
4.2.2 vitis 程序开发  
我们在上节的基础上，创建基于串口的应用程序。  
1) 登录 vitis，切换到之前的工作目录

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 97, figure 1](../../assets/fpga-tutorial/page-097-image-01.jpg)

---

<a id="page-98"></a>
## 原 PDF 第 98 页

96 / 223  
2) 新建应用程序 File->New->Application Project  
3) 点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 98, figure 1](../../assets/fpga-tutorial/page-098-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 98, figure 2](../../assets/fpga-tutorial/page-098-image-02.jpg)

---

<a id="page-99"></a>
## 原 PDF 第 99 页

97 / 223  
4) 此处默认选择的就是之前生成的 platform，直接点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 99, figure 1](../../assets/fpga-tutorial/page-099-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 99, figure 2](../../assets/fpga-tutorial/page-099-image-02.jpg)

---

<a id="page-100"></a>
## 原 PDF 第 100 页

98 / 223  
5) 填入 APP 工程名称，其他默认，点击 Next  
6) 点击 Next  
7) 选择 Hello World 模板，点击 Finish

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 100, figure 1](../../assets/fpga-tutorial/page-100-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 100, figure 2](../../assets/fpga-tutorial/page-100-image-02.jpg)

---

<a id="page-101"></a>
## 原 PDF 第 101 页

99 / 223  
8) 完成之后可以看到生成的 APP 工程  
9) 在 APP 工程上右键，选择 Build Project，或者点击菜单栏的锤子按键，进行  
工程编译；

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 101, figure 1](../../assets/fpga-tutorial/page-101-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 101, figure 2](../../assets/fpga-tutorial/page-101-image-02.jpg)

---

<a id="page-102"></a>
## 原 PDF 第 102 页

100 / 223  
Console 窗口会显示编译信息，编译结束会生成 elf 文件  
10) 右键 APP 工程，选择 Run As->Run Configuration

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 102, figure 1](../../assets/fpga-tutorial/page-102-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 102, figure 2](../../assets/fpga-tutorial/page-102-image-02.jpg)

---

<a id="page-103"></a>
## 原 PDF 第 103 页

101 / 223  
11) 双击 Single Application Debug，生成 Debugger_hello；在 Target Setup 页面进  
行相关设置。（这里我们只有 PS 部分，所以不用使能 Program FPGA）

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 103, figure 1](../../assets/fpga-tutorial/page-103-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 103, figure 2](../../assets/fpga-tutorial/page-103-image-02.jpg)

---

<a id="page-104"></a>
## 原 PDF 第 104 页

102 / 223  
12) PC 侧打开串口调试终端，选择相应的串口号和波特率 115200；  
13) 点击 11 步的 Run，右下角会显示下载进度  
14) 下载完成后，查看串口输出

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 104, figure 1](../../assets/fpga-tutorial/page-104-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 104, figure 2](../../assets/fpga-tutorial/page-104-image-02.jpg)

---

<a id="page-105"></a>
## 原 PDF 第 105 页

103 / 223  
4.2.3 固化程序  
4.2.3.1 生成 boot.bin 文件  
普通的 FPGA 一般是可以从 flash 启动，或者被动加载，ZYNQ 的启动是由  
ARM 主导的，包括 FPGA 程序的加载。  
ZYNQ RFSOC 的启动流程主要分为三个阶段（UG1085 中有详细介绍）：  
- 预处理阶段（Pre-configuration stage）：通过 ROM 中的代码复位并且唤醒处
理器。  
- 配置阶段（Configuration stage）：通过 APU 或者 RPU 将 FSBL 代码加载到
片上 RAM（on-chip RAM，OCM）。  
- 后处理阶段（Post-configuration stage）：在 FSBL 之后启动 U-BOOT，Linux
等。  
下图给出了启动的详细步骤：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 105, figure 1](../../assets/fpga-tutorial/page-105-image-01.jpg)

---

<a id="page-106"></a>
## 原 PDF 第 106 页

104 / 223  
需要注意的是，对于 ZYNQ 而言，是不能够单独固化 PL 的程序的，这是因  
为 ZYNQ 系列中的 PL 部分通常是通过 PS 来配置的（可认为 PL 是作为 PS 的外  
设），且许多非易失性存储器是连接在 PS 端的。PL 的配置和启动通常依赖于  
PS 端的引导过程。PL 的程序需要通过 PS 端的引导过程来加载和配置。  
RFSoC 启动所需要的文件  
- Boot image/boot.bin 文件，该文件主要包含：
 First Stage Boot Loader（fsbl.elf）  
 平台管理固件（pmufw.elf）  
 PL 部分的 bitstream（system.bit），这部分是可选的  
 ARM 可信固件（bl31.elf）  
 Second Stage Boot Loader，例如针对 U-Boot 的 uboot.elf 或者应用软件  
- Linux 二进制镜像文件 image.ub，该文件主要包含
 展开的设备树（Flattened Device Tree）的二进制对象（system.dtb）  
 Linux 的内核（Image）  
- 根文件系统，可以是 Ramdisk（initrd）或者在 SD 卡上，Flash 上。
Xilinx 的工具 Vitis 可以实现左边裸机的启动步骤，Petalinux 可以实现右边 Linux  
系统的启动步骤。

---

<a id="page-107"></a>
## 原 PDF 第 107 页

105 / 223  
这里我们在 vitis 工具下生成裸机需要的启动文件 boot.bin：  
1. 选中我们新建的应用工程，在“xxx_system”文件夹上点击右键

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 107, figure 1](../../assets/fpga-tutorial/page-107-image-01.jpg)

---

<a id="page-108"></a>
## 原 PDF 第 108 页

106 / 223  
2. 点击【Build Project】，这一步会自动生成 boot.bin 文件

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 108, figure 1](../../assets/fpga-tutorial/page-108-image-01.jpg)

---

<a id="page-109"></a>
## 原 PDF 第 109 页

107 / 223  
我们也可以在手动生成 boot.bin 文件：  
1. 选中我们新建的应用工程，在“xxx_system”文件夹上点击右键

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 109, figure 1](../../assets/fpga-tutorial/page-109-image-01.jpg)

---

<a id="page-110"></a>
## 原 PDF 第 110 页

108 / 223  
2. 点击【Create Boot Image】  
3. 在弹出的窗口中可以看到生成的 BIF 文件路径和生成的 BOOT.BIN 文件路  
径，BOOT.bin 文件是我们需要的启动文件，可以放到 SD 卡启动，也可以烧  
写到 QSPI FLASH。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 110, figure 1](../../assets/fpga-tutorial/page-110-image-01.jpg)

---

<a id="page-111"></a>
## 原 PDF 第 111 页

109 / 223  
其中 BOOT Image Partitons 列表中有要合成的文件，第一个文件一定是 bootloader  
文件，这是生成硬件平台的时候编译完自动生成的 fsbl.elf 文件，第二个文件是  
FPGA 配置文件 bitstream，在本实验中由于没有 FPGA 的 bitstream，不需要添加，  
第三个是应用程序，在本实验中为 hello.elf，由于没有 bitstream，在本实验中只  
添加 bootloader 和应用程序，点击【Create Image】生成。  
4.2.3.2 SD 卡启动测试  
1. 格式化 SD 卡，文件系统选择为为 FAT32 格式；  
2. 把上一步生成的 BOOT.BIN 文件，复制到 SD 卡里面；  
3. SD 卡插入开发板的 SD 卡插槽；  
4. 启动模式调整为 SD 卡启动（SWC1 拨码开关全拨到 OFF）；  
5. 打开串口软件，上电启动，即可看到打印信息；

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 111, figure 1](../../assets/fpga-tutorial/page-111-image-01.jpg)

---

<a id="page-112"></a>
## 原 PDF 第 112 页

110 / 223  
4.2.3.3 QSPI 启动测试  
1. 在 vitis 菜单 Xilinx->Program Flash  
2. 弹出的 Program Flash Memory 界面里面，Image File 文件选择我们要烧写的  
BOOT.BIN 文件 ， FSBL File 选择 fsbl.elf 文件 ， Flash Type 选择  
qspi-x8-dual_parallel 类型，点击【Program】后，等待烧写完成；  
3. 烧写完成后，设置启动模式为 QSPI 启动（SWC1 拨码开关全拨到 ON），重  
新上电启动，可以在串口软件里面看到与 SD 卡启动同样的效果。  
4.3 PS 端 RTC 中断实验  
RTC（Real Time Clock）实时时钟单元为系统和应用软件提供精确的时间基

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 112, figure 1](../../assets/fpga-tutorial/page-112-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 112, figure 2](../../assets/fpga-tutorial/page-112-image-02.jpg)

---

<a id="page-113"></a>
## 原 PDF 第 113 页

111 / 223  
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

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 113, figure 1](../../assets/fpga-tutorial/page-113-image-01.jpg)

---

<a id="page-114"></a>
## 原 PDF 第 114 页

112 / 223  
图 12 RTC 功能图  
4.3.1 软件设计  
1) 登录 Vitis，切换到之前的工作目录，然后双击 platform.spr，选中 Board Support  
Package，可以看到 psu_rtc 的文档和导入示例。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 114, figure 1](../../assets/fpga-tutorial/page-114-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 114, figure 2](../../assets/fpga-tutorial/page-114-image-02.jpg)

---

<a id="page-115"></a>
## 原 PDF 第 115 页

113 / 223  
2) 点击 Import Example，会弹出如下图所示的导入示例界面；  
3) 这里我们选中第三个官方示例 RTC 中断周期报警的示例  
（xrtcpsu_periodic_alarm_interrupt_example），点击 OK  
4) 这里我们就导入了 example 工程

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 115, figure 1](../../assets/fpga-tutorial/page-115-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 115, figure 2](../../assets/fpga-tutorial/page-115-image-02.jpg)

---

<a id="page-116"></a>
## 原 PDF 第 116 页

114 / 223  
5) 选中应用工程，右键后选中 Build Project 对工程进行编译  
编译进度可以在工具下方的控制台面板（Console）中进行查看，如下图十  
所：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 116, figure 1](../../assets/fpga-tutorial/page-116-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 116, figure 2](../../assets/fpga-tutorial/page-116-image-02.jpg)

---

<a id="page-117"></a>
## 原 PDF 第 117 页

115 / 223  
4.3.2 下载验证  
首先我们将 USB 转 Type-C 线缆的 Type-C 端与 RFEVM2116 开发板上的  
JTAG 接口连接，USB 转 Type-C 线缆的另外一端与电脑连接。连接开发板电源，  
给开发板上电。  
下载程序，右键点击应用工程，选择 Run As->Run Configuration...

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 117, figure 1](../../assets/fpga-tutorial/page-117-image-01.jpg)

---

<a id="page-118"></a>
## 原 PDF 第 118 页

116 / 223  
双击 Single Application Debug 一项  
选中 Target Setup 标签页，默认配置，点击 Run

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 118, figure 1](../../assets/fpga-tutorial/page-118-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 118, figure 2](../../assets/fpga-tutorial/page-118-image-02.jpg)

---

<a id="page-119"></a>
## 原 PDF 第 119 页

117 / 223  
下载完成后，在串口调试终端可以看到串口的要打印信息：  
4.4 PS 端 IIC 的使用  
4.4.1 硬件设计  
PS 端 IIC 接了一个外设 EEPROM，本节介绍如何利用 IIC 读写外设。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 119, figure 1](../../assets/fpga-tutorial/page-119-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 119, figure 2](../../assets/fpga-tutorial/page-119-image-02.jpg)

---

<a id="page-120"></a>
## 原 PDF 第 120 页

118 / 223  
4.4.2 软件设计  
1) 登录 Vitis，切换到之前的工作目录，然后双击 platform.spr，选中 Board Support  
Package，可以看到 psu_i2c_1 的文档链接和导入示例。  
2) 点击 Import Example，然后选中 xiicps_eeprom_polled_example 示例，点击  
OK

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 120, figure 1](../../assets/fpga-tutorial/page-120-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 120, figure 2](../../assets/fpga-tutorial/page-120-image-02.jpg)

---

<a id="page-121"></a>
## 原 PDF 第 121 页

119 / 223  
3) 可以看到导入的示例应用工程  
4) EEPROM 的设备地址在程序的前面做了定义，这个地址就是系统访问外部  
IIC 外设的设备地址，这里 EEPROM 地址修改为 0x50，然后保存。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 121, figure 1](../../assets/fpga-tutorial/page-121-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 121, figure 2](../../assets/fpga-tutorial/page-121-image-02.jpg)

---

<a id="page-122"></a>
## 原 PDF 第 122 页

120 / 223  
EEPROM 的设备地址可以在 AT24CM01 的芯片手册上找到。  
其中 A1、A2 硬件里面直接接地，为 0；  
程序流程如下：  
ReadBuffer 清 0，WriteBuffer 赋递增数据->写 32 个字节到 EEPROM->读  
EEPROM 的 16 个字节到 ReadBuffer->检验是否正确->返回。  
5) 选中应用工程，右键点击 Build Project

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 122, figure 1](../../assets/fpga-tutorial/page-122-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 122, figure 2](../../assets/fpga-tutorial/page-122-image-02.jpg)

---

<a id="page-123"></a>
## 原 PDF 第 123 页

121 / 223  
编译信息可以在 Console 窗口中看到  
4.4.3 下载验证  
首先我们将下载线（USB 转 Type-C 线缆）与开发板的 JTAG 接口连接，另

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 123, figure 1](../../assets/fpga-tutorial/page-123-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 123, figure 2](../../assets/fpga-tutorial/page-123-image-02.jpg)

---

<a id="page-124"></a>
## 原 PDF 第 124 页

122 / 223  
外一端与电脑连接。最后打开开发板的电源开关。  
右键应用工程，选择 Run As->Launch Hardware(Single Application Debug)  
打开串口终端，下载完成后，可以查看串口输出：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 124, figure 1](../../assets/fpga-tutorial/page-124-image-01.jpg)

---

<a id="page-125"></a>
## 原 PDF 第 125 页

123 / 223  
4.5 PS 端以太网使用之 lwip  
LWIP 是瑞典计算机科学院（SICS）的 Adam Dunkels 等开发的一个小型开  
源的 TCP/IP 协议栈，是 TCP/IP 的一种实现方式。LWIP 是轻量级 IP 协议，有无  
操作系统的支持都可以运行。LWIP 实现的重点是在保持 TCP 协议主要功能的基  
础上减少对 RAM 的占用，它只需要十几 KB 的 RAM 和 40K 左右的 ROM 就可  
以运行，这使 LWIP 协议栈适合在低端的嵌入式系统中使用。  
这里我们使用 Vitis 软件自带的 Lwip Echo Server 模板了解 LWIP 的使用。  
4.5.1 硬件设计  
RFEVM216 开发板上有一个 PS 端的 RJ45 以太网接口，用于连接以太网线，  
其原理图如图所示：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 125, figure 1](../../assets/fpga-tutorial/page-125-image-01.jpg)

---

<a id="page-126"></a>
## 原 PDF 第 126 页

124 / 223  
图 13 RJ45 接口原理图  
以太网的数据传输离不开以太网 PHY（物理层）芯片的支持。RFEVM216  
开发板上使用的 PHY 芯片为德州仪器(Texas Instruments)的 DP83867ISRGZ 芯  
片，其部分原理图如图所示：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 126, figure 1](../../assets/fpga-tutorial/page-126-image-01.jpg)

---

<a id="page-127"></a>
## 原 PDF 第 127 页

125 / 223  
图 14 DP83867ISRGZ 原理图  
4.5.2 软件设计  
BSP 库文件里面添加 lwip 库  
双击 platform.spr，选中 Board Support Package，点击 Modify BSP Settings...

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 127, figure 1](../../assets/fpga-tutorial/page-127-image-01.jpg)

---

<a id="page-128"></a>
## 原 PDF 第 128 页

126 / 223  
使能 lwip 库，点击 OK  
编译 paltform

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 128, figure 1](../../assets/fpga-tutorial/page-128-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 128, figure 2](../../assets/fpga-tutorial/page-128-image-02.jpg)

---

<a id="page-129"></a>
## 原 PDF 第 129 页

127 / 223  
新建应用程序 File->New->Application Project  
点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 129, figure 1](../../assets/fpga-tutorial/page-129-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 129, figure 2](../../assets/fpga-tutorial/page-129-image-02.jpg)

---

<a id="page-130"></a>
## 原 PDF 第 130 页

128 / 223  
点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 130, figure 1](../../assets/fpga-tutorial/page-130-image-01.jpg)

---

<a id="page-131"></a>
## 原 PDF 第 131 页

129 / 223  
设置 APP 名称，点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 131, figure 1](../../assets/fpga-tutorial/page-131-image-01.jpg)

---

<a id="page-132"></a>
## 原 PDF 第 132 页

130 / 223  
点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 132, figure 1](../../assets/fpga-tutorial/page-132-image-01.jpg)

---

<a id="page-133"></a>
## 原 PDF 第 133 页

131 / 223  
选择 Lwip Echo Server 模板，点击 Finish  
我们修改板卡的 ip 和网段，是板卡和 PC 处于同一个网段

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 133, figure 1](../../assets/fpga-tutorial/page-133-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 133, figure 2](../../assets/fpga-tutorial/page-133-image-02.jpg)

---

<a id="page-134"></a>
## 原 PDF 第 134 页

132 / 223  
修改完成之后，保存文件，右键 lwip_echo_server 工程，点击 Build Project

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 134, figure 1](../../assets/fpga-tutorial/page-134-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 134, figure 2](../../assets/fpga-tutorial/page-134-image-02.jpg)

---

<a id="page-135"></a>
## 原 PDF 第 135 页

133 / 223  
4.5.3 下载验证  
1) 这里我们用千兆网线连接 PC 和 RFEVM 开发板，然后给板卡上电  
2) PC 和 RFEVM 的 IP 地址要在同一个网段，才可以相互通信。  
RFEVM216 以太网的的默认配置：  
mac 地址：00: 0a: 35: 00: 01: 02  
IP 地址：192.168.5.10  
子网掩码：255.255.255.0  
网关：192.168.5.1  
3) 右键 lwip_echo_server 工程，选择 Run As->Run Configuration

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 135, figure 1](../../assets/fpga-tutorial/page-135-image-01.jpg)

---

<a id="page-136"></a>
## 原 PDF 第 136 页

134 / 223  
4) 我们打开串口调试终端，下载完程序后，终端会显示程序的打印信息  
5) 打开 cmd 窗口，ping 板卡 IP

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 136, figure 1](../../assets/fpga-tutorial/page-136-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 136, figure 2](../../assets/fpga-tutorial/page-136-image-02.jpg)

---

<a id="page-137"></a>
## 原 PDF 第 137 页

135 / 223  
4.5.4 参考文档  
https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842366/Standalone+LWIP+lib  
rary  
4.6 PS 端 DiplayPort 的使用  
4.6.1 硬件设计  
RFEVM216 底板上有一路 DP 显示接口，可以连接 DP 显示器进行输出。设  
计原理框图如下所示：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 137, figure 1](../../assets/fpga-tutorial/page-137-image-01.jpg)

---

<a id="page-138"></a>
## 原 PDF 第 138 页

136 / 223  
4.6.2 软件设计  
1) 双击 platform.spr，选中 Board Support Package  
2) 点击 Import Example，然后选中 xdpdma_video_example 示例，点击 OK

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 138, figure 1](../../assets/fpga-tutorial/page-138-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 138, figure 2](../../assets/fpga-tutorial/page-138-image-02.jpg)

---

<a id="page-139"></a>
## 原 PDF 第 139 页

137 / 223  
3) 选中应用工程，右键点击 Build Project  
4.6.3 下载验证  
这里我们需要使用 DP 数据线一端连到带 DP 接口的显示器上，另外一端连  
到板卡的 DP 接口。然后给开发板上电。  
右键应用工程，选择 Run As->Launch Hardware(Single Application Debug)

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 139, figure 1](../../assets/fpga-tutorial/page-139-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 139, figure 2](../../assets/fpga-tutorial/page-139-image-02.jpg)

---

<a id="page-140"></a>
## 原 PDF 第 140 页

138 / 223  
打开串口终端，下载完成后，可以查看串口输出：  
同时显示器上输出彩条

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 140, figure 1](../../assets/fpga-tutorial/page-140-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 140, figure 2](../../assets/fpga-tutorial/page-140-image-02.jpg)

---

<a id="page-141"></a>
## 原 PDF 第 141 页

139 / 223  
4.7 SD 卡读写 TXT 文本实验  
RFEVM216 底板上 SD 卡接口为小卡的设计，可以连接 Micro SD 卡（也叫  
TF 卡），MPSOC 内部集成了两个 SD 卡控制器，并且 Xilinx Vitis 的 standlone  
已经移植好了 FATFS（Vitis 软件中叫做 xilffs）文件系统，FATFS 是一个完全开  
源免费的 FAT 文件系统模块，专门为小型的嵌入式系统而设计。它完全用标准 C  
语言编写，所以有良好的硬件平台独立性，可以很方便的移植到各种嵌入式处理  
器中。因此在 Vitis 中添加 xilffs 库后，就可以在程序中使用 FATFS 中的 API 函  
数来操作 SD 卡。  
使用者无需理会 FATFS 的内部结构和复杂的 FAT 协议，只需要调用 FATFS  
模块提供给用户的一系列应用接口函数，如 f_open、f_read、f_write 和 f_close  
等，就可以像在 PC 上读/写文件那样简单。  
4.7.1 硬件设计  
我们的 RFEVM216 开发板上面有一个 SD 卡接口，可以连接 Micro SD 卡（TF  
卡），原理图如下图所示：

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 141, figure 1](../../assets/fpga-tutorial/page-141-image-01.jpg)

---

<a id="page-142"></a>
## 原 PDF 第 142 页

140 / 223  
图 15 Micro SD 卡原理图  
由上图可知，SD 卡共有四根数据线（SDIO_DAT0~SDIO_DAT3），连接至  
MPSOC 的引脚。图中 SDIO_DETECT 信号是 TF 卡检测信号，用于标志开发板  
是否连接了 TF 卡。当开发板没有连接 TF 卡时，此信号为高电平；而当开发板  
连接了 TF 卡之后，此信号为低电平，表示开发板已经连接了 TF 卡。  
4.7.2 软件设计  
BSP 库文件里面添加 xilffs 库  
双击 platform.spr，选中 Board Support Package，点击 Modify BSP Settings...

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 142, figure 1](../../assets/fpga-tutorial/page-142-image-01.jpg)

---

<a id="page-143"></a>
## 原 PDF 第 143 页

141 / 223  
使能“xilffs”库，点击“OK”  
添加完 FATFS 库之后，对 TF 卡的操作会简单很多，我们只需要在程序中调用  
FATFS 的库函数即可。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 143, figure 1](../../assets/fpga-tutorial/page-143-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 143, figure 2](../../assets/fpga-tutorial/page-143-image-02.jpg)

---

<a id="page-144"></a>
## 原 PDF 第 144 页

142 / 223  
添加完成之后，重新编译 platform  
新建应用程序 File->New->Application Project  
点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 144, figure 1](../../assets/fpga-tutorial/page-144-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 144, figure 2](../../assets/fpga-tutorial/page-144-image-02.jpg)

---

<a id="page-145"></a>
## 原 PDF 第 145 页

143 / 223  
点击 Next

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 145, figure 1](../../assets/fpga-tutorial/page-145-image-01.jpg)

---

<a id="page-146"></a>
## 原 PDF 第 146 页

144 / 223  
设置应用名称，点击“Next”

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 146, figure 1](../../assets/fpga-tutorial/page-146-image-01.jpg)

---

<a id="page-147"></a>
## 原 PDF 第 147 页

145 / 223  
点击“Next”

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 147, figure 1](../../assets/fpga-tutorial/page-147-image-01.jpg)

---

<a id="page-148"></a>
## 原 PDF 第 148 页

146 / 223  
这里我们选择 Empty Application(C)作为模板，点击“Finish”

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 148, figure 1](../../assets/fpga-tutorial/page-148-image-01.jpg)

---

<a id="page-149"></a>
## 原 PDF 第 149 页

147 / 223  
这里我们可以看到新建的应用工程。  
接下来为应用工程新建一个源文件“main.c”

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 149, figure 1](../../assets/fpga-tutorial/page-149-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 149, figure 2](../../assets/fpga-tutorial/page-149-image-02.jpg)

---

<a id="page-150"></a>
## 原 PDF 第 150 页

148 / 223

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 150, figure 1](../../assets/fpga-tutorial/page-150-image-01.jpg)

---

<a id="page-151"></a>
## 原 PDF 第 151 页

149 / 223  
我们在新建的 main.c 文件中输入下列代码：  
#include "xparameters.h"  
#include "xil_printf.h"  
#include "ff.h"  
#include "xstatus.h"  
#define FILE_NAME "WE5G.txt" //定义文件名  
const char src_str[30] = "www.v3t.com.cn"; //定义文本内容  
//main 函数  
int main()  
{

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 151, figure 1](../../assets/fpga-tutorial/page-151-image-01.jpg)

---

<a id="page-152"></a>
## 原 PDF 第 152 页

150 / 223  
int status,len;  
char dest_str[30] = "";  
static FATFS fatfs;  
FIL fil; //文件对象  
UINT bw; //f_write 函数返回已写入的字节数  
UINT br; //f_read 函数返回已读出的字节数  
//注册一个工作区(挂载分区文件系统)  
//在使用任何其它文件函数之前，必须使用 f_mount 函数为每个使用卷注册一个工作区  
status = f_mount(&fatfs,"1:/", 1); //挂载 SD 卡  
if (status != FR_OK) {  
xil_printf("\r\nUnable to mount FATfs\r\n");  
return -1;  
}  
xil_printf("Success to open SD card!\r\n");  
len = strlen(src_str); //计算字符串长度  
//打开一个文件,如果不存在，则创建一个文件  
status=f_open(&fil,"1:/WE5G.txt",FA_OPEN_ALWAYS | FA_WRITE | FA_READ);  
if (status != FR_OK) {  
xil_printf("Unable to open file!\r\n");  
return -1;  
}  
xil_printf("Success to open file.\r\n");  
//移动打开的文件对象的文件读/写指针 0:指向文件开头  
f_lseek(&fil, 0);  
//向文件中写入数据  
f_write(&fil,(void*) src_str,len,&bw);  
xil_printf("write file return:%d.\r\n",bw);  
//SD 卡读数据  
//sd_read_data(FILE_NAME,(u32)dest_str,len);  
f_lseek(&fil, 0);  
f_read(&fil,(void*)dest_str,len,&br);  
f_close(&fil);  
xil_printf("read file return:%d.\r\n",bw);  
//比较写入的字符串和读出的字符串是否相等  
if (strcmp(src_str, dest_str) == 0)  
xil_printf("src_str is equal to dest_str,SD card test success!\r\n");  
else  
xil_printf("src_str is not equal to dest_str,SD card test failed!\r\n");

---

<a id="page-153"></a>
## 原 PDF 第 153 页

151 / 223  
return 0;  
}  
在 main 函数中，实现的功能是向 TF 卡中读写 TXT 文本，并比较写入的数  
据和读出的数据是否一致。程序首先调用 f_mount()函数挂载 TF 卡，接下来根据  
待写入字符串的长度，通过 f_write()函数和 f_read()函数对 TF 卡中的 TXT 文本  
进行写入和读出，然后比较写入和读出的值，并打印比较的结果。  
4.7.3 下载验证  
首先我们将下载线（USB 转 Type-C 线缆）与开发板的 JTAG 接口连接，另  
外一端与电脑连接。接下来插入 TF 卡。最后打开开发板的电源开关。  
右键应用工程，选择 Run As->Launch Hardware(Single Application Debug)  
打开串口终端，下载完成后，可以查看串口输出：  
由上图可知，显示写入的字符和读出的字符一致，说明 TF 卡读写测试成功。  
接下来从开发板的卡槽中取出 TF 卡，通过连接读卡器来插入电脑的 USB  
接口，此时可以看到 TF 卡中的文件内容如下图所示。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 153, figure 1](../../assets/fpga-tutorial/page-153-image-01.jpg)

---

<a id="page-154"></a>
## 原 PDF 第 154 页

152 / 223  
打开“WE5G.txt”文本，可以看到文本的内容，如下图所示：  
4.7.4 参考文档  
http://elm-chan.org/fsw/ff/00index_e.html  
4.8 基于 PS 的 USB slave 功能测试  
ZYNQ 的 USB 接口可以同时当作 USB HOST 和 USB DEVICE(SLAVE)，USB  
功能大多数情况下都是在 linux 下使用的，这里我们在裸机下去测试 USB 功能。  
我们使用官方提供的演示 demo，去把 usb 设备模拟成 U 盘的功能进行测试。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 154, figure 1](../../assets/fpga-tutorial/page-154-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 154, figure 2](../../assets/fpga-tutorial/page-154-image-02.jpg)

---

<a id="page-155"></a>
## 原 PDF 第 155 页

153 / 223  
4.8.1 硬件设计  
图 16 USB 接口原理图  
4.8.2 软件设计  
4) 登录 Vitis，切换到之前的工作目录，然后双击 platform.spr，选中 Board Support  
Package，可以看到 psu_usb_xhci_0 的文档链接和导入示例。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 155, figure 1](../../assets/fpga-tutorial/page-155-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 155, figure 2](../../assets/fpga-tutorial/page-155-image-02.jpg)

---

<a id="page-156"></a>
## 原 PDF 第 156 页

154 / 223  
5) 点击 Import Example，然后选中 xusb_poll_example 示例，点击 OK  
6) 可以看到导入的示例应用工程  
7) 选中应用工程，右键点击 Build Project

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 156, figure 1](../../assets/fpga-tutorial/page-156-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 156, figure 2](../../assets/fpga-tutorial/page-156-image-02.jpg)

---

<a id="page-157"></a>
## 原 PDF 第 157 页

155 / 223  
编译信息可以在 Console 窗口中看到。  
4.8.3 下载验证  
这里我们需要使用 USB 公对公的数据线一端连到 RFEVM216 的 USB 接口  
上，另外一端连到 PC 端。然后给开发板上电。  
右键应用工程，选择 Run As->Launch Hardware(Single Application Debug)

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 157, figure 1](../../assets/fpga-tutorial/page-157-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 157, figure 2](../../assets/fpga-tutorial/page-157-image-02.jpg)

---

<a id="page-158"></a>
## 原 PDF 第 158 页

156 / 223  
打开串口终端，下载完成后，可以查看串口输出：  
PC 侧会弹出如下窗口，点击“格式化磁盘”即可  
在我的电脑里面，可以看到由 DDR RAM 虚拟出来的 U 盘，可以像正常 U 盘一  
样复制粘贴文件，注意这个 U 盘断电数据会丢失请不要放重要文件。  
容量大小可以在程序里面去配置，请不要超过板子上的 DDR 容量大小。  
我们可以使用 Xilinx WiKi 推荐的 CrystalDiskMark 工具对 U 盘进行性能测速。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 158, figure 1](../../assets/fpga-tutorial/page-158-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 158, figure 2](../../assets/fpga-tutorial/page-158-image-02.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 158, figure 3](../../assets/fpga-tutorial/page-158-image-03.jpg)

---

<a id="page-159"></a>
## 原 PDF 第 159 页

157 / 223  
4.8.4 参考文档  
https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842468/ZynqMp+USB+Stadal  
one+Driver

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 159, figure 1](../../assets/fpga-tutorial/page-159-image-01.jpg)
