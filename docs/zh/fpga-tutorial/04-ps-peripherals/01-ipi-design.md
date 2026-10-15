# 4.1 IPI 设计建立

[Switch to English](../../../en/fpga-tutorial/04-ps-peripherals/01-ipi-design.md)

[返回章节总览](index.md)

Vivado IP 集成器（IPI）是 vivado 集成开发环境提供的 IP 集成设计界面。IP
集成器是一个图形化，支持脚本配置与连接的设计开发环境。在 IP 集成器不仅
可使用 IP 进行基于处理器的设计还可以进行非处理器的纯逻辑设计开发。
这里我们在 IPI 里面使能所有 PS 的外设，后续的 PS 外设实验就只需在 vitis
下面操作即可。

## 4.1.1 硬件工程搭建

1. 打开 vivado
2. 选择 Create Project
3. 点击 Next
4. 设置工程名称（rfevm216_ipi）和位置(E:/rfevm216/demo),点击 Next；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-072-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-072-image-02.jpg)

5. 选择 RTL Project，点击 Next
6. 选择芯片型号 xczu49dr-fsvf1760-2-i，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-073-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-073-image-02.jpg)

7. 点击 Finish
8. 在 IPI（IP INTEGRATOR）下选择 Create Block Design

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-074-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-074-image-02.jpg)

9. 设置设计名称：system，点击 OK
10. 点击+（Add IP）

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-075-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-075-image-02.jpg)

11. 选择 Zynq UltraScale+ MPSoC
12. 双击 Zynq UltraScale+ MPSoC 或者右键选择 Customize Block...

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-076-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-076-image-02.jpg)

13. 下面会显示 MPSoC 硬核的架构图

 在 IO Configuration 窗口
配置 Bank0、Bank1、Bank2、Bank3 电压为 LVCMOS18

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-077-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-077-image-02.jpg)

 在 Low Speed->Memory Interface 界面，勾选 QSPI 和 SD 0、SD 1；
QSPI：Dual Parallel、x4

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-078-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-078-image-02.jpg)

SD 0：MIO13..22、eMMC、8Bit、Reset MIO23
SD 1：MIO46..51、SD 2.0、4Bit、CD MIO45
 在 Low Speed->I/O Peripherals 界面，勾选 I2C 1、UART 0、UART 1；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-079-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-079-image-02.jpg)

在 Low Speed->Processing Uint 界面，勾选 TTC 0、TTC1、TTC 2、TTC 3；
在 High Speed 界面，勾选 GEM 3、USB 0 、USB3.0、PCIe、Display Port；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-080-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-080-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-081-image-01.jpg)

 在 Clock Configuration 窗口
按照下图配置输入时钟，其他默认即可；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-082-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-083-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-083-image-02.jpg)

 在 DDR Configuration 窗口，配置 DDR 的参数，如下图

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-084-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-084-image-02.jpg)

 在 PCIe Configuration 窗口，主要配置设备端口类型和设备 ID，其他默
认即可；
 在 PS-PL Configuration 页，配置如下。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-085-image-01.jpg)

14. 点击 OK
15. 选择 Tools->Validate Design，检查设置是否有错误
16. 在 system 上右键选择 Create HDL Wrapper

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-086-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-086-image-02.jpg)

17. 选择 Let Vivado manage wrapper and auto-update
18. 点击 Run Synthesis（这里我们只使用 PS 的资源，不用产生 bit）

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-087-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-087-image-02.jpg)

19. 综合完成之后，点击 OK
20. 选择 File->Export->Export Hardware

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-088-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-088-image-02.jpg)

21. 点击 Next
22. 这里我们没有 bit，默认配置，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-089-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-089-image-02.jpg)

23. 设置名称和路径，点击 Next
24. 点击 Finish

这里我们能看到新生成的 xsa 文件：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-090-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-090-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-090-image-03.jpg)

## 4.1.2 软件工程搭建

上篇我们在 vivado 下搭建好硬件工程，导出 xsa 文件。这里在工程目录下面
创建 vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis
2. 选择工作目录，点击 Launch

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-091-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-091-image-02.jpg)

3. 点击 Create Platform Project
4. 设置工程名称，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-092-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-092-image-02.jpg)

5. 点击 Browse..

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-093-image-01.jpg)

6. 选择之前生成的 xsa 文件，点击 Finish

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-094-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-094-image-02.jpg)

7. 在生成的 plf 上面右键，点击编译

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-095-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-095-image-02.jpg)

至此我们软件工程搭建完毕，后面在此基础上就可以进行 PS 裸机的实验；
