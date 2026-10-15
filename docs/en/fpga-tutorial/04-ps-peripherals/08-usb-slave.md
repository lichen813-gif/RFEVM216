# 4.8 USB Slave Function Test Based on PS

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/08-usb-slave.md)

[Back to chapter overview](index.md)

The USB interface of Zynq can act as both a USB HOST and a USB DEVICE (SLAVE). In most cases, the USB function is used under Linux. Here, we will test the USB function in a bare-metal environment.
We use the officially provided demo to test the USB device by simulating the function of a USB flash drive.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-154-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-154-image-02.jpg)

## 4.8.1 Hardware Design

Figure 16 USB Interface Schematic

## 4.8.2 Software Design

4. Log in to Vitis, switch to the previous working directory, then double-click platform.spr, select Board Support Package, where you can see the documentation link for psu_usb_xhci_0 and import examples.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-155-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-155-image-02.jpg)

5. Click Import Example, then select the xusb_poll_example example, and click OK
6. You can see the imported example application project
7. Select the application project, right-click and click Build Project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-156-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-156-image-02.jpg)

Compilation information can be seen in the Console window.

## 4.8.3 Download Verification

Here we need to use a USB A-to-A data cable, with one end connected to the USB interface of the RFEVM216, and the other end connected to the PC. Then power on the development board.
Right-click the application project, and select Run As->Launch Hardware (Single Application Debug)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-157-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-157-image-02.jpg)

Open the serial terminal. After the download is complete, you can check the serial output:
On the PC side, the following window will pop up. Click 'Format Disk' to proceed.
In My Computer, you can see a U disk virtualized by the DDR RAM. You can copy and paste files just like a normal U disk. Note that this U disk will lose data when powered off, so do not store important files on it.
The capacity can be configured in the program. Please do not exceed the DDR capacity on the board.
We can use the CrystalDiskMark tool recommended by Xilinx Wiki to test the U disk's performance.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-158-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-158-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-158-image-03.jpg)

## 4.8.4 Reference Documents

https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842468/ZynqMp+USB+Standalone+Driver

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-159-image-01.jpg)
