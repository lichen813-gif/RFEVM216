# 3. PL Peripherals

[Switch to 中文](../../zh/fpga-tutorial/03-pl-peripherals.md)

## 3.1 LED Breathing Light Experiment

The breathing light is an LED that is controlled by a microprocessor, gradually dimming, brightening, and then dimming again, imitating the way a person breathes.
The FPGA pin levels only have two states, '0' and '1'. Therefore, the breathing light is achieved by changing the duration of the high-level output within a unit of time on the pin, that is, making the FPGA pin output a series of PWM wave signals and continuously changing the duty cycle of the PWM wave to control the brightness of the LED.
The diagram of PWM duty cycle adjustment is shown below:
Figure 3 PWM Duty Cycle Diagram of Breathing Light

### 3.1.1 Hardware Design

The RFEVM216 development board has 4 user-controllable LED lights. Its schematic diagram is shown below:

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-011-image-01.jpg)

Figure 4 LED Lamp Hardware Schematic

### 3.1.2 Hardware Project Setup

1. On the PC, open Vivado
2. Click Create Project

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-012-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-012-image-02.jpg)

3. Click Next
4. Set the project name and location, then click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-013-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-013-image-02.jpg)

5. Click Next
6. Select FPGA model xczu49dr-fsvf1760-2-i, and click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-014-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-014-image-02.jpg)

7. Click Finish

Here we can see the project we created

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-015-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-015-image-02.jpg)

8. In the Flow Navigator window, click Add Source
9. Select the design files to add, then click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-016-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-016-image-02.jpg)

10. Click Create Files
11. Set the name, click OK

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-017-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-017-image-02.jpg)

12. Click Finish
13. Do not add a port for now, click OK

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-018-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-018-image-02.jpg)

Click Yes

14. After completion, you can see the .v file we newly created

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-019-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-019-image-02.jpg)

15. Double-click breath_led, then enter the following code

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-020-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-020-image-02.jpg)

16. Click Add Source

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-021-image-01.jpg)

17. Choose to add or create a constraint file, click Next
18. Click Create File

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-022-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-022-image-02.jpg)

19. Set the name, click OK
20. Click Finish

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-023-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-023-image-02.jpg)

21. Here you can see the newly created constraint file

Double-click rfevm_led.xdc and enter the following constraints:

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-024-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-024-image-02.jpg)

22. In the Flow Navigator, click Generate Bitstream
23. Click OK and wait for the bitstream to be generated

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-025-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-025-image-02.jpg)

24. After the bit generation is completed, select [View Reports] and click OK

### 3.1.3 Download Verification

Use a USB to Type-C cable, connect one end to the board and the other end to the PC, then power on the board.
In the Vivado interface, click Open Hardware Manager -> Open Target -> Auto Connect

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-026-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-026-image-02.jpg)

On the device, right-click and select Program device

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-027-image-01.jpg)

Click Program
After the download is complete, you can see the LEDs on the baseboard gradually changing from dim to bright, and then from bright to dim,
which produces a "breathing" effect.

## 3.2 PL Side DDR4 Read and Write Experiment

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-028-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-028-image-02.jpg)

DDR4 SDRAM (Double-Data-Rate Fourth Generation Synchronous Dynamic Random Access Memory) is a high-speed dynamic random-access memory. It belongs to the SDRAM family of memory products and offers higher operational performance and lower voltage compared to DDR3 SDRAM. Due to the very complex timing of DDR4, if DDR4 controller code is written directly, the workload is very large and performance is difficult to guarantee. It is worth mentioning that Vivado software comes with a DDR4 controller IP core, which allows users to perform DDR4 read and write operations directly using the IP core, greatly reducing the development difficulty of DDR4. In this experiment, the Xilinx MIG IP core will be used to implement DDR4 read and write operations.
MIG (Memory Interface Generator) is a free software tool used to generate memory controllers and interfaces for AMD FPGAs. The figure below is the structure diagram of the MIG IP core. The MIG IP core provides two sets of interfaces externally: the left side is the user interface, which the user must fully understand to operate the MIG; the right side is the DDR physical chip interface, responsible for generating specific operational timing and directly controlling the chip pins.
Figure 5 Structure Diagram of the MIG IP Core
Using this IP core, users can perform DDR4 read and write operations without needing to be familiar with the specific DDR4 read and write control timing.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-029-image-01.jpg)

### 3.2.1 Hardware Design

The PL side of the RFEVM216 development board has five 16-bit DDR4 chips, forming a 64-bit DDR4 channel with ECC functionality.
Figure 6 DDR4 Hardware Schematic

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-030-image-01.jpg)

Figure 7 DDR4 Pin Allocation Hardware Schematic

### 3.2.2 Hardware Engineering Setup

1. Open Vivado software
2. Select Create Project

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-031-image-01.jpg)

3. Click Next
4. Set the project name (rfevm216_pl_ddr4) and location (E:/rfevm216/), then click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-032-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-032-image-02.jpg)

5. Select the RTL project, click Next
6. Select the chip model xczu49dr-fsvf1760-2-i, click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-033-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-033-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-033-image-03.jpg)

7. Click Finish
8. In the Flow Navigator window, click IP Catalog
9. Select DDR4 SDRAM (MIG)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-034-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-034-image-02.jpg)

10. Under the Basic tab, make the following settings

 Memory Device Interface Speed (ps): 750
 Reference Input Clock Speed (ps): 8000 (125MHz)
 Memory Part: MT40A512M16LY-075
 Data Width: 72
 ECC: Enable
Keep other settings as default and click OK

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-035-image-01.jpg)

11. Click Generate

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-036-image-01.jpg)

12. Wait until ddr4_0_synth_1 shows a check mark
13. Add source code by clicking Add Sources, select Add or create design sources, and click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-037-image-01.jpg)

14. Click Add Files
15. Select the test file and click Finish

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-038-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-038-image-02.jpg)

16. Click IP Catalog

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-039-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-039-image-02.jpg)

17. Add ILA (Integrated Logic Analyzer) IP, configured as follows

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-040-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-040-image-02.jpg)

18. Click Generate

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-041-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-042-image-01.jpg)

19. Click Add Sources, select Add or create constraints to add a constraint file, and click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-043-image-01.jpg)

20. Click Create Files
21. Set the name of the xdc file and click OK

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-044-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-044-image-02.jpg)

22. Add DDR4 pin constraints
23. Click Generate Bitstream to generate the bit

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-045-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-045-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-046-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-046-image-02.jpg)

### 3.2.3 Download Verification

1. Click Open Hardware Manager -> Open Target -> Auto Connect

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-047-image-01.jpg)

2. Click Program device

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-048-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-048-image-02.jpg)

3. Just leave it as default and click Program
4. After the download is complete, the DDR4 calibration information and calibration status (CAL PASS) will be displayed in the MIG_1 window

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-049-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-049-image-02.jpg)

Debug signals can be viewed in the hw_ila_0 window

### 3.2.3 Reference Documents

 Zynq UltraScale Memory

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-050-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-050-image-02.jpg)

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

## 3.3 GTY Transceiver Bit Error Rate Test IBERT Experiment

IBERT (Integrated Bit Error Ratio Tester) is specifically designed by Xilinx for UltraScaleTM/UltraScale+TM architecture GTY transceivers to assess and monitor GTY transceivers. IBERT includes a pattern generator and checker implemented with FPGA logic and can access GTY transceiver ports and dynamic reconfiguration port attributes. It also includes communication logic that can be accessed at runtime via JTAG.
The IBERT tool is used for board-level hardware testing of Xilinx FPGA chips' high-speed serial transceivers. Using IBERT, the bit error rate can be obtained, eye diagrams can be observed, and transceiver parameters can be adjusted, which helps identify potential issues and facilitates the verification of hardware stability and signal integrity.

### 3.3.1 Hardware Introduction

To test BER and eye diagrams using IBERT, a transceiver loopback hardware is required. The development board has two QSFP28 fiber optic interfaces. In this experiment, the two QSFP28 fiber optic interfaces can be connected via 100G fiber to form a transceiver loopback link.
Figure 8 QSFP Hardware Schematic

### 3.3.2 Hardware Engineering Setup

1. Open Vivado
2. Select Create Project

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-052-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-052-image-02.jpg)

3. Click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-053-image-01.jpg)

4. Set the project name (ibert_bank_all) and location (E:/rfevm216/), then click Next
5. Select RTL project, then click Next

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-054-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-054-image-02.jpg)

6. Select the chip model xczu49dr-fsvf1760-2-i, click Next
7. Click Finish

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-055-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-055-image-02.jpg)

8. Click IP Catalog

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-056-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-056-image-02.jpg)

9. Select IBERT UltraScale GTY

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-057-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-057-image-02.jpg)

10. Double-click IBERT UltraScale GTY
11. Set module name: ibert_bank_all

● Under the 'Protocol Definition' tab:
Protocol Custom 1: LineRate 25, Refclk: 156.25, Quad Count: 2
● Under the 'Protocol Selection' tab:
QUAD_130: Custom 1/25 Gbps, MGTREFCLK1 130
QUAD_131: Custom 1/25 Gbps, MGTREFCLK1 131
● Under the 'Clock Settings' tab, set the clock

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-058-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-058-image-02.jpg)

 View the summary, and click 'OK'

12. Click 'Skip'

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-059-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-059-image-02.jpg)

 The generated IBERT IP appears in Design Sources

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-060-image-01.jpg)

13. Right-click ibert_bank_all and select Open IP Example Design ...

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-061-image-01.jpg)

14. Select a location and click OK
15. Create a new project

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-062-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-062-image-02.jpg)

16. Click Generate Bitstream
17. Click [OK] and wait for the bit to be generated

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-063-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-063-image-02.jpg)

18. After generating the bit, select [View Reports] and click OK

### 3.3.3 Download and Verification

1. Click Open Hardware Manager -> Open Target -> Auto Connect

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-064-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-064-image-02.jpg)

2. Select Program device
3. Bitstream file and LTX file default, click Program

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-065-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-065-image-02.jpg)

4. Click Create links
5. Select MGTX0Y12~MGTX0Y19 one by one, click the Add button, and then click OK

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-066-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-066-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-067-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-068-image-01.jpg)

6. Links will appear under the Serial I/O Links tab
7. Click BERT Reset to reset the link error counter, links will show no errors

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-069-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-069-image-02.jpg)

### 3.3.4 Reference Documents

 IBERT IP
IBERT for UltraScale GTY Transceivers - PG196
https://docs.xilinx.com/v/u/en-US/pg196-ibert-ultrascale-gty
 Vivado Programming and Debugging
Vivado Design Suite Programming and Debugging User Guide - UG908
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/
Introduction

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-070-image-01.jpg)
