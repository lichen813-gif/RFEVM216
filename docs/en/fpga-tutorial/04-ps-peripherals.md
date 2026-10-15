# 4. PS Peripherals

[Switch to 中文](../../zh/fpga-tutorial/04-ps-peripherals.md)

> This chapter is translated from the Chinese source PDF. Figures and UI screenshots retain their original labels so that they match the hardware and software.  
> Source PDF: `RFEVM216开发平台FPGA教程.pdf`  
> Source pages: 71-159

<a id="page-71"></a>
## Source PDF page 71

69 / 223  
4 PS End Peripherals  
This chapter mainly introduces the configuration of the Zynq core and the application of PS end peripherals, such as basic experiments with MIO, UART, Ethernet, and RTC.  
The previous experiments were all conducted on the PL side, which can be seen to have no difference from the ordinary FPGA development process. The main advantage of Zynq is the reasonable combination of FPGA and ARM, which places higher demands on developers. From this chapter onwards, we start using ARM, which is what we refer to as PS.  

4.1 IPI Design Creation  
Vivado IP Integrator (IPI) is an IP integration design interface provided by the Vivado integrated development environment. The IP Integrator is a graphical design and development environment that supports script configuration and connection. In the IP Integrator, IP can be used for processor-based designs as well as non-processor pure logic design development.  

Here, we enable all PS peripherals in the IPI; subsequent PS peripheral experiments only need to be operated under Vitis.  

4.1.1 Hardware Project Setup  
1) Open Vivado  
2) Select Create Project

---

<a id="page-72"></a>
## Source PDF page 72

70 / 223  
3) Click Next  
4) Set the project name (rfevm216_ipi) and location (E:/rfevm216/demo), then click Next;

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 72, figure 1](../../assets/fpga-tutorial/page-072-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 72, figure 2](../../assets/fpga-tutorial/page-072-image-02.jpg)

---

<a id="page-73"></a>
## Source PDF page 73

71 / 223  
5) Select RTL Project, click Next  
6) Select chip model xczu49dr-fsvf1760-2-i, click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 73, figure 1](../../assets/fpga-tutorial/page-073-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 73, figure 2](../../assets/fpga-tutorial/page-073-image-02.jpg)

---

<a id="page-74"></a>
## Source PDF page 74

72 / 223  
7) Click Finish  
8) Under IPI (IP INTEGRATOR) select Create Block Design

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 74, figure 1](../../assets/fpga-tutorial/page-074-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 74, figure 2](../../assets/fpga-tutorial/page-074-image-02.jpg)

---

<a id="page-75"></a>
## Source PDF page 75

73 / 223  
9) Set the design name: system, click OK  
10) Click + (Add IP)

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 75, figure 1](../../assets/fpga-tutorial/page-075-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 75, figure 2](../../assets/fpga-tutorial/page-075-image-02.jpg)

---

<a id="page-76"></a>
## Source PDF page 76

74 / 223  
11) Select Zynq UltraScale+ MPSoC  
12) Double-click Zynq UltraScale+ MPSoC or right-click and choose Customize Block...

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 76, figure 1](../../assets/fpga-tutorial/page-076-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 76, figure 2](../../assets/fpga-tutorial/page-076-image-02.jpg)

---

<a id="page-77"></a>
## Source PDF page 77

75 / 223  
13) The architecture diagram of the MPSoC hard core will be displayed below  
 In the IO Configuration window  
Configure the voltages of Bank0, Bank1, Bank2, and Bank3 to LVCMOS18

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 77, figure 1](../../assets/fpga-tutorial/page-077-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 77, figure 2](../../assets/fpga-tutorial/page-077-image-02.jpg)

---

<a id="page-78"></a>
## Source PDF page 78

76 / 223  
 In the Low Speed->Memory Interface interface, check QSPI and SD 0, SD 1;  
QSPI: Dual Parallel, x4

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 78, figure 1](../../assets/fpga-tutorial/page-078-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 78, figure 2](../../assets/fpga-tutorial/page-078-image-02.jpg)

---

<a id="page-79"></a>
## Source PDF page 79

77 / 223  
SD 0: MIO13..22, eMMC, 8Bit, Reset MIO23  
SD 1: MIO46..51, SD 2.0, 4Bit, CD MIO45  
 In the Low Speed -> I/O Peripherals interface, check I2C 1, UART 0, UART 1;

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 79, figure 1](../../assets/fpga-tutorial/page-079-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 79, figure 2](../../assets/fpga-tutorial/page-079-image-02.jpg)

---

<a id="page-80"></a>
## Source PDF page 80

78 / 223  
In the Low Speed -> Processing Unit interface, check TTC 0, TTC1, TTC 2, TTC 3;  
In the High Speed interface, check GEM 3, USB 0, USB 3.0, PCIe, Display Port;

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 80, figure 1](../../assets/fpga-tutorial/page-080-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 80, figure 2](../../assets/fpga-tutorial/page-080-image-02.jpg)

---

<a id="page-81"></a>
## Source PDF page 81

79 / 223

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 81, figure 1](../../assets/fpga-tutorial/page-081-image-01.jpg)

---

<a id="page-82"></a>
## Source PDF page 82

80 / 223  
 In the Clock Configuration window  
Configure the input clock as shown in the figure below, the rest can remain default;

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 82, figure 1](../../assets/fpga-tutorial/page-082-image-01.jpg)

---

<a id="page-83"></a>
## Source PDF page 83

81 / 223

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 83, figure 1](../../assets/fpga-tutorial/page-083-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 83, figure 2](../../assets/fpga-tutorial/page-083-image-02.jpg)

---

<a id="page-84"></a>
## Source PDF page 84

82 / 223  
 In the DDR Configuration window, configure the DDR parameters as shown in the figure below

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 84, figure 1](../../assets/fpga-tutorial/page-084-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 84, figure 2](../../assets/fpga-tutorial/page-084-image-02.jpg)

---

<a id="page-85"></a>
## Source PDF page 85

83 / 223  
 In the PCIe Configuration window, mainly configure the device port type and device ID; other settings can remain default;  
 On the PS-PL Configuration page, configure as follows.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 85, figure 1](../../assets/fpga-tutorial/page-085-image-01.jpg)

---

<a id="page-86"></a>
## Source PDF page 86

84 / 223  
14) Click OK  
15) Select Tools->Validate Design to check if there are any errors in the settings  
16) Right-click on the system and select Create HDL Wrapper

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 86, figure 1](../../assets/fpga-tutorial/page-086-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 86, figure 2](../../assets/fpga-tutorial/page-086-image-02.jpg)

---

<a id="page-87"></a>
## Source PDF page 87

85 / 223  
17) Select 'Let Vivado manage wrapper and auto-update'  
18) Click 'Run Synthesis' (here we only use PS resources, no bitstream is generated)

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 87, figure 1](../../assets/fpga-tutorial/page-087-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 87, figure 2](../../assets/fpga-tutorial/page-087-image-02.jpg)

---

<a id="page-88"></a>
## Source PDF page 88

86 / 223  
19) After completing the integration, click OK  
20) Select File->Export->Export Hardware

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 88, figure 1](../../assets/fpga-tutorial/page-088-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 88, figure 2](../../assets/fpga-tutorial/page-088-image-02.jpg)

---

<a id="page-89"></a>
## Source PDF page 89

87 / 223  
21) Click Next  
22) Here we don't have bits, use the default configuration, click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 89, figure 1](../../assets/fpga-tutorial/page-089-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 89, figure 2](../../assets/fpga-tutorial/page-089-image-02.jpg)

---

<a id="page-90"></a>
## Source PDF page 90

88 / 223  
23) Set the name and path, click Next  
24) Click Finish  
Here we can see the newly generated xsa file:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 90, figure 1](../../assets/fpga-tutorial/page-090-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 90, figure 2](../../assets/fpga-tutorial/page-090-image-02.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 90, figure 3](../../assets/fpga-tutorial/page-090-image-03.jpg)

---

<a id="page-91"></a>
## Source PDF page 91

89 / 223  
4.1.2 Software Engineering Setup  
In the previous section, we set up the hardware project in Vivado and exported the XSA file. Here, create a Vitis folder under the project directory to serve as the working directory for Vitis.  
1) Log in to Vitis  
2) Select the working directory and click Launch

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 91, figure 1](../../assets/fpga-tutorial/page-091-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 91, figure 2](../../assets/fpga-tutorial/page-091-image-02.jpg)

---

<a id="page-92"></a>
## Source PDF page 92

90 / 223  
3) Click Create Platform Project  
4) Set the project name, then click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 92, figure 1](../../assets/fpga-tutorial/page-092-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 92, figure 2](../../assets/fpga-tutorial/page-092-image-02.jpg)

---

<a id="page-93"></a>
## Source PDF page 93

91 / 223  
5) Click Browse..

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 93, figure 1](../../assets/fpga-tutorial/page-093-image-01.jpg)

---

<a id="page-94"></a>
## Source PDF page 94

92 / 223  
6) Select the previously generated xsa file and click Finish

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 94, figure 1](../../assets/fpga-tutorial/page-094-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 94, figure 2](../../assets/fpga-tutorial/page-094-image-02.jpg)

---

<a id="page-95"></a>
## Source PDF page 95

93 / 223  
7) Right-click on the generated plf and click Compile

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 95, figure 1](../../assets/fpga-tutorial/page-095-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 95, figure 2](../../assets/fpga-tutorial/page-095-image-02.jpg)

---

<a id="page-96"></a>
## Source PDF page 96

94 / 223  
At this point, our software engineering setup is complete. From here, we can carry out PS bare-metal experiments based on this foundation;  

4.2 Experiencing ARM, Bare-Metal Output of 'Hello World'  
'Hello World!' is the simplest and most classic introductory experiment in various programming languages. Here, we will print 'Hello World' through the serial port as the opening experiment for embedded systems, which also marks our starting point for the PS section.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 96, figure 1](../../assets/fpga-tutorial/page-096-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 96, figure 2](../../assets/fpga-tutorial/page-096-image-02.jpg)

---

<a id="page-97"></a>
## Source PDF page 97

95 / 223  
4.2.1 Hardware Introduction  
The RFEVM216 baseboard reserves a JTAG & UART interface, which can be used both to download and debug programs and to communicate with a PC via serial port.  
Figure 10 JTAG & UART Hardware Schematic  
4.2.2 Vitis Program Development  
Based on the previous section, we create a UART-based application program.  
1) Log in to Vitis and switch to the previous working directory

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 97, figure 1](../../assets/fpga-tutorial/page-097-image-01.jpg)

---

<a id="page-98"></a>
## Source PDF page 98

96 / 223  
2) Create a new application File->New->Application Project  
3) Click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 98, figure 1](../../assets/fpga-tutorial/page-098-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 98, figure 2](../../assets/fpga-tutorial/page-098-image-02.jpg)

---

<a id="page-99"></a>
## Source PDF page 99

97 / 223  
4) Here, the platform previously generated is selected by default, just click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 99, figure 1](../../assets/fpga-tutorial/page-099-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 99, figure 2](../../assets/fpga-tutorial/page-099-image-02.jpg)

---

<a id="page-100"></a>
## Source PDF page 100

98 / 223  
5) Enter the APP project name, keep the rest default, and click Next  
6) Click Next  
7) Select the Hello World template and click Finish

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 100, figure 1](../../assets/fpga-tutorial/page-100-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 100, figure 2](../../assets/fpga-tutorial/page-100-image-02.jpg)

---

<a id="page-101"></a>
## Source PDF page 101

99 / 223  
8) After completion, you can see the generated APP project.  
9) Right-click on the APP project, select Build Project, or click the hammer button in the menu bar to compile the project;

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 101, figure 1](../../assets/fpga-tutorial/page-101-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 101, figure 2](../../assets/fpga-tutorial/page-101-image-02.jpg)

---

<a id="page-102"></a>
## Source PDF page 102

100 / 223  
The Console window will display compilation information, and an elf file will be generated after the compilation is finished.  
10) Right-click the APP project, and select Run As->Run Configuration

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 102, figure 1](../../assets/fpga-tutorial/page-102-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 102, figure 2](../../assets/fpga-tutorial/page-102-image-02.jpg)

---

<a id="page-103"></a>
## Source PDF page 103

101 / 223 11) Double-click Single Application Debug to generate Debugger_hello; carry out related settings on the Target Setup page. (Here we only have the PS part, so there is no need to enable Program FPGA)

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 103, figure 1](../../assets/fpga-tutorial/page-103-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 103, figure 2](../../assets/fpga-tutorial/page-103-image-02.jpg)

---

<a id="page-104"></a>
## Source PDF page 104

102 / 223  
12) On the PC side, open the serial debug terminal, select the corresponding serial port number and baud rate 115200;  
13) Click Run in step 11, the download progress will be displayed in the lower right corner  
14) After the download is complete, check the serial output

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 104, figure 1](../../assets/fpga-tutorial/page-104-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 104, figure 2](../../assets/fpga-tutorial/page-104-image-02.jpg)

---

<a id="page-105"></a>
## Source PDF page 105

103 / 223  
4.2.3 Programming Procedure  
4.2.3.1 Generating the boot.bin File  
Ordinary FPGAs can generally boot from flash or be passively loaded, while the Zynq boot is controlled by the ARM processor, including the loading of FPGA programs.  
The Zynq RFSOC boot process is mainly divided into three stages (detailed in UG1085):  
- Pre-configuration stage: Resets and wakes up the processor through the code in ROM.
- Configuration stage: Loads the FSBL code into on-chip RAM (OCM) via the APU or RPU.
- Post-configuration stage: Starts U-Boot, Linux, etc., after the FSBL.
The figure below shows the detailed steps of the boot process:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 105, figure 1](../../assets/fpga-tutorial/page-105-image-01.jpg)

---

<a id="page-106"></a>
## Source PDF page 106

104 / 223  
It should be noted that for Zynq, it is not possible to program the PL alone. This is because the PL part in the Zynq series is usually configured through the PS (it can be considered that PL acts as a peripheral of the PS), and many non-volatile memories are connected to the PS side. The configuration and startup of the PL generally rely on the boot process of the PS. The PL program needs to be loaded and configured through the PS boot process.  

Files required for RFSoC startup:  
- Boot image/boot.bin file, which mainly includes:
 First Stage Boot Loader (fsbl.elf)  
 Platform Management Firmware (pmufw.elf)  
 PL bitstream (system.bit), this part is optional  
 ARM Trusted Firmware (bl31.elf)  
 Second Stage Boot Loader, such as uboot.elf for U-Boot or application software  
- Linux binary image file image.ub, which mainly includes:
 Flattened Device Tree binary object (system.dtb)  
 Linux kernel (Image)  
- Root filesystem, which can be a Ramdisk (initrd) or on SD card or Flash.
Xilinx's tool Vitis can realize the bare-metal startup steps on the left, and Petalinux can realize the Linux system startup steps on the right.

---

<a id="page-107"></a>
## Source PDF page 107

105 / 223  
Here we generate the boot file boot.bin required for bare-metal under the Vitis tool:  
1. Select our newly created application project, right-click on the 'xxx_system' folder

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 107, figure 1](../../assets/fpga-tutorial/page-107-image-01.jpg)

---

<a id="page-108"></a>
## Source PDF page 108

106 / 223  
2. Click [Build Project]; this step will automatically generate the boot.bin file

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 108, figure 1](../../assets/fpga-tutorial/page-108-image-01.jpg)

---

<a id="page-109"></a>
## Source PDF page 109

107 / 223  
We can also manually generate the boot.bin file:  
1. Select our newly created application project, and right-click on the "xxx_system" folder

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 109, figure 1](../../assets/fpga-tutorial/page-109-image-01.jpg)

---

<a id="page-110"></a>
## Source PDF page 110

108 / 223  
2. Click [Create Boot Image]  
3. In the pop-up window, you can see the path of the generated BIF file and the path of the generated BOOT.BIN file. The BOOT.BIN file is the boot file we need, which can be used to boot from the SD card or be written to QSPI flash.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 110, figure 1](../../assets/fpga-tutorial/page-110-image-01.jpg)

---

<a id="page-111"></a>
## Source PDF page 111

109 / 223  
In the BOOT Image Partitions list, there are files to be combined. The first file must be the bootloader file, which is the automatically generated fsbl.elf file after compiling when generating the hardware platform. The second file is the FPGA configuration bitstream file. In this experiment, since there is no FPGA bitstream, it does not need to be added. The third file is the application program, which in this experiment is hello.elf. Due to the absence of the bitstream, only the bootloader and the application program are added in this experiment. Click [Create Image] to generate.  

4.2.3.2 SD Card Boot Test  
1. Format the SD card and select FAT32 as the file system;  
2. Copy the BOOT.BIN file generated in the previous step to the SD card;  
3. Insert the SD card into the SD card slot of the development board;  
4. Set the boot mode to SD card boot (set all SWC1 DIP switches to OFF);  
5. Open the serial software, power on and start, and you will see the printed information.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 111, figure 1](../../assets/fpga-tutorial/page-111-image-01.jpg)

---

<a id="page-112"></a>
## Source PDF page 112

110 / 223  
4.2.3.3 QSPI Boot Test  
1. In the Vitis menu, go to Xilinx -> Program Flash.  
2. In the pop-up Program Flash Memory interface, select the BOOT.BIN file we want to write under Image File, select fsbl.elf under FSBL File, choose qspi-x8-dual_parallel for Flash Type, click [Program], and wait for the programming to complete.  
3. After the programming is complete, set the boot mode to QSPI boot (switch all positions of SWC1 to ON), power cycle the board, and you can see the same result as SD card boot in the serial software.  
4.3 PS-side RTC Interrupt Experiment  
The RTC (Real Time Clock) unit provides precise time to the system and application software.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 112, figure 1](../../assets/fpga-tutorial/page-112-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 112, figure 2](../../assets/fpga-tutorial/page-112-image-02.jpg)

---

<a id="page-113"></a>
## Source PDF page 113

111 / 223  
Calibration. To meet the need for high precision, the RTC also includes a calibration circuit to compensate for temperature and voltage fluctuations. The RTC is powered by VCC-PSAUX or VCC-PSBATT. When the auxiliary power is available, the RTC uses it to keep the counter running. When the auxiliary power VCC PSAUX is unavailable, the RTC automatically switches to the battery power VCC PSBATT.  
The RTC has the following features:  
- Can operate using either auxiliary power or battery power. When the system loses power, the RTC automatically switches to battery power to maintain continuous operation.
- Alarm settings and periodic interrupts (timer interrupts).
- Complex calibration circuit for high-precision timing.
- 32-bit second counter, capable of counting approximately 136 years.
- Three counters: 32-bit second counter, 16-bit tick counter for measuring seconds based on a 32 kHz crystal oscillator, and a 4-bit fractional counter for calibration.
Figure 11 RTC controller structure diagram

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 113, figure 1](../../assets/fpga-tutorial/page-113-image-01.jpg)

---

<a id="page-114"></a>
## Source PDF page 114

112 / 223  
Figure 12 RTC Function Diagram  
4.3.1 Software Design  
1) Log in to Vitis, switch to the previous working directory, then double-click platform.spr, select Board Support Package, and you can see the documentation and import example for psu_rtc.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 114, figure 1](../../assets/fpga-tutorial/page-114-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 114, figure 2](../../assets/fpga-tutorial/page-114-image-02.jpg)

---

<a id="page-115"></a>
## Source PDF page 115

113 / 223  
2) Click Import Example, and the import example interface as shown in the figure below will pop up;  
3) Here we select the third official example, the RTC periodic alarm interrupt example (xrtcpsu_periodic_alarm_interrupt_example), and click OK  
4) Here we have imported the example project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 115, figure 1](../../assets/fpga-tutorial/page-115-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 115, figure 2](../../assets/fpga-tutorial/page-115-image-02.jpg)

---

<a id="page-116"></a>
## Source PDF page 116

114 / 223  
5) Select the application project, right-click and then choose Build Project to compile the project. The compilation progress can be viewed in the console panel at the bottom of the tool, as shown in the figure below:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 116, figure 1](../../assets/fpga-tutorial/page-116-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 116, figure 2](../../assets/fpga-tutorial/page-116-image-02.jpg)

---

<a id="page-117"></a>
## Source PDF page 117

115 / 223  
4.3.2 Download Verification  
First, connect the Type-C end of the USB to Type-C cable to the JTAG interface on the RFEVM2116 development board, and connect the other end of the USB to Type-C cable to the computer. Connect the development board power and turn on the development board.  
Download the program, right-click the application project, and select Run As->Run Configuration...

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 117, figure 1](../../assets/fpga-tutorial/page-117-image-01.jpg)

---

<a id="page-118"></a>
## Source PDF page 118

116 / 223  
Double-click the Single Application Debug item  
Select the Target Setup tab, use the default configuration, and click Run

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 118, figure 1](../../assets/fpga-tutorial/page-118-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 118, figure 2](../../assets/fpga-tutorial/page-118-image-02.jpg)

---

<a id="page-119"></a>
## Source PDF page 119

117 / 223  
After the download is complete, you can see the information that the serial port needs to print in the serial debugging terminal:  
4.4 Use of IIC on the PS side  
4.4.1 Hardware Design  
The PS side IIC is connected to an external EEPROM. This section introduces how to use IIC to read and write the external device.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 119, figure 1](../../assets/fpga-tutorial/page-119-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 119, figure 2](../../assets/fpga-tutorial/page-119-image-02.jpg)

---

<a id="page-120"></a>
## Source PDF page 120

118 / 223  
4.4.2 Software Design  
1) Log in to Vitis, switch to the previous working directory, then double-click platform.spr, select Board Support Package, and you can see the documentation link and import example for psu_i2c_1.  
2) Click Import Example, then select the xiicps_eeprom_polled_example example, and click OK

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 120, figure 1](../../assets/fpga-tutorial/page-120-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 120, figure 2](../../assets/fpga-tutorial/page-120-image-02.jpg)

---

<a id="page-121"></a>
## Source PDF page 121

119 / 223  
3) You can see the imported example application project.  
4) The device address of the EEPROM is defined at the beginning of the program. This address is the device address the system uses to access external IIC peripherals. Here, the EEPROM address is changed to 0x50, then saved.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 121, figure 1](../../assets/fpga-tutorial/page-121-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 121, figure 2](../../assets/fpga-tutorial/page-121-image-02.jpg)

---

<a id="page-122"></a>
## Source PDF page 122

120 / 223  
The device address of the EEPROM can be found in the AT24CM01 chip manual.  
Among them, A1 and A2 are directly connected to the ground in the hardware, which is 0;  
The program flow is as follows:  
Clear ReadBuffer to 0, assign incrementing data to WriteBuffer -> write 32 bytes to EEPROM -> read 16 bytes from EEPROM into ReadBuffer -> check if correct -> return.  
5) Select the application project, right-click and choose Build Project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 122, figure 1](../../assets/fpga-tutorial/page-122-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 122, figure 2](../../assets/fpga-tutorial/page-122-image-02.jpg)

---

<a id="page-123"></a>
## Source PDF page 123

121 / 223  
Compilation information can be seen in the Console window  
4.4.3 Download Verification  
First, we connect the download cable (USB to Type-C cable) to the JTAG interface of the development board, then

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 123, figure 1](../../assets/fpga-tutorial/page-123-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 123, figure 2](../../assets/fpga-tutorial/page-123-image-02.jpg)

---

<a id="page-124"></a>
## Source PDF page 124

122 / 223  
One end is connected to the computer. Finally, turn on the power switch of the development board.  
Right-click the application project, select Run As -> Launch Hardware (Single Application Debug)  
Open the serial terminal, and after the download is complete, you can view the serial output:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 124, figure 1](../../assets/fpga-tutorial/page-124-image-01.jpg)

---

<a id="page-125"></a>
## Source PDF page 125

123 / 223  
4.5 LWIP for PS-side Ethernet  
LWIP is a small open-source TCP/IP protocol stack developed by Adam Dunkels and others at the Swedish Institute of Computer Science (SICS). It is one implementation of TCP/IP. LWIP is a lightweight IP protocol that can run with or without operating system support. The focus of LWIP's implementation is to reduce RAM usage while maintaining the main functions of the TCP protocol. It only requires about a dozen KB of RAM and around 40K of ROM to run, making the LWIP protocol stack suitable for use in low-end embedded systems.  
Here, we use the Lwip Echo Server template provided with Vitis software to understand the use of LWIP.  
4.5.1 Hardware Design  
The RFEVM216 development board has a PS-side RJ45 Ethernet interface for connecting to an Ethernet cable. Its schematic diagram is shown as follows:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 125, figure 1](../../assets/fpga-tutorial/page-125-image-01.jpg)

---

<a id="page-126"></a>
## Source PDF page 126

124 / 223  
Figure 13 RJ45 Interface Schematic  
Ethernet data transmission cannot do without the support of the Ethernet PHY (Physical Layer) chip. The PHY chip used on the RFEVM216 development board is the DP83867ISRGZ chip from Texas Instruments, and part of the schematic is shown in the figure:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 126, figure 1](../../assets/fpga-tutorial/page-126-image-01.jpg)

---

<a id="page-127"></a>
## Source PDF page 127

125 / 223  
Figure 14 DP83867ISRGZ Schematic  
4.5.2 Software Design  
Add the lwip library in the BSP library files  
Double-click platform.spr, select Board Support Package, and click Modify BSP Settings...

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 127, figure 1](../../assets/fpga-tutorial/page-127-image-01.jpg)

---

<a id="page-128"></a>
## Source PDF page 128

126 / 223  
Enable the lwip library, click OK  
Compile platform

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 128, figure 1](../../assets/fpga-tutorial/page-128-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 128, figure 2](../../assets/fpga-tutorial/page-128-image-02.jpg)

---

<a id="page-129"></a>
## Source PDF page 129

127 / 223  
Create a new application File->New->Application Project  
Click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 129, figure 1](../../assets/fpga-tutorial/page-129-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 129, figure 2](../../assets/fpga-tutorial/page-129-image-02.jpg)

---

<a id="page-130"></a>
## Source PDF page 130

128 / 223  
Click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 130, figure 1](../../assets/fpga-tutorial/page-130-image-01.jpg)

---

<a id="page-131"></a>
## Source PDF page 131

129 / 223  
Set the APP name, click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 131, figure 1](../../assets/fpga-tutorial/page-131-image-01.jpg)

---

<a id="page-132"></a>
## Source PDF page 132

130 / 223  
Click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 132, figure 1](../../assets/fpga-tutorial/page-132-image-01.jpg)

---

<a id="page-133"></a>
## Source PDF page 133

131 / 223  
Select the Lwip Echo Server template and click Finish.  
We modify the IP and subnet of the board so that the board and the PC are on the same subnet.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 133, figure 1](../../assets/fpga-tutorial/page-133-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 133, figure 2](../../assets/fpga-tutorial/page-133-image-02.jpg)

---

<a id="page-134"></a>
## Source PDF page 134

After making modifications, save the file, right-click the lwip_echo_server project, and click Build Project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 134, figure 1](../../assets/fpga-tutorial/page-134-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 134, figure 2](../../assets/fpga-tutorial/page-134-image-02.jpg)

---

<a id="page-135"></a>
## Source PDF page 135

133 / 223  
4.5.3 Download Verification  
1) Here we connect the PC and the RFEVM development board using a gigabit Ethernet cable, then power on the board.  
2) The IP addresses of the PC and the RFEVM must be in the same subnet to communicate with each other.  
Default configuration of RFEVM216 Ethernet:  
MAC address: 00:0a:35:00:01:02  
IP address: 192.168.5.10  
Subnet mask: 255.255.255.0  
Gateway: 192.168.5.1  
3) Right-click the lwip_echo_server project and select Run As->Run Configuration

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 135, figure 1](../../assets/fpga-tutorial/page-135-image-01.jpg)

---

<a id="page-136"></a>
## Source PDF page 136

134 / 223  
4) We open the serial port debugging terminal. After downloading the program, the terminal will display the program’s output information.  
5) Open the cmd window and ping the board’s IP

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 136, figure 1](../../assets/fpga-tutorial/page-136-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 136, figure 2](../../assets/fpga-tutorial/page-136-image-02.jpg)

---

<a id="page-137"></a>
## Source PDF page 137

135 / 223  
4.5.4 Reference Documents  
https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842366/Standalone+LWIP+library  
4.6 Use of DisplayPort on the PS Side  
4.6.1 Hardware Design  
The RFEVM216 baseboard has one DP display interface, which can be connected to a DP monitor for output. The design block diagram is shown below:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 137, figure 1](../../assets/fpga-tutorial/page-137-image-01.jpg)

---

<a id="page-138"></a>
## Source PDF page 138

136 / 223  
4.6.2 Software Design  
1) Double-click platform.spr and select Board Support Package  
2) Click Import Example, then select the xdpdma_video_example example, and click OK

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 138, figure 1](../../assets/fpga-tutorial/page-138-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 138, figure 2](../../assets/fpga-tutorial/page-138-image-02.jpg)

---

<a id="page-139"></a>
## Source PDF page 139

137 / 223  
3) Select the application project, right-click and click Build Project  
4.6.3 Download and Verification  
Here we need to connect one end of the DP data cable to a monitor with a DP interface, and the other end to the DP interface of the board. Then power on the development board.  
Right-click the application project, select Run As->Launch Hardware (Single Application Debug)

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 139, figure 1](../../assets/fpga-tutorial/page-139-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 139, figure 2](../../assets/fpga-tutorial/page-139-image-02.jpg)

---

<a id="page-140"></a>
## Source PDF page 140

138 / 223  
Open the serial terminal, after the download is complete, you can check the serial output:  
At the same time, color bars are displayed on the monitor

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 140, figure 1](../../assets/fpga-tutorial/page-140-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 140, figure 2](../../assets/fpga-tutorial/page-140-image-02.jpg)

---

<a id="page-141"></a>
## Source PDF page 141

139 / 223  
4.7 SD Card Read/Write TXT Text Experiment  
The SD card interface on the RFEVM216 board is designed for a small card, which can connect a Micro SD card (also called a TF card). The MPSoC internally integrates two SD card controllers, and the Xilinx Vitis standalone environment has already ported the FATFS (called xilffs in Vitis) file system. FATFS is a completely open-source and free FAT file system module, specifically designed for small embedded systems. It is entirely written in standard C language, so it has good hardware platform independence and can be easily ported to various embedded processors. Therefore, after adding the xilffs library in Vitis, you can use the API functions provided by FATFS in your program to operate the SD card.  

Users do not need to worry about the internal structure of FATFS or the complex FAT protocol; they only need to call a series of application interface functions provided by the FATFS module, such as f_open, f_read, f_write, and f_close. This makes reading/writing files as simple as on a PC.  

4.7.1 Hardware Design  
There is an SD card interface on our RFEVM216 development board, which can connect a Micro SD card (TF card). The schematic is shown in the figure below:

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 141, figure 1](../../assets/fpga-tutorial/page-141-image-01.jpg)

---

<a id="page-142"></a>
## Source PDF page 142

140 / 223  
Figure 15 Micro SD Card Schematic  
From the above figure, it can be seen that the SD card has four data lines (SDIO_DAT0~SDIO_DAT3), which are connected to the pins of the MPSoC. In the figure, the SDIO_DETECT signal is the TF card detection signal, used to indicate whether the development board has a TF card connected. When the development board does not have a TF card connected, this signal is high; when the development board has a TF card connected, this signal is low, indicating that the development board already has a TF card connected.  

4.7.2 Software Design  
Add the xilffs library to the BSP library files.  
Double-click platform.spr, select Board Support Package, and click Modify BSP Settings...

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 142, figure 1](../../assets/fpga-tutorial/page-142-image-01.jpg)

---

<a id="page-143"></a>
## Source PDF page 143

141 / 223  
Enable the "xilffs" library and click "OK"  
After adding the FATFS library, operations on the TF card will be much simpler. We only need to call the FATFS library functions in the program.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 143, figure 1](../../assets/fpga-tutorial/page-143-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 143, figure 2](../../assets/fpga-tutorial/page-143-image-02.jpg)

---

<a id="page-144"></a>
## Source PDF page 144

142 / 223  
After adding is complete, recompile the platform  
Create a new application File->New->Application Project  
Click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 144, figure 1](../../assets/fpga-tutorial/page-144-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 144, figure 2](../../assets/fpga-tutorial/page-144-image-02.jpg)

---

<a id="page-145"></a>
## Source PDF page 145

143 / 223  
Click Next

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 145, figure 1](../../assets/fpga-tutorial/page-145-image-01.jpg)

---

<a id="page-146"></a>
## Source PDF page 146

144 / 223  
Set the application name, then click 'Next'

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 146, figure 1](../../assets/fpga-tutorial/page-146-image-01.jpg)

---

<a id="page-147"></a>
## Source PDF page 147

145 / 223  
Click 'Next'

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 147, figure 1](../../assets/fpga-tutorial/page-147-image-01.jpg)

---

<a id="page-148"></a>
## Source PDF page 148

146 / 223  
Here we choose Empty Application (C) as the template, and click 'Finish'

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 148, figure 1](../../assets/fpga-tutorial/page-148-image-01.jpg)

---

<a id="page-149"></a>
## Source PDF page 149

147 / 223  
Here we can see the newly created application project.  
Next, create a new source file "main.c" for the application project.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 149, figure 1](../../assets/fpga-tutorial/page-149-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 149, figure 2](../../assets/fpga-tutorial/page-149-image-02.jpg)

---

<a id="page-150"></a>
## Source PDF page 150

148 / 223

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 150, figure 1](../../assets/fpga-tutorial/page-150-image-01.jpg)

---

<a id="page-151"></a>
## Source PDF page 151

149 / 223  
In the newly created main.c file, we enter the following code:  
#include "xparameters.h"  
#include "xil_printf.h"  
#include "ff.h"  
#include "xstatus.h"  
#define FILE_NAME "WE5G.txt" // Define the file name  
const char src_str[30] = "www.v3t.com.cn"; // Define the text content  
// main function  
int main()  
{

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 151, figure 1](../../assets/fpga-tutorial/page-151-image-01.jpg)

---

<a id="page-152"></a>
## Source PDF page 152

150 / 223  
int status, len;  
char dest_str[30] = "";  
static FATFS fatfs;  
FIL fil; // file object  
UINT bw; // number of bytes written returned by f_write function  
UINT br; // number of bytes read returned by f_read function  
// Register a workspace (mount partition filesystem)  
// Before using any other file functions, you must use the f_mount function to register a workspace for each used volume  
status = f_mount(&fatfs, "1:/", 1); // mount SD card  
if (status != FR_OK) {  
xil_printf("\r\nUnable to mount FATfs\r\n");  
return -1;  
}  
xil_printf("Success to open SD card!\r\n");  
len = strlen(src_str); // calculate string length  
// Open a file, if it does not exist, create a file  
status = f_open(&fil, "1:/WE5G.txt", FA_OPEN_ALWAYS | FA_WRITE | FA_READ);  
if (status != FR_OK) {  
xil_printf("Unable to open file!\r\n");  
return -1;  
}  
xil_printf("Success to open file.\r\n");  
// Move the read/write pointer of the opened file object 0: point to the beginning of the file  
f_lseek(&fil, 0);  
// Write data to the file  
f_write(&fil, (void*) src_str, len, &bw);  
xil_printf("write file return:%d.\r\n", bw);  
// SD card data reading  
// sd_read_data(FILE_NAME, (u32)dest_str, len);  
f_lseek(&fil, 0);  

f_read(&fil, (void*)dest_str, len, &br);  
f_close(&fil);  
xil_printf("read file return:%d.\r\n", bw);  
// Compare whether the written string and the read string are equal  
if (strcmp(src_str, dest_str) == 0)  
    xil_printf("src_str is equal to dest_str, SD card test success!\r\n");  
else  
    xil_printf("src_str is not equal to dest_str, SD card test failed!\r\n");

---

<a id="page-153"></a>
## Source PDF page 153

151 / 223  
return 0;  
}  
In the main function, the implemented functionality is to read and write TXT files on the TF card and compare whether the written data and the read data are consistent. The program first calls the f_mount() function to mount the TF card. Next, based on the length of the string to be written, it uses the f_write() function and the f_read() function to write to and read from the TXT file on the TF card, then compares the written and read values and prints the comparison result.  

4.7.3 Download Verification  
First, we connect the download cable (USB to Type-C cable) to the JTAG interface of the development board, with the other end connected to the computer. Next, insert the TF card. Finally, turn on the power switch of the development board.  
Right-click the application project, select Run As -> Launch Hardware (Single Application Debug).  
Open the serial terminal. After the download is complete, you can check the serial output:  
From the above figure, it can be seen that the displayed written characters and the read characters are consistent, indicating that the TF card read/write test was successful.  
Next, remove the TF card from the development board slot, and use a card reader to connect it to the USB port of the computer. At this time, the file contents on the TF card can be seen as shown in the figure below.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 153, figure 1](../../assets/fpga-tutorial/page-153-image-01.jpg)

---

<a id="page-154"></a>
## Source PDF page 154

152 / 223  
Open the "WE5G.txt" text file, and you can see the content of the text, as shown in the figure below:  
4.7.4 Reference Documents  
http://elm-chan.org/fsw/ff/00index_e.html  
4.8 USB Slave Function Test Based on PS  
The USB interface of Zynq can act as both a USB HOST and a USB DEVICE (SLAVE). In most cases, the USB function is used under Linux. Here, we will test the USB function in a bare-metal environment.  
We use the officially provided demo to test the USB device by simulating the function of a USB flash drive.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 154, figure 1](../../assets/fpga-tutorial/page-154-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 154, figure 2](../../assets/fpga-tutorial/page-154-image-02.jpg)

---

<a id="page-155"></a>
## Source PDF page 155

153 / 223  
4.8.1 Hardware Design  
Figure 16 USB Interface Schematic  
4.8.2 Software Design  
4) Log in to Vitis, switch to the previous working directory, then double-click platform.spr, select Board Support Package, where you can see the documentation link for psu_usb_xhci_0 and import examples.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 155, figure 1](../../assets/fpga-tutorial/page-155-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 155, figure 2](../../assets/fpga-tutorial/page-155-image-02.jpg)

---

<a id="page-156"></a>
## Source PDF page 156

154 / 223  
5) Click Import Example, then select the xusb_poll_example example, and click OK  
6) You can see the imported example application project  
7) Select the application project, right-click and click Build Project

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 156, figure 1](../../assets/fpga-tutorial/page-156-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 156, figure 2](../../assets/fpga-tutorial/page-156-image-02.jpg)

---

<a id="page-157"></a>
## Source PDF page 157

155 / 223  
Compilation information can be seen in the Console window.  
4.8.3 Download Verification  
Here we need to use a USB A-to-A data cable, with one end connected to the USB interface of the RFEVM216, and the other end connected to the PC. Then power on the development board.  
Right-click the application project, and select Run As->Launch Hardware (Single Application Debug)

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 157, figure 1](../../assets/fpga-tutorial/page-157-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 157, figure 2](../../assets/fpga-tutorial/page-157-image-02.jpg)

---

<a id="page-158"></a>
## Source PDF page 158

156 / 223  
Open the serial terminal. After the download is complete, you can check the serial output:  
On the PC side, the following window will pop up. Click 'Format Disk' to proceed.  
In My Computer, you can see a U disk virtualized by the DDR RAM. You can copy and paste files just like a normal U disk. Note that this U disk will lose data when powered off, so do not store important files on it.  
The capacity can be configured in the program. Please do not exceed the DDR capacity on the board.  
We can use the CrystalDiskMark tool recommended by Xilinx Wiki to test the U disk's performance.

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 158, figure 1](../../assets/fpga-tutorial/page-158-image-01.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 158, figure 2](../../assets/fpga-tutorial/page-158-image-02.jpg)

![RFEVM216 Development Platform FPGA Tutorial, page 158, figure 3](../../assets/fpga-tutorial/page-158-image-03.jpg)

---

<a id="page-159"></a>
## Source PDF page 159

157 / 223  
4.8.4 Reference Documents  
https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842468/ZynqMp+USB+Standalone+Driver

### Figures

![RFEVM216 Development Platform FPGA Tutorial, page 159, figure 1](../../assets/fpga-tutorial/page-159-image-01.jpg)
