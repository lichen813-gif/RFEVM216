# 2. RFSOM216 核心板

[Switch to English](../../en/user-guide/02-som-board.md)

QSPI、eMMC 和 EEPROM 的可检索信号表格请参阅[管脚映射参考](04-pin-mapping.md#som-pin-mapping)。

- 按键

一个复位按键。

## 2.1 简介

RFSOM216 核心板的 ZYNQ 芯片是基于 XILINX 公司的 ZynqTM
UltraScale+TM RFSoC Gen3 系列 ZU49DR-2FSVF1760I。
这款核心板使用了 10 片 Micron 公司的 DDR4 芯片 MT40A512M16，其中
PS 端挂载 5 片 DDR4，组成带 ECC 功能的 64 位数据总线宽度。PL 端挂载 5 片
DDR4，组成 72 位数据总线宽度。每片 DDR4 容量为 1GB。DDR4 SDRAM 的最
高运行速度可达 1333MHz（数据速率 2666Mbps）。另外核心板上也集成了 1Gbit
大小的 QSPI FLASH 用于启动存储配置和系统文件。
为了和底板连接，这款核心板的 3 个 800Pin 的板对板连接器扩展出了 PS 端
的 USB3.0 接口、千兆以太网接口、SD 卡接口、M.2 接口、DP 接口以及剩余的
MIO 接口；以及 PL 端的 2 路 QSFP28 接口、FMC+扩展接口和其余扩展 IO。

![RFEVM216 用户手册图示](../../assets/user-guide/page-007-image-01.jpg)

图 2 RFSOM216 核心板正面
图 3 RFSOM216 核心板背面

## 2.2 ZYNQ 芯片

RFSOM216 核心板使用的是 Xilinx 公司的 ZynqTM UltraScale+TM RFSoC Gen3
系列的芯片，型号为 ZU49DR-2FSVF1760I。可编程逻辑部分的 FPGA 资源可提
供高吞吐量数字信号处理 (DSP) 和 IP 核，例如数字上/下变频 (DUC/DDC) 内
核。通过软件无线电开发架构应用程序编程接口和 FPGA 基础架构更容易实现
FPGA 加速。这有助于您快速启动和运行，以便您可以专注于增值 IP。用于快
速傅立叶变换 (FFT) 和有限脉冲响应 (FIR) 滤波器等常用功能的 FPGA 系统是
一个很好的起点。然后，您可以使用首选的硬件描述语言 (HDL) 将自己的 IP 块
添加到模块化架构中除了系统的 FPGA 架构部分，Xilinx UltraScale+ RFSoC 还
配备了四个板载应用处理单元 (APU) 和两个实时处理单元 (RPU)，适用于需要
板载嵌入式操作系统进行独立操作的应用。

![RFEVM216 用户手册图示](../../assets/user-guide/page-008-image-01.jpg)

图 4 RFSOM 硬件系统框图

## 2.3 DDR4 SDRAM

RFSOM216 核心板上配有 10 片 Micron（镁光）的 1GB 的 DDR4 芯片，型
号为 MT40A512M16LY-075E，其中 PS 端挂载了 5 片 DDR4，组成 64 为数据总
线带宽，带 ECC 功能。PL 端挂载 5 片 DDR4，组成 72 位数据总线带宽。PS 端
的 DDR4 SDRAM 的最高运行速度可达 1200MHz（数据速率 2400Mbps），5 片
DDR4 存储系统直接连接到了 PS 的 BANK504 的存储器接口上。PL 端的 DDR
SDRAM 的最高运行速度可达 1333MHz（数据速率 2666Mbps），5 片 DDR4 连
接到了 FPGA 的 BANK67、68、69 的接口上。PS 端和 PL 端 DDR4 SDRAM 的
具体配置如下表所示。
表 1 DDR4 SDRAM 配置
位置位号芯片型号容量厂家
PS UM1,UM2,UM5,UM6,UM9 MT40A512M16LY-075E 512x16bit Micron
PL UM3,UM4,UM7,UM8,UM10 MT40A512M16LY-075E 512x16bit Micron
PS 端的 DDR4 的硬件连接方式如下图所示：

![RFEVM216 用户手册图示](../../assets/user-guide/page-009-image-01.jpg)

图 5 PS 端 DDR4 SDRAM 连接示意图
PL 端的 DDR4 SDRAM 的硬件连接方式如下图所示：
图 6 PL 端 DDR4 SDRAM 连接示意图

![RFEVM216 用户手册图示](../../assets/user-guide/page-010-image-01.jpg)

![RFEVM216 用户手册图示](../../assets/user-guide/page-010-image-02.jpg)

## 2.4 QSPI FLASH

RFSOM216 核心板配有 2 片 512Mbit 大小的 QUAD SPI FLASH 芯片组成 8
位带宽数据总线，FLASH 型号为 MT25QU512ABBIEW9-0SIT ，它使用 1.8V
CMOS 电压标准。由于 QSPI FLASH 的非易失特性，在使用中，它可以作为系
统的启动设备来存储系统的启动镜像。这些镜像主要包括 FPGA 的 bit 文件、ARM
的应用程序代码以及它的用户数据文件。QSPI FLASH 的具体型号和相关特性见
下表。
表 2 QSPI FLASH 型号和参数
位置位号芯片型号容量厂家
PS U6,U7 MT25QU512ABBIEW9-0SIT 512M bit 镁光
QSPI FLASH 连接到 ZYNQ 芯片的 PS 部分 BANK500 的 MIO 上，在系统设
计中需要配置这些 PS 端的 MIO 功能为 QSPI FLASH 接口。
图 7 QSPI FLASH 连接示意图
表 3 配置芯片引脚分配
信号名称引脚名引脚号
SPIL_SCLK PS_MIO0 BB27
SPIL_MO1 PS_MIO1 BA27

![RFEVM216 用户手册图示](../../assets/user-guide/page-011-image-01.jpg)

SPIL_MO2 PS_MIO2 BB26
SPIL_MO3 PS_MIO3 BB28
SPIL_MO0 PS_MIO4 BA28
SPIL_CS PS_MIO5 BA29
SPIH_CS PS_MIO7 AY27
SPIH_MO0 PS_MIO8 AW27
SPIH_MO1 PS_MIO9 AW26
SPIH_MO2 PS_MIO10 AV26
SPIH_MO3 PS_MIO11 AW28
SPIH_SCLK PS_MIO12 AV28

## 2.5 eMMC Flash

RFSOM216 核心板上配有 1 片 8GB 的 eMMC FLASH 芯片 ， 型号为
MTFC8GLVEA-1MWT，电平标准支持 1.8V。eMMC FLASH 和 ZYNQ 连接的数
据宽度为 8bit。由于 eMMC FLASH 的大容量和非易失性，在 ZYNQ 系统使用中，
它可以作为系统大容量的存储设备，比如存储 ARM 的应用程序、系统文件以及
其它的用户数据文件。eMMC FLASH 的具体型号和相关参数见下表。
位置位号芯片型号容量厂家
PS U4 MTFC8GLVEA-1MWT 8GB 镁光
eMMC FLASH 连接到 ZYNQ 的 PS 部分 BANK500 的 MIO 上，在系统设计
中需要配置这些 PS 端的 MIO 功能为 EMMC 接口。eMMC Flash 在原理图中的
连接方式如下所示。
信号名称引脚名引脚号
EMMC_RST PS_MIO23 AM27
EMMC_CLK PS_MIO22 AL27
EMMC_CMD PS_MIO21 AN28
EMMC_IO0 PS_MIO13 AU26
EMMC_IO1 PS_MIO14 AU27
EMMC_IO2 PS_MIO15 AT27
EMMC_IO3 PS_MIO16 AU28
EMMC_IO4 PS_MIO17 AT28
EMMC_IO5 PS_MIO18 AP28
EMMC_IO6 PS_MIO19 AR27
EMMC_IO7 PS_MIO20 AP27

## 2.6 EEPROM

RFSOM216 核心模块上板载了一片 EEPROM，型号为 AT24CM01，容量为
1Mbit，通过 IIC 总线连接到 PS 端进行通信。

![RFEVM216 用户手册图示](../../assets/user-guide/page-013-image-01.jpg)

图 8 EEPROM 硬件原理图
表 4 EEPROM 引脚分配
信号名称引脚名引脚号备注
IIC_SCL PS_MIO24 AL28 I2C 时钟信号
IIC_SDA PS_MIO25 AM28 I2C 数据信号

## 2.7 时钟配置

核心模块上提供双晶振时钟，系统时钟默认使用 33.3333MHz 有源晶振，封
装 3.2x2.5mm。晶体 32.768KHz，驱动 RFSOC 内部 RTC 电路。时钟电路设计的
示意图如下图所示：

![RFEVM216 用户手册图示](../../assets/user-guide/page-014-image-01.jpg)

图 9 晶振原理图
核心模块系统采用 LMK04828 时钟芯片分配 ADC 和 DAC 模块所需时钟，
主晶振采用 96MHz 高稳 VCXO。支持外部参考时钟的单端输入与 SYSREF 差分
输入，可实现多模块并联形成更大规模相参射频通道。
图 10 时钟分配连接示意图

## 2.8 RF-ADC 接口

RFSOM 核心模块使用的 FPGA 芯片是 ZynqTM UltraScale+TM RFSoC Gen3 系

![RFEVM216 用户手册图示](../../assets/user-guide/page-015-image-01.jpg)

![RFEVM216 用户手册图示](../../assets/user-guide/page-015-image-02.jpg)

列业界唯一单芯片自适应无线电平台，芯片集成了 14-bit 的 RF-ADC，最大采样
率可达 2.5GSPS，并且 VCM 信号也引出至连接器。
图 11 RF-ADC 接口示意图

## 2.9 RF-DAC 接口

RFSOM 核心模块使用的 FPGA 芯片是 ZynqTM UltraScale+TM RFSoC Gen3 系
列业界唯一单芯片自适应无线电平台，芯片集成了 14-bit 的 RF-DAC，最大采样
率可达 9.85GSPS。
图 12 RF-DAC 接口示意图

## 2.10 高速板间连接器

核心板一共扩展出 3 个高速扩展口，使用 3 个 400Pin 的板间连接器（J1、

![RFEVM216 用户手册图示](../../assets/user-guide/page-016-image-01.jpg)

![RFEVM216 用户手册图示](../../assets/user-guide/page-016-image-02.jpg)

J2、J3）和底板连接，连接器使用 Samtec 公司的 ASP_230332-01 连接器,0.635mm
间距，插合高度 5mm，每个通道最高 32Gbps。

## 2.11 电源

RFSOM216 核心板采用直流 12V 供电，通过连接器底板给核心板供电。12V
系统电源通过降压型稳压器变换不同的电压驱动板卡上的 FPGA 以及其它电路，
板卡 ADC 与 DAC 的供电由线性低压 LDO 提供，具有较好的电源抑制（PSRR）。
核心模块的扩展 IO BANK 接口电平图下：
BANK 电平（V） 备注
BANK64 从底板提供,1.8V HP BANK
BANK65 从底板提供,1.8V HP BANK
BANK66 从底板提供,1.8V HP BANK
BANK67 1.2V 固定 DDR4 信号
BANK68 1.2V 固定 DDR4 信号
BANK69 1.2V 固定 DDR4 信号
BANK84 1.8V 固定 LMK04828 配置信号和输出
BANK87 从底板提供,3.3V HD BANK
BANK88 从底板提供,3.3V HD BANK
BANK89 从底板提供,3.3V HD BANK
BANK128 MGTY FMC+信号
BANK129 MGTY FMC+信号
BANK130 MGTY QSFP28 信号
BANK131 MGTY QSFP28 信号
BANK500 1.8V 固定 QSPI 和 EMMC 信号

![RFEVM216 用户手册图示](../../assets/user-guide/page-017-image-01.jpg)

BANK501 从底板提供 MIO BANK 支持 1.8V、2.5V，and 3.3V at ±5%
BANK502 从底板提供 MIO BANK 支持 1.8V、2.5V，and 3.3V at ±5%
BANK503 从底板提供 MIO BANK 支持 1.8V、2.5V，and 3.3V at ±5%
BANK505 PS_MGTR 高速信号管脚和时钟信号全部拉出至连接器
RFSOM 核心板的电源设计框图如下所示：
图 13 RFSOM 核心板电源设计框图

![RFEVM216 用户手册图示](../../assets/user-guide/page-018-image-01.jpg)

## 2.12 结构图

图 14 RFSOM216 核心模块正面图

![RFEVM216 用户手册图示](../../assets/user-guide/page-019-image-01.jpg)
