# 4.3 PS-side RTC Interrupt Experiment

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/03-rtc-interrupt.md)

[Back to chapter overview](index.md)

The RTC (Real Time Clock) unit provides precise time to the system and application software.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-112-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-112-image-02.jpg)

Calibration. To meet the need for high precision, the RTC also includes a calibration circuit to compensate for temperature and voltage fluctuations. The RTC is powered by VCC-PSAUX or VCC-PSBATT. When the auxiliary power is available, the RTC uses it to keep the counter running. When the auxiliary power VCC PSAUX is unavailable, the RTC automatically switches to the battery power VCC PSBATT.
The RTC has the following features:

- Can operate using either auxiliary power or battery power. When the system loses power, the RTC automatically switches to battery power to maintain continuous operation.
- Alarm settings and periodic interrupts (timer interrupts).
- Complex calibration circuit for high-precision timing.
- 32-bit second counter, capable of counting approximately 136 years.
- Three counters: 32-bit second counter, 16-bit tick counter for measuring seconds based on a 32 kHz crystal oscillator, and a 4-bit fractional counter for calibration.

Figure 11 RTC controller structure diagram

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-113-image-01.jpg)

Figure 12 RTC Function Diagram

## 4.3.1 Software Design

1. Log in to Vitis, switch to the previous working directory, then double-click platform.spr, select Board Support Package, and you can see the documentation and import example for psu_rtc.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-114-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-114-image-02.jpg)

2. Click Import Example, and the import example interface as shown in the figure below will pop up;
3. Here we select the third official example, the RTC periodic alarm interrupt example (xrtcpsu_periodic_alarm_interrupt_example), and click OK
4. Here we have imported the example project

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-115-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-115-image-02.jpg)

5. Select the application project, right-click and then choose Build Project to compile the project. The compilation progress can be viewed in the console panel at the bottom of the tool, as shown in the figure below:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-116-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-116-image-02.jpg)

## 4.3.2 Download Verification

First, connect the Type-C end of the USB to Type-C cable to the JTAG interface on the RFEVM2116 development board, and connect the other end of the USB to Type-C cable to the computer. Connect the development board power and turn on the development board.
Download the program, right-click the application project, and select Run As->Run Configuration...

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-117-image-01.jpg)

Double-click the Single Application Debug item
Select the Target Setup tab, use the default configuration, and click Run

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-118-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-118-image-02.jpg)

After the download is complete, you can see the information that the serial port needs to print in the serial debugging terminal:
