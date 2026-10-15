# 4. PS Peripherals

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/index.md)

## Experiments

- [4.1 IPI Design Creation](01-ipi-design.md)
- [4.2 Experiencing ARM, Bare-Metal Output of 'Hello World'](02-arm-hello-world.md)
- [4.3 PS-side RTC Interrupt Experiment](03-rtc-interrupt.md)
- [4.4 Use of IIC on the PS side](04-iic.md)
- [4.5 LWIP for PS-side Ethernet](05-lwip-ethernet.md)
- [4.6 Use of DisplayPort on the PS Side](06-displayport.md)
- [4.7 SD Card Read/Write TXT Text Experiment](07-sd-card.md)
- [4.8 USB Slave Function Test Based on PS](08-usb-slave.md)

## Chapter Overview

This chapter mainly introduces the configuration of the Zynq core and the application of PS end peripherals, such as basic experiments with MIO, UART, Ethernet, and RTC.
The previous experiments were all conducted on the PL side, which can be seen to have no difference from the ordinary FPGA development process. The main advantage of Zynq is the reasonable combination of FPGA and ARM, which places higher demands on developers. From this chapter onwards, we start using ARM, which is what we refer to as PS.
