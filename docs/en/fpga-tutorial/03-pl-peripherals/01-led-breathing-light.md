# 3.1 LED Breathing Light Experiment

[Switch to 中文](../../../zh/fpga-tutorial/03-pl-peripherals/01-led-breathing-light.md)

[Back to chapter overview](index.md)

The breathing light is an LED that is controlled by a microprocessor, gradually dimming, brightening, and then dimming again, imitating the way a person breathes.
The FPGA pin levels only have two states, '0' and '1'. Therefore, the breathing light is achieved by changing the duration of the high-level output within a unit of time on the pin, that is, making the FPGA pin output a series of PWM wave signals and continuously changing the duty cycle of the PWM wave to control the brightness of the LED.
The diagram of PWM duty cycle adjustment is shown below:
Figure 3 PWM Duty Cycle Diagram of Breathing Light

## 3.1.1 Hardware Design

The RFEVM216 development board has 4 user-controllable LED lights. Its schematic diagram is shown below:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-011-image-01.jpg)

Figure 4 LED Lamp Hardware Schematic

## 3.1.2 Hardware Project Setup

1. On the PC, open Vivado
2. Click Create Project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-012-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-012-image-02.jpg)

3. Click Next
4. Set the project name and location, then click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-013-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-013-image-02.jpg)

5. Click Next
6. Select FPGA model xczu49dr-fsvf1760-2-i, and click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-014-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-014-image-02.jpg)

7. Click Finish

Here we can see the project we created

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-015-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-015-image-02.jpg)

8. In the Flow Navigator window, click Add Source
9. Select the design files to add, then click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-016-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-016-image-02.jpg)

10. Click Create Files
11. Set the name, click OK

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-017-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-017-image-02.jpg)

12. Click Finish
13. Do not add a port for now, click OK

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-018-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-018-image-02.jpg)

Click Yes

14. After completion, you can see the .v file we newly created

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-019-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-019-image-02.jpg)

15. Double-click breath_led, then enter the following code

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-020-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-020-image-02.jpg)

16. Click Add Source

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-021-image-01.jpg)

17. Choose to add or create a constraint file, click Next
18. Click Create File

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-022-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-022-image-02.jpg)

19. Set the name, click OK
20. Click Finish

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-023-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-023-image-02.jpg)

21. Here you can see the newly created constraint file

Double-click rfevm_led.xdc and enter the following constraints:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-024-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-024-image-02.jpg)

22. In the Flow Navigator, click Generate Bitstream
23. Click OK and wait for the bitstream to be generated

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-025-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-025-image-02.jpg)

24. After the bit generation is completed, select [View Reports] and click OK

## 3.1.3 Download Verification

Use a USB to Type-C cable, connect one end to the board and the other end to the PC, then power on the board.
In the Vivado interface, click Open Hardware Manager -> Open Target -> Auto Connect

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-026-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-026-image-02.jpg)

On the device, right-click and select Program device

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-027-image-01.jpg)

Click Program
After the download is complete, you can see the LEDs on the baseboard gradually changing from dim to bright, and then from bright to dim,
which produces a "breathing" effect.
