# 4.6 Use of DisplayPort on the PS Side

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/06-displayport.md)

[Back to chapter overview](index.md)

## 4.6.1 Hardware Design

The RFEVM216 baseboard has one DP display interface, which can be connected to a DP monitor for output. The design block diagram is shown below:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-137-image-01.jpg)

## 4.6.2 Software Design

1. Double-click platform.spr and select Board Support Package
2. Click Import Example, then select the xdpdma_video_example example, and click OK

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-138-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-138-image-02.jpg)

3. Select the application project, right-click and click Build Project

## 4.6.3 Download and Verification

Here we need to connect one end of the DP data cable to a monitor with a DP interface, and the other end to the DP interface of the board. Then power on the development board.
Right-click the application project, select Run As->Launch Hardware (Single Application Debug)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-139-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-139-image-02.jpg)

Open the serial terminal, after the download is complete, you can check the serial output:
At the same time, color bars are displayed on the monitor

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-140-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-140-image-02.jpg)
