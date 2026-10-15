# 3.3 GTY Transceiver Bit Error Rate Test IBERT Experiment

[Switch to 中文](../../../zh/fpga-tutorial/03-pl-peripherals/03-gty-ibert.md)

[Back to chapter overview](index.md)

IBERT (Integrated Bit Error Ratio Tester) is specifically designed by Xilinx for UltraScaleTM/UltraScale+TM architecture GTY transceivers to assess and monitor GTY transceivers. IBERT includes a pattern generator and checker implemented with FPGA logic and can access GTY transceiver ports and dynamic reconfiguration port attributes. It also includes communication logic that can be accessed at runtime via JTAG.
The IBERT tool is used for board-level hardware testing of Xilinx FPGA chips' high-speed serial transceivers. Using IBERT, the bit error rate can be obtained, eye diagrams can be observed, and transceiver parameters can be adjusted, which helps identify potential issues and facilitates the verification of hardware stability and signal integrity.

## 3.3.1 Hardware Introduction

To test BER and eye diagrams using IBERT, a transceiver loopback hardware is required. The development board has two QSFP28 fiber optic interfaces. In this experiment, the two QSFP28 fiber optic interfaces can be connected via 100G fiber to form a transceiver loopback link.
Figure 8 QSFP Hardware Schematic

## 3.3.2 Hardware Engineering Setup

1. Open Vivado
2. Select Create Project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-052-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-052-image-02.jpg)

3. Click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-053-image-01.jpg)

4. Set the project name (ibert_bank_all) and location (E:/rfevm216/), then click Next
5. Select RTL project, then click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-054-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-054-image-02.jpg)

6. Select the chip model xczu49dr-fsvf1760-2-i, click Next
7. Click Finish

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-055-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-055-image-02.jpg)

8. Click IP Catalog

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-056-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-056-image-02.jpg)

9. Select IBERT UltraScale GTY

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-057-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-057-image-02.jpg)

10. Double-click IBERT UltraScale GTY
11. Set module name: ibert_bank_all

● Under the 'Protocol Definition' tab:
Protocol Custom 1: LineRate 25, Refclk: 156.25, Quad Count: 2
● Under the 'Protocol Selection' tab:
QUAD_130: Custom 1/25 Gbps, MGTREFCLK1 130
QUAD_131: Custom 1/25 Gbps, MGTREFCLK1 131
● Under the 'Clock Settings' tab, set the clock

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-058-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-058-image-02.jpg)

 View the summary, and click 'OK'

12. Click 'Skip'

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-059-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-059-image-02.jpg)

 The generated IBERT IP appears in Design Sources

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-060-image-01.jpg)

13. Right-click ibert_bank_all and select Open IP Example Design ...

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-061-image-01.jpg)

14. Select a location and click OK
15. Create a new project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-062-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-062-image-02.jpg)

16. Click Generate Bitstream
17. Click [OK] and wait for the bit to be generated

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-063-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-063-image-02.jpg)

18. After generating the bit, select [View Reports] and click OK

## 3.3.3 Download and Verification

1. Click Open Hardware Manager -> Open Target -> Auto Connect

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-064-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-064-image-02.jpg)

2. Select Program device
3. Bitstream file and LTX file default, click Program

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-065-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-065-image-02.jpg)

4. Click Create links
5. Select MGTX0Y12~MGTX0Y19 one by one, click the Add button, and then click OK

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-066-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-066-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-067-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-068-image-01.jpg)

6. Links will appear under the Serial I/O Links tab
7. Click BERT Reset to reset the link error counter, links will show no errors

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-069-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-069-image-02.jpg)

## 3.3.4 Reference Documents

 IBERT IP
IBERT for UltraScale GTY Transceivers - PG196
https://docs.xilinx.com/v/u/en-US/pg196-ibert-ultrascale-gty
 Vivado Programming and Debugging
Vivado Design Suite Programming and Debugging User Guide - UG908
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/
Introduction

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-070-image-01.jpg)
