# 5. PS-PL Interconnect

[Switch to 中文](../../zh/fpga-tutorial/05-ps-pl-interconnect.md)

This chapter mainly introduces the interconnection between PS and PL. Before starting, a brief introduction to the data paths between PS and PL is provided. For details, please refer to the "ug1085 Zynq UltraScale+ Device Technical Reference Manual."
The data paths between PS and PL are mainly through the general AXI Memory interface. As a master device, PS has interfaces with 128-bit width HPM0/HPM1 and 64-bit width LPD_PL; as a master device, PL has interfaces ACP/ACE/HPC0/HPC1/HP0/HP1/HP2/HP3. All AXI Memory interfaces

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-160-image-01.jpg)

The bit width can support up to 128-bit.
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
Excerpt from "ug1085"

## 5.1 Using EMIO on the PS side

Previously, the experiment of the LED breathing light on the PL side was introduced. Here, we use the PS side to control the on/off of the LED on the PL side.
The PL side’s extended IO can also be controlled in this way.
Zynq GPIO is divided into MIO (multiplexed I/O) and EMIO (extended multiplexed I/O).
MIO is the multifunction IO interface on the PS side. The IO is connected to the PS side, and each IO can be configured as GPIO, SPI, UART, TIMER, Ethernet, USB, and other functions according to needs. Since MIO is not visible to the PL side, the PL side cannot use MIO pins.
EMIO is the extended IO of MIO, connected to the PL side. Since EMIO is visible to both the PS and PL sides, both can use EMIO pins. Generally, when the PS side MIO resources are insufficient, the PS side can expand interfaces through EMIO. The usage of EMIO is similar to MIO, with the difference being that EMIO requires using the Vivado constraint file to assign pins.
MPSoC provides 96 GPIOs to the PL, connected to the PL via EMIO pins. Here we use
Use EMIO to connect to the LED on the PL side and control its status in Vitis.

### 5.1.1 Hardware Project Setup

1. Set up the hardware project. Follow the steps for setting up the IPI project in the previous chapter to add the MPSOC IP core.
2. Double-click the IP to enable the emio interface, and select 4 for the number of IOs (corresponding to the 4 LED lights on the baseboard);
3. Here we bring out the emio output emio_gpio_o and Make External.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-162-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-162-image-02.jpg)

4. Check if there are any errors in the design

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-163-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-163-image-02.jpg)

5. Creating HDL Wrapper...

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-164-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-164-image-02.jpg)

6. Create constraint file
7. Compile to generate bit file

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-165-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-165-image-02.jpg)

8. After the compilation is complete, export the hardware project for subsequent Vitis software development;

Here we choose to include the bitstream and click [Next]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-166-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-166-image-02.jpg)

Set the name and path of xsa

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-167-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-167-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-167-image-03.jpg)

After clicking [Finish], you can see the newly generated xsa file under the project path.

### 5.1.2 Software Project Setup

After setting up the hardware project in Vivado and exporting the xsa file, create a vitis folder under the project directory as the working directory for Vitis.

1. Log in to Vitis and select the vitis folder under the project path as the working directory

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-168-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-168-image-02.jpg)

2. Select 【Create Platform Project】

Set the platform name, and click 【Next】

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-169-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-169-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-170-image-01.jpg)

Click Browse here and select the generated xsa file

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-171-image-01.jpg)

Click [Finish] to generate the hardware platform

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-172-image-01.jpg)

3. Compile platform
4. After compilation is complete, create a new application project

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-173-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-173-image-02.jpg)

Click [Next]
Click [Next]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-174-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-174-image-02.jpg)

Set the application project name and click 【Next】

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-175-image-01.jpg)

Click [Next]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-176-image-01.jpg)

Select the "Hello World" template and click [Finish]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-177-image-01.jpg)

5. Here, we modify the hello world source file and add GPIO control code

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-178-image-01.jpg)

Note: The MPSoC has 78 MIOs, the numbering of EMIO starts from 78;

### 5.1.3 Download and Verification

Here we download the bit file and elf file in Vitis. Please refer to the previously introduced steps for downloading.
You can see that the four LED lights on the board keep flashing.

## 5.2 Usage of AXI GPIO on the PL Side

AXI GPIO is a specific type of GPIO (General Purpose Input/Output) controller that communicates using the AXI (Advanced eXtensible Interface) bus protocol.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-179-image-01.jpg)

AXI GPIO is used to control and read the status of GPIO pins. It is widely used in embedded systems for communication with processors or other peripherals to control and read the status of GPIO pins. It can be used to connect various peripherals, such as LEDs, buttons, sensors, etc., to interact with the external environment. Here we use AXI GPIO to control the on-off changes of the LEDs on the board.

### 5.2.1 Hardware Project Setup

1. According to the project setup steps in the previous chapter on IPI, set up the hardware project for this experiment.
2. In the IPI interface, right-click to add the AXI GPIO IP core.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-180-image-01.jpg)

3. Here we only enable GPIO 1. We only control the LED output, so we enable all outputs with a bit width of 4 bits, then click [OK]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-181-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-181-image-02.jpg)

4. In the MPSoC, we enable the LPD interface, and then click Auto Connect [Run Connection Automation]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-182-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-182-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-183-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-183-image-02.jpg)

5. Check if the design has any errors

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-184-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-184-image-02.jpg)

6. Create an HDL wrapper, then generate the bit file.
7. Add an XDC constraint file, constrain the LED pins, and generate the bit file.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-185-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-185-image-02.jpg)

8. Export the hardware engineering xsa file (including the bitstream).

### 5.2.2 Software Project Setup

After setting up the hardware project in Vivado and exporting the xsa file, create a
vitis folder under the project directory as the working directory for Vitis.

1. Log in to Vitis and select the vitis folder under this project path as the working directory.
2. Create the hardware platform; specific steps can refer to the previous section.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-186-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-186-image-02.jpg)

3. In the lower right corner, inside axi_gpio_0, select Import Example

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-187-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-187-image-02.jpg)

4. Select "xgpio_example"
5. Open the source file

Here we modify the macro definition of LED to the value 0xF, corresponding to 4 LED lights.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-188-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-188-image-02.jpg)

6. Compile the application to generate an elf file

### 5.2.3 Download and verification

Here we download the bit file and elf file in Vitis. Please refer to the previous introduction for the download steps.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-189-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-189-image-02.jpg)

After the download is successful, you can see that the four LEDs on the board keep flashing.

## 5.3 PS-side Reading and Writing PL Registers

Many times, only a simple data path is needed between the PS and PL. The PS only needs to send a limited number of parameters to the PL, and the PL only needs to feedback limited status data to the PS. In this case, only an AXI-Lite interface needs to be implemented inside the PL. The PS accesses the registers via the AXI interface, providing parameters to the PL and also reading back the status of the PL.

### 5.3.1 Hardware Project Setup

Here we still build the hardware project based on the previous IPI project.

1. We build the hardware project for this experiment according to the previous IPI project;
2. Double-click the IP to enable the AXI HPM0 LPD interface;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-190-image-01.jpg)

3. We add the up_axi.v source file to the project (the up_axi module implements the AXI-Lite protocol, which is open-source code from ADI, and we only need to focus on and use the user-side signals).

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-191-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-191-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-192-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-192-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-192-image-03.jpg)

4. After adding it, we right-click in the IPI interface and add a module

Select the up_axi.v module that we just added

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-193-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-193-image-02.jpg)

Click [OK]

5. We select automatic connection [Run Connection Automation]

Click [OK]

6. We bring out the user interface signals and clock reset signals of up_axi

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-194-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-194-image-02.jpg)

7. Validate Design

The following error is indicated here, showing that the clock frequencies are inconsistent.
We select up_axi, modify the frequency of the up_axi bus, and then re-validate;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-195-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-195-image-02.jpg)

8. We create a new top-level file, instantiate the bd file, and the register read/write module;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-196-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-196-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-196-image-03.jpg)

9. Generate the bitstream and export the hardware engineering xsa file;

### 5.3.2 Software Project Setup

After building the hardware project in Vivado and exporting the xsa file, create a
vitis folder under the project directory as the working directory for Vitis.

1. Log in to Vitis, select the vitis folder under the project path as the working directory, and click [Launch]
2. Compile the hardware platform
3. Create a new application

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-197-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-197-image-02.jpg)

Intermediate steps are omitted, set the application name
Finally, select the 'Hello World' template and click [Finish]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-198-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-198-image-02.jpg)

4. Modify the helloworld.c file and add register read/write code. In our hardware engineering work, we have enabled 3 registers, and here we perform read/write tests on these three registers;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-199-image-01.jpg)

5. Compile the Application

### 5.3.3 Download Verification

We debug the application in Vitis.

1. Right-click on the application, select 【Debug As】 -> 【Debug configurations...】

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-200-image-01.jpg)

2. Here we Step Over to run the program step by step

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-201-image-01.jpg)

At the same time, open Chipscope to observe the read and write signals of the registers. We set the read and write requests as trigger signals, then step through the C program to check the changes in Chipscope signals.

3. When we execute the code in Vitis, we can see the signal changes in ILA.

Write 0x01020304 to the register offset address 0.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-202-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-202-image-02.jpg)

Write 0x05060708 to the register at offset address 4
Write 0x090a0b0c to the register at offset address 8
Read back 0x01020304 from the register at offset address 0

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-203-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-203-image-02.jpg)

## 5.4 AXI-DMA Loopback Test

AXI DMA provides high-bandwidth direct memory access between system memory and bus-based AXI4-Stream target peripherals.
In the system, AXI DMA is interconnected with the processor and other devices via AXI Interconnect. The system processor accesses the internal registers of the DMA through the AXI4-Lite interface, writes configuration information to it, and then efficiently performs data transfer based on the configuration information; DMA can also initiate S/G transfer mode, obtain descriptors from DDR through an independent AXI S/G channel, and then coordinate data transfer between peripherals and memory.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-204-image-01.jpg)

AXI DMA utilizes three types of buses:
 AXI-Lite is used for configuring registers.
 AXI4 Memory Map is used for interacting with memory, which is further divided into two interfaces: AXI4 Memory Map Read and AXI4 Memory Map Write, one for reading and one for writing.
 AXI4 Stream interface is used for reading and writing to peripherals, where AXI4 Stream Master (MM2S) is used for writing to peripherals, and AXI4 Stream Slave (S2MM) is used for reading from peripherals.
AXI DMA provides three modes: Direct Register mode, Scatter/Gather mode, and Cyclic DMA mode. Here, we introduce the commonly used Direct Register mode and Scatter/Gather mode. Direct Register DMA mode is also called Simple DMA. The Direct Register mode provides a configuration for performing simple DMA transfers on MM2S and S2MM channels, which requires fewer FPGA resources. Simple DMA allows an application to define a single transaction between the DMA and the Device. It has two channels: one from DMA to Device, and one from Device to DMA. The application must set the buffer address and length fields to start the transfer on the corresponding channel. Scatter/Gather DMA mode allows data to be transferred to multiple memory areas or from multiple memory areas in a single DMA transaction. It is equivalent to linking multiple Simple DMA requests together.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-205-image-01.jpg)

Together. SGDMA allows applications to define a list of transactions in memory, and the hardware will process these transactions without further intervention from the application. During this time, the application can continue to add more work to keep the hardware busy. Users can check if the transactions are complete through polling or interrupts. SGDMA processes entire data packets (defined as a series of data bytes representing a message) and allows a data packet to be divided into one or more transactions.
In this chapter, we use the Direct Register mode, adopting the DMA example provided by Vitis, with slight modifications. After the DMA work is completed, an end interrupt is issued to notify the CPU to read the memory data.

### 5.4.1 Hardware Project Setup

Here, we still build the hardware project based on the IPI project from the previous chapter.

1. We build the hardware project for this experiment according to the previous IPI project;
2. Double-click the mpsoc, enable HPM0, HP0, and PL to PS interrupts, and click [OK]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-206-image-01.jpg)

3. Click '+', and add the AXI DMA module;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-207-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-207-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-208-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-208-image-02.jpg)

4. Set the AXI DMA IP parameters
5. Add the AXI Stream Data FIFO module;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-209-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-209-image-02.jpg)

6. The parameter settings are as follows

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-210-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-210-image-02.jpg)

7. Add the ILA module and click Auto Connect

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-211-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-211-image-02.jpg)

8. Create HDL Wrapper and generate bitstream;
9. Export hardware xsa file

Click [Next]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-212-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-212-image-02.jpg)

Select the one that contains 'bit', click [Next]
Set the name and export path, click [Next]
Click [Finish]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-213-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-213-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-213-image-03.jpg)

### 5.4.2 Software Engineering Setup

We set up the hardware project in Vivado, and after exporting the xsa file, we create a
vitis folder under the project directory to serve as the working directory for Vitis.

1. Log in to Vitis, select the vitis folder under this project path as the working directory, and click [Launch]
2. Choose to create the hardware platform

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-214-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-214-image-02.jpg)

Set the name, click [Next]
Click [Browse], select the generated xsa file;
Click [Finish]

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-215-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-215-image-02.jpg)

3. Compile the hardware platform
4. Click [Import Example] to import the reference example of AXI DMA

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-216-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-216-image-02.jpg)

5. Select the simple_poll example
6. Modify the example source file: set MAX_PKT_LEN, which is the length in bytes, TEST_START_VALUE as the starting data value, and NUMBER_OF_TRANSFERS as the number of test times;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-217-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-217-image-02.jpg)

Enable the IOC interrupt of S2MM and disable all interrupts of MM2S. After S2MM receives the data, it will trigger an interrupt.
Enable the MM2S path and the S2MM path.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-218-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-218-image-02.jpg)

### 5.4.3 Download Verification

1. We debug the application in Vitis.
2. After waiting for the bit to download, open the ILA in Vivado and set the trigger conditions.
3. In the Debug interface of Vitis, without setting breakpoints, click Resume.
4. At this point, you can see that the ILA has been triggered and can observe the collected data.

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-219-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-219-image-02.jpg)

In the serial debugging tool, you can see the printed information.

5. We can also set breakpoints in Vitis debugging to observe memory information;

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-220-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-220-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-220-image-03.jpg)

![RFEVM216 FPGA tutorial illustration](../../assets/fpga-tutorial/page-221-image-01.jpg)
