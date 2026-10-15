# 1. Introduction and Workflow

[Switch to 中文](../../zh/rf-development-guide/01-introduction.md)

> This chapter is translated from the Chinese source PDF. Figures and UI screenshots retain their original labels so that they match the hardware and software.  
> Source PDF: `RFEVM216开发板射频开发指南s.pdf`  
> Source pages: 3-3

<a id="page-3"></a>
## Source PDF page 3

1 Introduction  
The RFEVM216 development board is an ideal RF test platform for out-of-the-box evaluation and cutting-edge application development. The development board includes the Zynq UltraScale+ RFSoC ZU49DR, which integrates RF direct-sampling data converters, FPGA logic, a complete ARM processor subsystem, and high-speed transceivers into a single chip. Compared to previous generations, the third-generation RFSoC device extends RF input and output frequency response to fully support bands below 6GHz, helping users develop advanced RF designs such as large-scale MIMO wireless, 5G baseband, fixed wireless access, test and measurement, and phased array radar.  

Key Features:  
- Integrated device of the ZU49DR RF System on Chip (RFSoC)
- Built-in digital up/down conversion and interpolation/decimation functions
- Supports 16 channels of 14-bit transmission and 16 channels of 14-bit reception
- Supports frequencies from 1MHz to 6GHz
- Supports interpolation/decimation factors of 1x, 2x, 3x, 4x, 5x, 6x, 8x, 10x, 12x, 16x, 20x, 24x, and 40x

2. FPGA Minimum System Setup  
This document mainly introduces the FPGA RF development process of the RFEVM216, including the following parts:  
• Introduction to the RFEVM216 RF hardware structure  
• RF data converter configuration guide  
• FPGA hardware project introduction  
• Bare-metal configuration process guide  

Through this reference example, users can understand the hardware composition and programming architecture of the system. For users doing FPGA development, they can use this FPGA project for secondary development to implement baseband data transmission over the air interface.
