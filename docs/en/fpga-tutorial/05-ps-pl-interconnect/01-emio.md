# 5.1 Using EMIO on the PS side

[Switch to 中文](../../../zh/fpga-tutorial/05-ps-pl-interconnect/01-emio.md)

[Back to chapter overview](index.md)

Previously, the experiment of the LED breathing light on the PL side was introduced. Here, we use the PS side to control the on/off of the LED on the PL side.
The PL side’s extended IO can also be controlled in this way.
Zynq GPIO is divided into MIO (multiplexed I/O) and EMIO (extended multiplexed I/O).
MIO is the multifunction IO interface on the PS side. The IO is connected to the PS side, and each IO can be configured as GPIO, SPI, UART, TIMER, Ethernet, USB, and other functions according to needs. Since MIO is not visible to the PL side, the PL side cannot use MIO pins.
EMIO is the extended IO of MIO, connected to the PL side. Since EMIO is visible to both the PS and PL sides, both can use EMIO pins. Generally, when the PS side MIO resources are insufficient, the PS side can expand interfaces through EMIO. The usage of EMIO is similar to MIO, with the difference being that EMIO requires using the Vivado constraint file to assign pins.
MPSoC provides 96 GPIOs to the PL, connected to the PL via EMIO pins. Here we use
Use EMIO to connect to the LED on the PL side and control its status in Vitis.

## 5.1.1 Hardware Project Setup

1. Set up the hardware project. Follow the steps for setting up the IPI project in the previous chapter to add the MPSOC IP core.
2. Double-click the IP to enable the emio interface, and select 4 for the number of IOs (corresponding to the 4 LED lights on the baseboard);
3. Here we bring out the emio output emio_gpio_o and Make External.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-162-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-162-image-02.jpg)

4. Check if there are any errors in the design

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-163-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-163-image-02.jpg)

5. Creating HDL Wrapper...

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-164-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-164-image-02.jpg)

6. Create constraint file
7. Compile to generate bit file

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-165-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-165-image-02.jpg)

8. After the compilation is complete, export the hardware project for subsequent Vitis software development;

Here we choose to include the bitstream and click [Next]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-166-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-166-image-02.jpg)

Set the name and path of xsa

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-167-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-167-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-167-image-03.jpg)

After clicking [Finish], you can see the newly generated xsa file under the project path.

## 5.1.2 Software Project Setup

After setting up the hardware project in Vivado and exporting the xsa file, create a vitis folder under the project directory as the working directory for Vitis.

1. Log in to Vitis and select the vitis folder under the project path as the working directory

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-168-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-168-image-02.jpg)

2. Select 【Create Platform Project】

Set the platform name, and click 【Next】

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-169-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-169-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-170-image-01.jpg)

Click Browse here and select the generated xsa file

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-171-image-01.jpg)

Click [Finish] to generate the hardware platform

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-172-image-01.jpg)

3. Compile platform
4. After compilation is complete, create a new application project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-173-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-173-image-02.jpg)

Click [Next]
Click [Next]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-174-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-174-image-02.jpg)

Set the application project name and click 【Next】

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-175-image-01.jpg)

Click [Next]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-176-image-01.jpg)

Select the "Hello World" template and click [Finish]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-177-image-01.jpg)

5. Here, we modify the hello world source file and add GPIO control code

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-178-image-01.jpg)

Note: The MPSoC has 78 MIOs, the numbering of EMIO starts from 78;

## 5.1.3 Download and Verification

Here we download the bit file and elf file in Vitis. Please refer to the previously introduced steps for downloading.
You can see that the four LED lights on the board keep flashing.
