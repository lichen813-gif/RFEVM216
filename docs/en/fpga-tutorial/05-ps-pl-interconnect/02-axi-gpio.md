# 5.2 Usage of AXI GPIO on the PL Side

[Switch to 中文](../../../zh/fpga-tutorial/05-ps-pl-interconnect/02-axi-gpio.md)

[Back to chapter overview](index.md)

AXI GPIO is a specific type of GPIO (General Purpose Input/Output) controller that communicates using the AXI (Advanced eXtensible Interface) bus protocol.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-179-image-01.jpg)

AXI GPIO is used to control and read the status of GPIO pins. It is widely used in embedded systems for communication with processors or other peripherals to control and read the status of GPIO pins. It can be used to connect various peripherals, such as LEDs, buttons, sensors, etc., to interact with the external environment. Here we use AXI GPIO to control the on-off changes of the LEDs on the board.

## 5.2.1 Hardware Project Setup

1. According to the project setup steps in the previous chapter on IPI, set up the hardware project for this experiment.
2. In the IPI interface, right-click to add the AXI GPIO IP core.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-180-image-01.jpg)

3. Here we only enable GPIO 1. We only control the LED output, so we enable all outputs with a bit width of 4 bits, then click [OK]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-181-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-181-image-02.jpg)

4. In the MPSoC, we enable the LPD interface, and then click Auto Connect [Run Connection Automation]

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-182-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-182-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-183-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-183-image-02.jpg)

5. Check if the design has any errors

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-184-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-184-image-02.jpg)

6. Create an HDL wrapper, then generate the bit file.
7. Add an XDC constraint file, constrain the LED pins, and generate the bit file.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-185-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-185-image-02.jpg)

8. Export the hardware engineering xsa file (including the bitstream).

## 5.2.2 Software Project Setup

After setting up the hardware project in Vivado and exporting the xsa file, create a
vitis folder under the project directory as the working directory for Vitis.

1. Log in to Vitis and select the vitis folder under this project path as the working directory.
2. Create the hardware platform; specific steps can refer to the previous section.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-186-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-186-image-02.jpg)

3. In the lower right corner, inside axi_gpio_0, select Import Example

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-187-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-187-image-02.jpg)

4. Select "xgpio_example"
5. Open the source file

Here we modify the macro definition of LED to the value 0xF, corresponding to 4 LED lights.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-188-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-188-image-02.jpg)

6. Compile the application to generate an elf file

## 5.2.3 Download and verification

Here we download the bit file and elf file in Vitis. Please refer to the previous introduction for the download steps.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-189-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-189-image-02.jpg)

After the download is successful, you can see that the four LEDs on the board keep flashing.
