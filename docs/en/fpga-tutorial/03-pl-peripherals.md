# 3. PL Peripherals

[Switch to 中文](../../zh/fpga-tutorial/03-pl-peripherals.md)

> This chapter is translated from the Chinese source PDF. Figures and UI screenshots retain their original labels so that they match the hardware and software.  
> Source PDF: `RFEVM216开发平台FPGA教程.pdf`  
> Source pages: 11-70

<a id="page-11"></a>
## Source PDF page 11

9 / 223  
3 PL Peripheral  
3.1 LED Breathing Light Experiment  
The breathing light is an LED that is controlled by a microprocessor, gradually dimming, brightening, and then dimming again, imitating the way a person breathes.  
The FPGA pin levels only have two states, '0' and '1'. Therefore, the breathing light is achieved by changing the duration of the high-level output within a unit of time on the pin, that is, making the FPGA pin output a series of PWM wave signals and continuously changing the duty cycle of the PWM wave to control the brightness of the LED.  
The diagram of PWM duty cycle adjustment is shown below:  
Figure 3 PWM Duty Cycle Diagram of Breathing Light  
3.1.1 Hardware Design  
The RFEVM216 development board has 4 user-controllable LED lights. Its schematic diagram is shown below:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 11, figure 1](../../assets/fpga-tutorial/page-011-image-01.jpg)

---

<a id="page-12"></a>
## Source PDF page 12

10 / 223  
Figure 4 LED Lamp Hardware Schematic  
3.1.2 Hardware Project Setup  
1) On the PC, open Vivado  
2) Click Create Project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 12, figure 1](../../assets/fpga-tutorial/page-012-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 12, figure 2](../../assets/fpga-tutorial/page-012-image-02.jpg)

---

<a id="page-13"></a>
## Source PDF page 13

11 / 223  
3) Click Next  
4) Set the project name and location, then click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 13, figure 1](../../assets/fpga-tutorial/page-013-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 13, figure 2](../../assets/fpga-tutorial/page-013-image-02.jpg)

---

<a id="page-14"></a>
## Source PDF page 14

12 / 223  
5) Click Next  
6) Select FPGA model xczu49dr-fsvf1760-2-i, and click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 14, figure 1](../../assets/fpga-tutorial/page-014-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 14, figure 2](../../assets/fpga-tutorial/page-014-image-02.jpg)

---

<a id="page-15"></a>
## Source PDF page 15

13 / 223  
7) Click Finish  
Here we can see the project we created

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 15, figure 1](../../assets/fpga-tutorial/page-015-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 15, figure 2](../../assets/fpga-tutorial/page-015-image-02.jpg)

---

<a id="page-16"></a>
## Source PDF page 16

14 / 223  
8) In the Flow Navigator window, click Add Source  
9) Select the design files to add, then click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 16, figure 1](../../assets/fpga-tutorial/page-016-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 16, figure 2](../../assets/fpga-tutorial/page-016-image-02.jpg)

---

<a id="page-17"></a>
## Source PDF page 17

15 / 223  
10) Click Create Files  
11) Set the name, click OK

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 17, figure 1](../../assets/fpga-tutorial/page-017-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 17, figure 2](../../assets/fpga-tutorial/page-017-image-02.jpg)

---

<a id="page-18"></a>
## Source PDF page 18

16 / 223  
12) Click Finish  
13) Do not add a port for now, click OK

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 18, figure 1](../../assets/fpga-tutorial/page-018-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 18, figure 2](../../assets/fpga-tutorial/page-018-image-02.jpg)

---

<a id="page-19"></a>
## Source PDF page 19

17 / 223  
Click Yes  
14) After completion, you can see the .v file we newly created

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 19, figure 1](../../assets/fpga-tutorial/page-019-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 19, figure 2](../../assets/fpga-tutorial/page-019-image-02.jpg)

---

<a id="page-20"></a>
## Source PDF page 20

18 / 223  
15) Double-click breath_led, then enter the following code

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 20, figure 1](../../assets/fpga-tutorial/page-020-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 20, figure 2](../../assets/fpga-tutorial/page-020-image-02.jpg)

---

<a id="page-21"></a>
## Source PDF page 21

19 / 223  
16) Click Add Source

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 21, figure 1](../../assets/fpga-tutorial/page-021-image-01.jpg)

---

<a id="page-22"></a>
## Source PDF page 22

20 / 223  
17) Choose to add or create a constraint file, click Next  
18) Click Create File

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 22, figure 1](../../assets/fpga-tutorial/page-022-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 22, figure 2](../../assets/fpga-tutorial/page-022-image-02.jpg)

---

<a id="page-23"></a>
## Source PDF page 23

21 / 223  
19) Set the name, click OK  
20) Click Finish

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 23, figure 1](../../assets/fpga-tutorial/page-023-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 23, figure 2](../../assets/fpga-tutorial/page-023-image-02.jpg)

---

<a id="page-24"></a>
## Source PDF page 24

22 / 223  
21) Here you can see the newly created constraint file  
Double-click rfevm_led.xdc and enter the following constraints:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 24, figure 1](../../assets/fpga-tutorial/page-024-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 24, figure 2](../../assets/fpga-tutorial/page-024-image-02.jpg)

---

<a id="page-25"></a>
## Source PDF page 25

23 / 223  
22) In the Flow Navigator, click Generate Bitstream  
23) Click OK and wait for the bitstream to be generated

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 25, figure 1](../../assets/fpga-tutorial/page-025-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 25, figure 2](../../assets/fpga-tutorial/page-025-image-02.jpg)

---

<a id="page-26"></a>
## Source PDF page 26

24 / 223  
24) After the bit generation is completed, select [View Reports] and click OK  
3.1.3 Download Verification  
Use a USB to Type-C cable, connect one end to the board and the other end to the PC, then power on the board.  
In the Vivado interface, click Open Hardware Manager -> Open Target -> Auto Connect

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 26, figure 1](../../assets/fpga-tutorial/page-026-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 26, figure 2](../../assets/fpga-tutorial/page-026-image-02.jpg)

---

<a id="page-27"></a>
## Source PDF page 27

25 / 223  
On the device, right-click and select Program device

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 27, figure 1](../../assets/fpga-tutorial/page-027-image-01.jpg)

---

<a id="page-28"></a>
## Source PDF page 28

26 / 223  
Click Program  
After the download is complete, you can see the LEDs on the baseboard gradually changing from dim to bright, and then from bright to dim,  
which produces a "breathing" effect.  
3.2 PL Side DDR4 Read and Write Experiment

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 28, figure 1](../../assets/fpga-tutorial/page-028-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 28, figure 2](../../assets/fpga-tutorial/page-028-image-02.jpg)

---

<a id="page-29"></a>
## Source PDF page 29

27 / 223  
DDR4 SDRAM (Double-Data-Rate Fourth Generation Synchronous Dynamic Random Access Memory) is a high-speed dynamic random-access memory. It belongs to the SDRAM family of memory products and offers higher operational performance and lower voltage compared to DDR3 SDRAM. Due to the very complex timing of DDR4, if DDR4 controller code is written directly, the workload is very large and performance is difficult to guarantee. It is worth mentioning that Vivado software comes with a DDR4 controller IP core, which allows users to perform DDR4 read and write operations directly using the IP core, greatly reducing the development difficulty of DDR4. In this experiment, the Xilinx MIG IP core will be used to implement DDR4 read and write operations.  
MIG (Memory Interface Generator) is a free software tool used to generate memory controllers and interfaces for AMD FPGAs. The figure below is the structure diagram of the MIG IP core. The MIG IP core provides two sets of interfaces externally: the left side is the user interface, which the user must fully understand to operate the MIG; the right side is the DDR physical chip interface, responsible for generating specific operational timing and directly controlling the chip pins.  
Figure 5 Structure Diagram of the MIG IP Core  
Using this IP core, users can perform DDR4 read and write operations without needing to be familiar with the specific DDR4 read and write control timing.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 29, figure 1](../../assets/fpga-tutorial/page-029-image-01.jpg)

---

<a id="page-30"></a>
## Source PDF page 30

28 / 223  
3.2.1 Hardware Design  
The PL side of the RFEVM216 development board has five 16-bit DDR4 chips, forming a 64-bit DDR4 channel with ECC functionality.  
Figure 6 DDR4 Hardware Schematic

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 30, figure 1](../../assets/fpga-tutorial/page-030-image-01.jpg)

---

<a id="page-31"></a>
## Source PDF page 31

29 / 223  
Figure 7 DDR4 Pin Allocation Hardware Schematic  
3.2.2 Hardware Engineering Setup  
1) Open Vivado software  
2) Select Create Project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 31, figure 1](../../assets/fpga-tutorial/page-031-image-01.jpg)

---

<a id="page-32"></a>
## Source PDF page 32

30 / 223  
3) Click Next  
4) Set the project name (rfevm216_pl_ddr4) and location (E:/rfevm216/), then click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 32, figure 1](../../assets/fpga-tutorial/page-032-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 32, figure 2](../../assets/fpga-tutorial/page-032-image-02.jpg)

---

<a id="page-33"></a>
## Source PDF page 33

31 / 223  
5) Select the RTL project, click Next  
6) Select the chip model xczu49dr-fsvf1760-2-i, click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 33, figure 1](../../assets/fpga-tutorial/page-033-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 33, figure 2](../../assets/fpga-tutorial/page-033-image-02.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 33, figure 3](../../assets/fpga-tutorial/page-033-image-03.jpg)

---

<a id="page-34"></a>
## Source PDF page 34

32 / 223  
7) Click Finish  
8) In the Flow Navigator window, click IP Catalog  
9) Select DDR4 SDRAM (MIG)

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 34, figure 1](../../assets/fpga-tutorial/page-034-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 34, figure 2](../../assets/fpga-tutorial/page-034-image-02.jpg)

---

<a id="page-35"></a>
## Source PDF page 35

10) Under the Basic tab, make the following settings  
 Memory Device Interface Speed (ps): 750  
 Reference Input Clock Speed (ps): 8000 (125MHz)  
 Memory Part: MT40A512M16LY-075  
 Data Width: 72  
 ECC: Enable  
Keep other settings as default and click OK

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 35, figure 1](../../assets/fpga-tutorial/page-035-image-01.jpg)

---

<a id="page-36"></a>
## Source PDF page 36

34 / 223  
11) Click Generate

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 36, figure 1](../../assets/fpga-tutorial/page-036-image-01.jpg)

---

<a id="page-37"></a>
## Source PDF page 37

35 / 223  
12) Wait until ddr4_0_synth_1 shows a check mark  
13) Add source code by clicking Add Sources, select Add or create design sources, and click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 37, figure 1](../../assets/fpga-tutorial/page-037-image-01.jpg)

---

<a id="page-38"></a>
## Source PDF page 38

36 / 223  
14) Click Add Files  
15) Select the test file and click Finish

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 38, figure 1](../../assets/fpga-tutorial/page-038-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 38, figure 2](../../assets/fpga-tutorial/page-038-image-02.jpg)

---

<a id="page-39"></a>
## Source PDF page 39

37 / 223  
16) Click IP Catalog

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 39, figure 1](../../assets/fpga-tutorial/page-039-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 39, figure 2](../../assets/fpga-tutorial/page-039-image-02.jpg)

---

<a id="page-40"></a>
## Source PDF page 40

38 / 223  
17) Add ILA (Integrated Logic Analyzer) IP, configured as follows

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 40, figure 1](../../assets/fpga-tutorial/page-040-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 40, figure 2](../../assets/fpga-tutorial/page-040-image-02.jpg)

---

<a id="page-41"></a>
## Source PDF page 41

39 / 223  
18) Click Generate

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 41, figure 1](../../assets/fpga-tutorial/page-041-image-01.jpg)

---

<a id="page-42"></a>
## Source PDF page 42

40 / 223

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 42, figure 1](../../assets/fpga-tutorial/page-042-image-01.jpg)

---

<a id="page-43"></a>
## Source PDF page 43

41 / 223 19) Click Add Sources, select Add or create constraints to add a constraint file, and click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 43, figure 1](../../assets/fpga-tutorial/page-043-image-01.jpg)

---

<a id="page-44"></a>
## Source PDF page 44

42 / 223  
20) Click Create Files  
21) Set the name of the xdc file and click OK

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 44, figure 1](../../assets/fpga-tutorial/page-044-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 44, figure 2](../../assets/fpga-tutorial/page-044-image-02.jpg)

---

<a id="page-45"></a>
## Source PDF page 45

43 / 223  
22) Add DDR4 pin constraints  
23) Click Generate Bitstream to generate the bit

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 45, figure 1](../../assets/fpga-tutorial/page-045-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 45, figure 2](../../assets/fpga-tutorial/page-045-image-02.jpg)

---

<a id="page-46"></a>
## Source PDF page 46

44 / 223

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 46, figure 1](../../assets/fpga-tutorial/page-046-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 46, figure 2](../../assets/fpga-tutorial/page-046-image-02.jpg)

---

<a id="page-47"></a>
## Source PDF page 47

45 / 223  
3.2.3 Download Verification  
1) Click Open Hardware Manager -> Open Target -> Auto Connect

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 47, figure 1](../../assets/fpga-tutorial/page-047-image-01.jpg)

---

<a id="page-48"></a>
## Source PDF page 48

46 / 223  
2) Click Program device

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 48, figure 1](../../assets/fpga-tutorial/page-048-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 48, figure 2](../../assets/fpga-tutorial/page-048-image-02.jpg)

---

<a id="page-49"></a>
## Source PDF page 49

3) Just leave it as default and click Program  
4) After the download is complete, the DDR4 calibration information and calibration status (CAL PASS) will be displayed in the MIG_1 window

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 49, figure 1](../../assets/fpga-tutorial/page-049-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 49, figure 2](../../assets/fpga-tutorial/page-049-image-02.jpg)

---

<a id="page-50"></a>
## Source PDF page 50

48 / 223  
Debug signals can be viewed in the hw_ila_0 window  
3.2.3 Reference Documents  
 Zynq UltraScale Memory

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 50, figure 1](../../assets/fpga-tutorial/page-050-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 50, figure 2](../../assets/fpga-tutorial/page-050-image-02.jpg)

---

<a id="page-51"></a>
## Source PDF page 51

49 / 223  
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
3.3 GTY Transceiver Bit Error Rate Test IBERT Experiment  
IBERT (Integrated Bit Error Ratio Tester) is specifically designed by Xilinx for UltraScaleTM/UltraScale+TM architecture GTY transceivers to assess and monitor GTY transceivers. IBERT includes a pattern generator and checker implemented with FPGA logic and can access GTY transceiver ports and dynamic reconfiguration port attributes. It also includes communication logic that can be accessed at runtime via JTAG.  
The IBERT tool is used for board-level hardware testing of Xilinx FPGA chips' high-speed serial transceivers. Using IBERT, the bit error rate can be obtained, eye diagrams can be observed, and transceiver parameters can be adjusted, which helps identify potential issues and facilitates the verification of hardware stability and signal integrity.  
3.3.1 Hardware Introduction  

To test BER and eye diagrams using IBERT, a transceiver loopback hardware is required. The development board has two QSFP28 fiber optic interfaces. In this experiment, the two QSFP28 fiber optic interfaces can be connected via 100G fiber to form a transceiver loopback link.

---

<a id="page-52"></a>
## Source PDF page 52

50 / 223  
Figure 8 QSFP Hardware Schematic  
3.3.2 Hardware Engineering Setup  
1) Open Vivado  
2) Select Create Project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 52, figure 1](../../assets/fpga-tutorial/page-052-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 52, figure 2](../../assets/fpga-tutorial/page-052-image-02.jpg)

---

<a id="page-53"></a>
## Source PDF page 53

51 / 223  
3) Click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 53, figure 1](../../assets/fpga-tutorial/page-053-image-01.jpg)

---

<a id="page-54"></a>
## Source PDF page 54

52 / 223  
4) Set the project name (ibert_bank_all) and location (E:/rfevm216/), then click Next  
5) Select RTL project, then click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 54, figure 1](../../assets/fpga-tutorial/page-054-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 54, figure 2](../../assets/fpga-tutorial/page-054-image-02.jpg)

---

<a id="page-55"></a>
## Source PDF page 55

53 / 223  
6) Select the chip model xczu49dr-fsvf1760-2-i, click Next  
7) Click Finish

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 55, figure 1](../../assets/fpga-tutorial/page-055-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 55, figure 2](../../assets/fpga-tutorial/page-055-image-02.jpg)

---

<a id="page-56"></a>
## Source PDF page 56

54 / 223  
8) Click IP Catalog

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 56, figure 1](../../assets/fpga-tutorial/page-056-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 56, figure 2](../../assets/fpga-tutorial/page-056-image-02.jpg)

---

<a id="page-57"></a>
## Source PDF page 57

55 / 223  
9) Select IBERT UltraScale GTY

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 57, figure 1](../../assets/fpga-tutorial/page-057-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 57, figure 2](../../assets/fpga-tutorial/page-057-image-02.jpg)

---

<a id="page-58"></a>
## Source PDF page 58

56 / 223  
10) Double-click IBERT UltraScale GTY  
11) Set module name: ibert_bank_all  
● Under the 'Protocol Definition' tab:  
Protocol Custom 1: LineRate 25, Refclk: 156.25, Quad Count: 2  
● Under the 'Protocol Selection' tab:  
QUAD_130: Custom 1/25 Gbps, MGTREFCLK1 130  
QUAD_131: Custom 1/25 Gbps, MGTREFCLK1 131  
● Under the 'Clock Settings' tab, set the clock

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 58, figure 1](../../assets/fpga-tutorial/page-058-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 58, figure 2](../../assets/fpga-tutorial/page-058-image-02.jpg)

---

<a id="page-59"></a>
## Source PDF page 59

57 / 223  
 View the summary, and click 'OK'  
12) Click 'Skip'

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 59, figure 1](../../assets/fpga-tutorial/page-059-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 59, figure 2](../../assets/fpga-tutorial/page-059-image-02.jpg)

---

<a id="page-60"></a>
## Source PDF page 60

58 / 223  
 The generated IBERT IP appears in Design Sources

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 60, figure 1](../../assets/fpga-tutorial/page-060-image-01.jpg)

---

<a id="page-61"></a>
## Source PDF page 61

59 / 223  
13) Right-click ibert_bank_all and select Open IP Example Design ...

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 61, figure 1](../../assets/fpga-tutorial/page-061-image-01.jpg)

---

<a id="page-62"></a>
## Source PDF page 62

60 / 223  
14) Select a location and click OK  
15) Create a new project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 62, figure 1](../../assets/fpga-tutorial/page-062-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 62, figure 2](../../assets/fpga-tutorial/page-062-image-02.jpg)

---

<a id="page-63"></a>
## Source PDF page 63

61 / 223  
16) Click Generate Bitstream  
17) Click [OK] and wait for the bit to be generated

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 63, figure 1](../../assets/fpga-tutorial/page-063-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 63, figure 2](../../assets/fpga-tutorial/page-063-image-02.jpg)

---

<a id="page-64"></a>
## Source PDF page 64

62 / 223  
18) After generating the bit, select [View Reports] and click OK  
3.3.3 Download and Verification  
1) Click Open Hardware Manager -> Open Target -> Auto Connect

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 64, figure 1](../../assets/fpga-tutorial/page-064-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 64, figure 2](../../assets/fpga-tutorial/page-064-image-02.jpg)

---

<a id="page-65"></a>
## Source PDF page 65

63 / 223  
2) Select Program device  
3) Bitstream file and LTX file default, click Program

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 65, figure 1](../../assets/fpga-tutorial/page-065-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 65, figure 2](../../assets/fpga-tutorial/page-065-image-02.jpg)

---

<a id="page-66"></a>
## Source PDF page 66

64 / 223  
4) Click Create links  
5) Select MGTX0Y12~MGTX0Y19 one by one, click the Add button, and then click OK

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 66, figure 1](../../assets/fpga-tutorial/page-066-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 66, figure 2](../../assets/fpga-tutorial/page-066-image-02.jpg)

---

<a id="page-67"></a>
## Source PDF page 67

65 / 223

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 67, figure 1](../../assets/fpga-tutorial/page-067-image-01.jpg)

---

<a id="page-68"></a>
## Source PDF page 68

66 / 223

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 68, figure 1](../../assets/fpga-tutorial/page-068-image-01.jpg)

---

<a id="page-69"></a>
## Source PDF page 69

67 / 223  
6) Links will appear under the Serial I/O Links tab  
7) Click BERT Reset to reset the link error counter, links will show no errors

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 69, figure 1](../../assets/fpga-tutorial/page-069-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 69, figure 2](../../assets/fpga-tutorial/page-069-image-02.jpg)

---

<a id="page-70"></a>
## Source PDF page 70

68 / 223  
3.3.4 Reference Documents  
 IBERT IP  
IBERT for UltraScale GTY Transceivers - PG196  
https://docs.xilinx.com/v/u/en-US/pg196-ibert-ultrascale-gty  
 Vivado Programming and Debugging  
Vivado Design Suite Programming and Debugging User Guide - UG908  
https://docs.xilinx.com/r/2021.2-English/ug908-vivado-programming-debugging/  
Introduction

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 70, figure 1](../../assets/fpga-tutorial/page-070-image-01.jpg)
