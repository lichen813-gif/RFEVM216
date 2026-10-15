# 5.3 PS-side Reading and Writing PL Registers

[Switch to 中文](../../../zh/fpga-tutorial/05-ps-pl-interconnect/03-pl-register-access.md)

[Back to chapter overview](index.md)

Many times, only a simple data path is needed between the PS and PL. The PS only needs to send a limited number of parameters to the PL, and the PL only needs to feedback limited status data to the PS. In this case, only an AXI-Lite interface needs to be implemented inside the PL. The PS accesses the registers via the AXI interface, providing parameters to the PL and also reading back the status of the PL.

## 5.3.1 Hardware Project Setup

Here we still build the hardware project based on the previous IPI project.

1. We build the hardware project for this experiment according to the previous IPI project;
2. Double-click the IP to enable the AXI HPM0 LPD interface;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-190-image-01.jpg)

3. We add the up_axi.v source file to the project (the up_axi module implements the AXI-Lite protocol, which is open-source code from ADI, and we only need to focus on and use the user-side signals).

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-191-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-191-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-192-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-192-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-192-image-03.jpg)

4. After adding it, we right-click in the IPI interface and add a module

Select the up_axi.v module that we just added

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-193-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-193-image-02.jpg)

Click [OK]

5. We select automatic connection [Run Connection Automation]

Click [OK]

6. We bring out the user interface signals and clock reset signals of up_axi

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-194-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-194-image-02.jpg)

7. Validate Design

The following error is indicated here, showing that the clock frequencies are inconsistent.
We select up_axi, modify the frequency of the up_axi bus, and then re-validate;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-195-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-195-image-02.jpg)

8. We create a new top-level file, instantiate the bd file, and the register read/write module;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-196-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-196-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-196-image-03.jpg)

9. Generate the bitstream and export the hardware engineering xsa file;

## 5.3.2 Software Project Setup

After building the hardware project in Vivado and exporting the xsa file, create a
vitis folder under the project directory as the working directory for Vitis.

1. Log in to Vitis, select the vitis folder under the project path as the working directory, and click [Launch]
2. Compile the hardware platform
3. Create a new application

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-197-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-197-image-02.jpg)

Intermediate steps are omitted, set the application name
Finally, select the 'Hello World' template and click [Finish]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-198-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-198-image-02.jpg)

4. Modify the helloworld.c file and add register read/write code. In our hardware engineering work, we have enabled 3 registers, and here we perform read/write tests on these three registers;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-199-image-01.jpg)

5. Compile the Application

## 5.3.3 Download Verification

We debug the application in Vitis.

1. Right-click on the application, select 【Debug As】 -> 【Debug configurations...】

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-200-image-01.jpg)

2. Here we Step Over to run the program step by step

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-201-image-01.jpg)

At the same time, open Chipscope to observe the read and write signals of the registers. We set the read and write requests as trigger signals, then step through the C program to check the changes in Chipscope signals.

3. When we execute the code in Vitis, we can see the signal changes in ILA.

Write 0x01020304 to the register offset address 0.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-202-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-202-image-02.jpg)

Write 0x05060708 to the register at offset address 4
Write 0x090a0b0c to the register at offset address 8
Read back 0x01020304 from the register at offset address 0

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-203-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-203-image-02.jpg)
