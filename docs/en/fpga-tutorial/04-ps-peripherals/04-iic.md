# 4.4 Use of IIC on the PS side

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/04-iic.md)

[Back to chapter overview](index.md)

## 4.4.1 Hardware Design

The PS side IIC is connected to an external EEPROM. This section introduces how to use IIC to read and write the external device.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-119-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-119-image-02.jpg)

## 4.4.2 Software Design

1. Log in to Vitis, switch to the previous working directory, then double-click platform.spr, select Board Support Package, and you can see the documentation link and import example for psu_i2c_1.
2. Click Import Example, then select the xiicps_eeprom_polled_example example, and click OK

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-120-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-120-image-02.jpg)

3. You can see the imported example application project.
4. The device address of the EEPROM is defined at the beginning of the program. This address is the device address the system uses to access external IIC peripherals. Here, the EEPROM address is changed to 0x50, then saved.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-121-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-121-image-02.jpg)

The device address of the EEPROM can be found in the AT24CM01 chip manual.
Among them, A1 and A2 are directly connected to the ground in the hardware, which is 0;
The program flow is as follows:
Clear ReadBuffer to 0, assign incrementing data to WriteBuffer -> write 32 bytes to EEPROM -> read 16 bytes from EEPROM into ReadBuffer -> check if correct -> return.

5. Select the application project, right-click and choose Build Project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-122-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-122-image-02.jpg)

Compilation information can be seen in the Console window

## 4.4.3 Download Verification

First, we connect the download cable (USB to Type-C cable) to the JTAG interface of the development board, then

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-123-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-123-image-02.jpg)

One end is connected to the computer. Finally, turn on the power switch of the development board.
Right-click the application project, select Run As -> Launch Hardware (Single Application Debug)
Open the serial terminal, and after the download is complete, you can view the serial output:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-124-image-01.jpg)
