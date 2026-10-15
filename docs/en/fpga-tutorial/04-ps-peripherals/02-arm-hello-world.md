# 4.2 Experiencing ARM, Bare-Metal Output of 'Hello World'

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/02-arm-hello-world.md)

[Back to chapter overview](index.md)

'Hello World!' is the simplest and most classic introductory experiment in various programming languages. Here, we will print 'Hello World' through the serial port as the opening experiment for embedded systems, which also marks our starting point for the PS section.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-096-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-096-image-02.jpg)

## 4.2.1 Hardware Introduction

The RFEVM216 baseboard reserves a JTAG & UART interface, which can be used both to download and debug programs and to communicate with a PC via serial port.
Figure 10 JTAG & UART Hardware Schematic

## 4.2.2 Vitis Program Development

Based on the previous section, we create a UART-based application program.

1. Log in to Vitis and switch to the previous working directory

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-097-image-01.jpg)

2. Create a new application File->New->Application Project
3. Click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-098-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-098-image-02.jpg)

4. Here, the platform previously generated is selected by default, just click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-099-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-099-image-02.jpg)

5. Enter the APP project name, keep the rest default, and click Next
6. Click Next
7. Select the Hello World template and click Finish

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-100-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-100-image-02.jpg)

8. After completion, you can see the generated APP project.
9. Right-click on the APP project, select Build Project, or click the hammer button in the menu bar to compile the project;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-101-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-101-image-02.jpg)

The Console window will display compilation information, and an elf file will be generated after the compilation is finished.

10. Right-click the APP project, and select Run As->Run Configuration

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-102-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-102-image-02.jpg)

11. Double-click Single Application Debug to generate Debugger_hello; carry out related settings on the Target Setup page. (Here we only have the PS part, so there is no need to enable Program FPGA)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-103-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-103-image-02.jpg)

12. On the PC side, open the serial debug terminal, select the corresponding serial port number and baud rate 115200;
13. Click Run in step 11, the download progress will be displayed in the lower right corner
14. After the download is complete, check the serial output

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-104-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-104-image-02.jpg)

## 4.2.3 Programming Procedure

### 4.2.3.1 Generating the boot.bin File

Ordinary FPGAs can generally boot from flash or be passively loaded, while the Zynq boot is controlled by the ARM processor, including the loading of FPGA programs.
The Zynq RFSOC boot process is mainly divided into three stages (detailed in UG1085):

- Pre-configuration stage: Resets and wakes up the processor through the code in ROM.
- Configuration stage: Loads the FSBL code into on-chip RAM (OCM) via the APU or RPU.
- Post-configuration stage: Starts U-Boot, Linux, etc., after the FSBL.

The figure below shows the detailed steps of the boot process:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-105-image-01.jpg)

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
Here we generate the boot file boot.bin required for bare-metal under the Vitis tool:

1. Select our newly created application project, right-click on the 'xxx_system' folder

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-107-image-01.jpg)

2. Click [Build Project]; this step will automatically generate the boot.bin file

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-108-image-01.jpg)

We can also manually generate the boot.bin file:

1. Select our newly created application project, and right-click on the "xxx_system" folder

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-109-image-01.jpg)

2. Click [Create Boot Image]
3. In the pop-up window, you can see the path of the generated BIF file and the path of the generated BOOT.BIN file. The BOOT.BIN file is the boot file we need, which can be used to boot from the SD card or be written to QSPI flash.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-110-image-01.jpg)

In the BOOT Image Partitions list, there are files to be combined. The first file must be the bootloader file, which is the automatically generated fsbl.elf file after compiling when generating the hardware platform. The second file is the FPGA configuration bitstream file. In this experiment, since there is no FPGA bitstream, it does not need to be added. The third file is the application program, which in this experiment is hello.elf. Due to the absence of the bitstream, only the bootloader and the application program are added in this experiment. Click [Create Image] to generate.

### 4.2.3.2 SD Card Boot Test

1. Format the SD card and select FAT32 as the file system;
2. Copy the BOOT.BIN file generated in the previous step to the SD card;
3. Insert the SD card into the SD card slot of the development board;
4. Set the boot mode to SD card boot (set all SWC1 DIP switches to OFF);
5. Open the serial software, power on and start, and you will see the printed information.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-111-image-01.jpg)

### 4.2.3.3 QSPI Boot Test

1. In the Vitis menu, go to Xilinx -> Program Flash.
2. In the pop-up Program Flash Memory interface, select the BOOT.BIN file we want to write under Image File, select fsbl.elf under FSBL File, choose qspi-x8-dual_parallel for Flash Type, click [Program], and wait for the programming to complete.
3. After the programming is complete, set the boot mode to QSPI boot (switch all positions of SWC1 to ON), power cycle the board, and you can see the same result as SD card boot in the serial software.
