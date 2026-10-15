# 4.2 体验 ARM，裸机输出”Hello World”

[Switch to English](../../../en/fpga-tutorial/04-ps-peripherals/02-arm-hello-world.md)

[返回章节总览](index.md)

“Hello World！”是各种编程语言中最简单，也是最经典的入门实验。这里
我们将串口打印“Hello World”作为嵌入式系统的开篇实验，这也是我们步入
PS 部分的始发点。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-096-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-096-image-02.jpg)

## 4.2.1 硬件介绍

RFEVM216 底板上预留了一个 JTAG&UART 接口，既可以用它下载调试程
序，也可以通过串口和 PC 通信。
图 10 JTAG&UART 硬件原理图

## 4.2.2 vitis 程序开发

我们在上节的基础上，创建基于串口的应用程序。

1. 登录 vitis，切换到之前的工作目录

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-097-image-01.jpg)

2. 新建应用程序 File->New->Application Project
3. 点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-098-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-098-image-02.jpg)

4. 此处默认选择的就是之前生成的 platform，直接点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-099-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-099-image-02.jpg)

5. 填入 APP 工程名称，其他默认，点击 Next
6. 点击 Next
7. 选择 Hello World 模板，点击 Finish

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-100-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-100-image-02.jpg)

8. 完成之后可以看到生成的 APP 工程
9. 在 APP 工程上右键，选择 Build Project，或者点击菜单栏的锤子按键，进行

工程编译；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-101-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-101-image-02.jpg)

Console 窗口会显示编译信息，编译结束会生成 elf 文件

10. 右键 APP 工程，选择 Run As->Run Configuration

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-102-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-102-image-02.jpg)

11. 双击 Single Application Debug，生成 Debugger_hello；在 Target Setup 页面进

行相关设置。（这里我们只有 PS 部分，所以不用使能 Program FPGA）

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-103-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-103-image-02.jpg)

12. PC 侧打开串口调试终端，选择相应的串口号和波特率 115200；
13. 点击 11 步的 Run，右下角会显示下载进度
14. 下载完成后，查看串口输出

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-104-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-104-image-02.jpg)

## 4.2.3 固化程序

### 4.2.3.1 生成 boot.bin 文件

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

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-105-image-01.jpg)

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
这里我们在 vitis 工具下生成裸机需要的启动文件 boot.bin：

1. 选中我们新建的应用工程，在“xxx_system”文件夹上点击右键

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-107-image-01.jpg)

2. 点击【Build Project】，这一步会自动生成 boot.bin 文件

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-108-image-01.jpg)

我们也可以在手动生成 boot.bin 文件：

1. 选中我们新建的应用工程，在“xxx_system”文件夹上点击右键

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-109-image-01.jpg)

2. 点击【Create Boot Image】
3. 在弹出的窗口中可以看到生成的 BIF 文件路径和生成的 BOOT.BIN 文件路

径，BOOT.bin 文件是我们需要的启动文件，可以放到 SD 卡启动，也可以烧
写到 QSPI FLASH。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-110-image-01.jpg)

其中 BOOT Image Partitons 列表中有要合成的文件，第一个文件一定是 bootloader
文件，这是生成硬件平台的时候编译完自动生成的 fsbl.elf 文件，第二个文件是
FPGA 配置文件 bitstream，在本实验中由于没有 FPGA 的 bitstream，不需要添加，
第三个是应用程序，在本实验中为 hello.elf，由于没有 bitstream，在本实验中只
添加 bootloader 和应用程序，点击【Create Image】生成。

### 4.2.3.2 SD 卡启动测试

1. 格式化 SD 卡，文件系统选择为为 FAT32 格式；
2. 把上一步生成的 BOOT.BIN 文件，复制到 SD 卡里面；
3. SD 卡插入开发板的 SD 卡插槽；
4. 启动模式调整为 SD 卡启动（SWC1 拨码开关全拨到 OFF）；
5. 打开串口软件，上电启动，即可看到打印信息；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-111-image-01.jpg)

### 4.2.3.3 QSPI 启动测试

1. 在 vitis 菜单 Xilinx->Program Flash
2. 弹出的 Program Flash Memory 界面里面，Image File 文件选择我们要烧写的

BOOT.BIN 文件 ， FSBL File 选择 fsbl.elf 文件 ， Flash Type 选择
qspi-x8-dual_parallel 类型，点击【Program】后，等待烧写完成；

3. 烧写完成后，设置启动模式为 QSPI 启动（SWC1 拨码开关全拨到 ON），重

新上电启动，可以在串口软件里面看到与 SD 卡启动同样的效果。
