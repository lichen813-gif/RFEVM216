# 5.4 AXI-DMA Loopback Test

[Switch to 中文](../../../zh/fpga-tutorial/05-ps-pl-interconnect/04-axi-dma-loopback.md)

[Back to chapter overview](index.md)

AXI DMA provides high-bandwidth direct memory access between system memory and bus-based AXI4-Stream target peripherals.
In the system, AXI DMA is interconnected with the processor and other devices via AXI Interconnect. The system processor accesses the internal registers of the DMA through the AXI4-Lite interface, writes configuration information to it, and then efficiently performs data transfer based on the configuration information; DMA can also initiate S/G transfer mode, obtain descriptors from DDR through an independent AXI S/G channel, and then coordinate data transfer between peripherals and memory.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-204-image-01.jpg)

AXI DMA utilizes three types of buses:
 AXI-Lite is used for configuring registers.
 AXI4 Memory Map is used for interacting with memory, which is further divided into two interfaces: AXI4 Memory Map Read and AXI4 Memory Map Write, one for reading and one for writing.
 AXI4 Stream interface is used for reading and writing to peripherals, where AXI4 Stream Master (MM2S) is used for writing to peripherals, and AXI4 Stream Slave (S2MM) is used for reading from peripherals.
AXI DMA provides three modes: Direct Register mode, Scatter/Gather mode, and Cyclic DMA mode. Here, we introduce the commonly used Direct Register mode and Scatter/Gather mode. Direct Register DMA mode is also called Simple DMA. The Direct Register mode provides a configuration for performing simple DMA transfers on MM2S and S2MM channels, which requires fewer FPGA resources. Simple DMA allows an application to define a single transaction between the DMA and the Device. It has two channels: one from DMA to Device, and one from Device to DMA. The application must set the buffer address and length fields to start the transfer on the corresponding channel. Scatter/Gather DMA mode allows data to be transferred to multiple memory areas or from multiple memory areas in a single DMA transaction. It is equivalent to linking multiple Simple DMA requests together.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-205-image-01.jpg)

Together. SGDMA allows applications to define a list of transactions in memory, and the hardware will process these transactions without further intervention from the application. During this time, the application can continue to add more work to keep the hardware busy. Users can check if the transactions are complete through polling or interrupts. SGDMA processes entire data packets (defined as a series of data bytes representing a message) and allows a data packet to be divided into one or more transactions.
In this chapter, we use the Direct Register mode, adopting the DMA example provided by Vitis, with slight modifications. After the DMA work is completed, an end interrupt is issued to notify the CPU to read the memory data.

## 5.4.1 Hardware Project Setup

Here, we still build the hardware project based on the IPI project from the previous chapter.

1. We build the hardware project for this experiment according to the previous IPI project;
2. Double-click the mpsoc, enable HPM0, HP0, and PL to PS interrupts, and click [OK]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-206-image-01.jpg)

3. Click '+', and add the AXI DMA module;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-207-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-207-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-208-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-208-image-02.jpg)

4. Set the AXI DMA IP parameters
5. Add the AXI Stream Data FIFO module;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-209-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-209-image-02.jpg)

6. The parameter settings are as follows

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-210-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-210-image-02.jpg)

7. Add the ILA module and click Auto Connect

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-211-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-211-image-02.jpg)

8. Create HDL Wrapper and generate bitstream;
9. Export hardware xsa file

Click [Next]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-212-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-212-image-02.jpg)

Select the one that contains 'bit', click [Next]
Set the name and export path, click [Next]
Click [Finish]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-213-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-213-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-213-image-03.jpg)

## 5.4.2 Software Engineering Setup

We set up the hardware project in Vivado, and after exporting the xsa file, we create a
vitis folder under the project directory to serve as the working directory for Vitis.

1. Log in to Vitis, select the vitis folder under this project path as the working directory, and click [Launch]
2. Choose to create the hardware platform

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-214-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-214-image-02.jpg)

Set the name, click [Next]
Click [Browse], select the generated xsa file;
Click [Finish]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-215-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-215-image-02.jpg)

3. Compile the hardware platform
4. Click [Import Example] to import the reference example of AXI DMA

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-216-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-216-image-02.jpg)

5. Select the simple_poll example
6. Modify the example source file: set MAX_PKT_LEN, which is the length in bytes, TEST_START_VALUE as the starting data value, and NUMBER_OF_TRANSFERS as the number of test times;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-217-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-217-image-02.jpg)

Enable the IOC interrupt of S2MM and disable all interrupts of MM2S. After S2MM receives the data, it will trigger an interrupt.
Enable the MM2S path and the S2MM path.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-218-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-218-image-02.jpg)

## 5.4.3 Download Verification

1. We debug the application in Vitis.
2. After waiting for the bit to download, open the ILA in Vivado and set the trigger conditions.
3. In the Debug interface of Vitis, without setting breakpoints, click Resume.
4. At this point, you can see that the ILA has been triggered and can observe the collected data.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-219-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-219-image-02.jpg)

In the serial debugging tool, you can see the printed information.

5. We can also set breakpoints in Vitis debugging to observe memory information;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-220-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-220-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-220-image-03.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-221-image-01.jpg)
