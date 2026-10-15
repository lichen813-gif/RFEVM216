# 4.1 IPI Design Creation

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/01-ipi-design.md)

[Back to chapter overview](index.md)

Vivado IP Integrator (IPI) is an IP integration design interface provided by the Vivado integrated development environment. The IP Integrator is a graphical design and development environment that supports script configuration and connection. In the IP Integrator, IP can be used for processor-based designs as well as non-processor pure logic design development.
Here, we enable all PS peripherals in the IPI; subsequent PS peripheral experiments only need to be operated under Vitis.

## 4.1.1 Hardware Project Setup

1. Open Vivado
2. Select Create Project
3. Click Next
4. Set the project name (rfevm216_ipi) and location (E:/rfevm216/demo), then click Next;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-072-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-072-image-02.jpg)

5. Select RTL Project, click Next
6. Select chip model xczu49dr-fsvf1760-2-i, click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-073-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-073-image-02.jpg)

7. Click Finish
8. Under IPI (IP INTEGRATOR) select Create Block Design

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-074-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-074-image-02.jpg)

9. Set the design name: system, click OK
10. Click + (Add IP)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-075-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-075-image-02.jpg)

11. Select Zynq UltraScale+ MPSoC
12. Double-click Zynq UltraScale+ MPSoC or right-click and choose Customize Block...

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-076-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-076-image-02.jpg)

13. The architecture diagram of the MPSoC hard core will be displayed below

 In the IO Configuration window
Configure the voltages of Bank0, Bank1, Bank2, and Bank3 to LVCMOS18

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-077-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-077-image-02.jpg)

 In the Low Speed->Memory Interface interface, check QSPI and SD 0, SD 1;
QSPI: Dual Parallel, x4

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-078-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-078-image-02.jpg)

SD 0: MIO13..22, eMMC, 8Bit, Reset MIO23
SD 1: MIO46..51, SD 2.0, 4Bit, CD MIO45
 In the Low Speed -> I/O Peripherals interface, check I2C 1, UART 0, UART 1;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-079-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-079-image-02.jpg)

In the Low Speed -> Processing Unit interface, check TTC 0, TTC1, TTC 2, TTC 3;
In the High Speed interface, check GEM 3, USB 0, USB 3.0, PCIe, Display Port;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-080-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-080-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-081-image-01.jpg)

 In the Clock Configuration window
Configure the input clock as shown in the figure below, the rest can remain default;

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-082-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-083-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-083-image-02.jpg)

 In the DDR Configuration window, configure the DDR parameters as shown in the figure below

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-084-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-084-image-02.jpg)

 In the PCIe Configuration window, mainly configure the device port type and device ID; other settings can remain default;
 On the PS-PL Configuration page, configure as follows.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-085-image-01.jpg)

14. Click OK
15. Select Tools->Validate Design to check if there are any errors in the settings
16. Right-click on the system and select Create HDL Wrapper

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-086-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-086-image-02.jpg)

17. Select 'Let Vivado manage wrapper and auto-update'
18. Click 'Run Synthesis' (here we only use PS resources, no bitstream is generated)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-087-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-087-image-02.jpg)

19. After completing the integration, click OK
20. Select File->Export->Export Hardware

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-088-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-088-image-02.jpg)

21. Click Next
22. Here we don't have bits, use the default configuration, click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-089-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-089-image-02.jpg)

23. Set the name and path, click Next
24. Click Finish

Here we can see the newly generated xsa file:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-090-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-090-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-090-image-03.jpg)

## 4.1.2 Software Engineering Setup

In the previous section, we set up the hardware project in Vivado and exported the XSA file. Here, create a Vitis folder under the project directory to serve as the working directory for Vitis.

1. Log in to Vitis
2. Select the working directory and click Launch

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-091-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-091-image-02.jpg)

3. Click Create Platform Project
4. Set the project name, then click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-092-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-092-image-02.jpg)

5. Click Browse..

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-093-image-01.jpg)

6. Select the previously generated xsa file and click Finish

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-094-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-094-image-02.jpg)

7. Right-click on the generated plf and click Compile

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-095-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-095-image-02.jpg)

At this point, our software engineering setup is complete. From here, we can carry out PS bare-metal experiments based on this foundation;
