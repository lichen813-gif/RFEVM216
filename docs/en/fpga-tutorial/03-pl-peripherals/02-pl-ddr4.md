# 3.2 PL Side DDR4 Read and Write Experiment

[Switch to 中文](../../../zh/fpga-tutorial/03-pl-peripherals/02-pl-ddr4.md)

[Back to chapter overview](index.md)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-028-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-028-image-02.jpg)

DDR4 SDRAM (Double-Data-Rate Fourth Generation Synchronous Dynamic Random Access Memory) is a high-speed dynamic random-access memory. It belongs to the SDRAM family of memory products and offers higher operational performance and lower voltage compared to DDR3 SDRAM. Due to the very complex timing of DDR4, if DDR4 controller code is written directly, the workload is very large and performance is difficult to guarantee. It is worth mentioning that Vivado software comes with a DDR4 controller IP core, which allows users to perform DDR4 read and write operations directly using the IP core, greatly reducing the development difficulty of DDR4. In this experiment, the Xilinx MIG IP core will be used to implement DDR4 read and write operations.
MIG (Memory Interface Generator) is a free software tool used to generate memory controllers and interfaces for AMD FPGAs. The figure below is the structure diagram of the MIG IP core. The MIG IP core provides two sets of interfaces externally: the left side is the user interface, which the user must fully understand to operate the MIG; the right side is the DDR physical chip interface, responsible for generating specific operational timing and directly controlling the chip pins.
Figure 5 Structure Diagram of the MIG IP Core
Using this IP core, users can perform DDR4 read and write operations without needing to be familiar with the specific DDR4 read and write control timing.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-029-image-01.jpg)

## 3.2.1 Hardware Design

The PL side of the RFEVM216 development board has five 16-bit DDR4 chips, forming a 64-bit DDR4 channel with ECC functionality.
Figure 6 DDR4 Hardware Schematic

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-030-image-01.jpg)

Figure 7 DDR4 Pin Allocation Hardware Schematic

## 3.2.2 Hardware Engineering Setup

1. Open Vivado software
2. Select Create Project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-031-image-01.jpg)

3. Click Next
4. Set the project name (rfevm216_pl_ddr4) and location (E:/rfevm216/), then click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-032-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-032-image-02.jpg)

5. Select the RTL project, click Next
6. Select the chip model xczu49dr-fsvf1760-2-i, click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-033-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-033-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-033-image-03.jpg)

7. Click Finish
8. In the Flow Navigator window, click IP Catalog
9. Select DDR4 SDRAM (MIG)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-034-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-034-image-02.jpg)

10. Under the Basic tab, make the following settings

 Memory Device Interface Speed (ps): 750
 Reference Input Clock Speed (ps): 8000 (125MHz)
 Memory Part: MT40A512M16LY-075
 Data Width: 72
 ECC: Enable
Keep other settings as default and click OK

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-035-image-01.jpg)

11. Click Generate

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-036-image-01.jpg)

12. Wait until ddr4_0_synth_1 shows a check mark
13. Add source code by clicking Add Sources, select Add or create design sources, and click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-037-image-01.jpg)

14. Click Add Files
15. Select the test file and click Finish

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-038-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-038-image-02.jpg)

16. Click IP Catalog

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-039-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-039-image-02.jpg)

17. Add ILA (Integrated Logic Analyzer) IP, configured as follows

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-040-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-040-image-02.jpg)

18. Click Generate

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-041-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-042-image-01.jpg)

19. Click Add Sources, select Add or create constraints to add a constraint file, and click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-043-image-01.jpg)

20. Click Create Files
21. Set the name of the xdc file and click OK

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-044-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-044-image-02.jpg)

22. Add DDR4 pin constraints
23. Click Generate Bitstream to generate the bit

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-045-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-045-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-046-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-046-image-02.jpg)

## 3.2.3 Download Verification

1. Click Open Hardware Manager -> Open Target -> Auto Connect

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-047-image-01.jpg)

2. Click Program device

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-048-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-048-image-02.jpg)

3. Just leave it as default and click Program
4. After the download is complete, the DDR4 calibration information and calibration status (CAL PASS) will be displayed in the MIG_1 window

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-049-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-049-image-02.jpg)

Debug signals can be viewed in the hw_ila_0 window

## 3.2.3 Reference Documents

 Zynq UltraScale Memory

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-050-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-050-image-02.jpg)

UltraScale FPGA Memory Interface Solutions Product Guide - PG150
https://docs.xilinx.com/v/u/en-US/pg150-ultrascale-memory-ip
 Vivado Programming and Debugging
Vivado Design Suite Programming and Debugging User Guide - UG908
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/
Introduction
 ILA
Integrated Logic Analyzer Product Guide - PG172
https://docs.xilinx.com/v/u/en-US/pg172-ila
 DDR4-MT40A512M16
https://pdf1.alldatasheet.com/datasheet-pdf/view/928163/MICRON/MT40A512M16.html
