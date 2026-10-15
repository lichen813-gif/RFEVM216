# 5. PS 与 PL 互联

[Switch to English](../../../en/fpga-tutorial/05-ps-pl-interconnect/index.md)

## 实验目录

- [5.1 PS 端 EMIO 的使用](01-emio.md)
- [5.2 PL 端 AXI GPIO 的使用](02-axi-gpio.md)
- [5.3 PS 端读写 PL 端的寄存器](03-pl-register-access.md)
- [5.4 AXI-DMA 环回测试](04-axi-dma-loopback.md)

## 章节概述

本章主要介绍 PS 与 PL 之间的互联，在开始之前，首先简要介绍 PS/PL 之
间的数据通路，具体请参考《ug1085 Zynq UltraScale+ Device Technical Reference
Manual》。
PS/PL 之间的数据通路主要是通用的 AXI Memory 接口，其中 PS 作为主设
备的接口有 128-bit 位宽的 HPM0/HPM1，64-bit 位宽的 LPD_PL；PL 作为主设
备的接口有 ACP/ACE/HPC0/HPC1/HP0/HP1/HP2/HP3。所有 AXI Memory 接口

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-160-image-01.jpg)

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
