# 1. Introduction

[Switch to 中文](../../zh/user-guide/01-introduction.md)

> This chapter is translated from the Chinese source PDF. Figures and UI screenshots retain their original labels so that they match the hardware and software.  
> Source PDF: `RFEVM216_UG.pdf`  
> Source pages: 5-6

<a id="page-5"></a>
## Source PDF page 5

1 Introduction  
The RFEVM216 development board consists of the RFSOM216 SoM board and a carrier board, connected via a high-speed board-to-board connector.  
The RFSOM216 SoM board uses the Zynq chip, which is Xilinx's ZynqTM UltraScale+TM RFSoC Gen3 series ZU49DR FPGA main chip. It supports 16 channels of 14-bit RF-ADC with a maximum sampling rate of 2.5 GSPS and 16 channels of 14-bit RF-DAC with a maximum sampling rate of 9.85 GSPS. It can reduce the complexity of the RF signal processing chain, maximize input/output channel density without sacrificing bandwidth, leverage heterogeneous processing capabilities, and consume lower power (by eliminating ADC/DAC components and removing the FPGA-to-analog interface power consumption). The Zynq UltraScale+ device provides an ARM Cortex-A53 processing subsystem, UltraScale+ programmable logic, and maximum signal processing bandwidth, offering a comprehensive RF signal chain suitable for wireless, cable TV access, test and measurement, early warning/radar, and other high-performance RF applications.  
The RFSOM216 SoM board uses 10 Micron DDR4 chips MT40A512M16LY, with 5 chips on the PS side forming a 64-bit data bus with ECC functionality, and 5 chips on the PL side forming a 72-bit data bus. The SoM board also integrates 1 Gb QSPI flash and 8 GB EMMC for boot storage configuration and system files.  
The carrier board extends a variety of peripheral interfaces for the SoM board, which primarily include 1 M.2 NVMe interface, 1 USB3.0 interface, 1 Gigabit Ethernet interface, 1 JTAG/UART interface, 1 TF card interface, 1 FMC+ expansion interface, and 2 QSFP28 interfaces.  
The following diagram illustrates the structure of the entire development system:

### Figures

![RFEVM216 User Guide, page 5, figure 1](../../assets/user-guide/page-005-image-01.jpg)

---

<a id="page-6"></a>
## Source PDF page 6

Figure 1 RFEVM216 Development Board  
Through this schematic, we can see the interfaces and functions that the RFEVM216 development platform can include.  
- RFSOM216 Core Board
Consists of ZU49DR + 4GB DDR4 (PS) + 4GB DDR4 (PL) + 1Gb QSPI Flash + 8GB eMMC. Additionally, the core module provides dual crystal oscillator clock sources: a single-ended 33.3333MHz active crystal oscillator for the PS system, and a 32.76KHz crystal driving the internal RTC circuit of the RFSOC.  
- M.2 Interface
One PCIe x2 standard M.2 interface, used to connect an M.2 SSD.  
- USB3.0 Interface
One USB3.0 interface, supporting HOST and SLAVE three modes.  
- Gigabit Ethernet Interface
One 10M/100M/1000M Ethernet RJ45 interface, used for Ethernet data exchange with computers or other network devices.  
- JTAG & UART Interface
JTAG & UART debug interface is a Type-C interface. JTAG and UART share this interface, used for FPGA program download and debugging.  
- Micro SD Card Slot
One Micro SD card slot, used to store the operating system image and file system.  
- FMC+ Expansion Interface
One FMC+ expansion interface, used to extend other FMC daughter cards.  
- QSFP28 Optical Interfaces
Two QSFP28 optical interfaces, supporting 40G/100G communication rates.  
- Expansion IO
Three sets of expansion IO, two sets of PL-side expansion IO, one set of PS-side expansion IO, available for user custom use.  
- LED Lights
Four extendable LED pin headers, available for user custom use.  
- Board-to-Board and Mid-layer Connectors
Two sets of 80P 5mm board-to-board and mid-layer connectors.
