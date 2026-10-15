# 1. 开发板简介

[Switch to English](../../en/fpga-tutorial/01-board-introduction.md)

RFEVM216 开发板由 RFSOM216 核心板和载板构成，核心板和载板之间使
用高速板间连接器连接。
RFSOM216 核心板采用 Xilinx 公司的 ZynqTM UltraScale+TM RFSoc Gen3 系列
ZU49DR FPGA 主芯片，它支持 16 路 14 位 RF-ADC，最大采样率可达 2.5GSPS，
16 路 14 位 RF-DAC，最高采样率可达 9.85GSPS 。可以降低 RF 信号处理链的
复杂性，最大化输入/输出通道密度，而不会牺牲宽带并利用异构处理能力，并
且拥有更低的功耗（取消了 ADC/DAC 组件，消除了 FPGA 至模拟的接口功耗）。
Zynq UltraScale+ 器件中提供 ARM 4 核 Cortex-A53 处理子系统 、 双核
Cortex-R5F、UltraScale+可编程逻辑，能够提供综合 RF 信号链，满足无线、有
线电视接入、测试测量、早期预警/雷达以及其它高性能 RF 应用需求。
载板为核心板扩展了丰富的外围接口，其中包含一路 USB3.0 接口、1 路千
兆以太网接口、一路 JTAG/UART 接口、一路 TF 卡接口、2 路 QSFP 4G 光纤接
口。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-007-image-01.jpg)

图 1 RFEVM216 开发板实物图
下图为整个开发系统的结构示意图：
图 2 RFEVM216 开发板
通过这个示意图，我们可以看到 RFEVM 开发平台所能包含的接口和功能。

- RFSOM216 核心板

由 ZU49DR+4GB DDR4（PS 带 ECC）+4GB DDR4（PL 带 ECC）+1Gb QSPI
Flash 组成，另外核心模块提供双晶振时钟源，一个单端 33.3333MHz 有源晶振
提供给 PS 系统，一个晶体 32.76MHz 驱动 RFSOC 内部 RTC 电路。

- M.2 接口

一路 PCIe x2 标准的 M.2 接口，用于连接 M.2 的 SSD 固态硬盘

- USB3.0 接口

一路 USB3.0 接口，支持 HOST、SLAVE 三种模式。

- 千兆以太网接口

一路 10M/100M/1000M 以太网 RJ45 接口，用于和电脑或者其它网络设备行
以太网数据交换。

- JTAG&UART 接口

JTAG&UART 调试接口类型为 Type-C 接口，JTAG 和 UART 共用此接口，用
于 FPGA 程序的下载和调试。

- Micro SD 卡座

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-008-image-01.jpg)

一路 Micro SD 卡座，用于存储操作系统镜像和文件系统。

- QSFP 28 光纤接口

2 路 QSFP 28 光纤接口。

- 扩展 IO

三组扩展 IO，两组 PL 端扩展 IO，一组 PS 端扩展 IO，可供用户自定义使用。

- LED 灯

4 个可扩展的 LED 直插针座，供用户自定义使用。

- FMC+

一个 FMC+连接器可以连接扩展子卡。

- MINI_DP

一个 MINI_DP 的接口。

- 按键

一个复位按键。
