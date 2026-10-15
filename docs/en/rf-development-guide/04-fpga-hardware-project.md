# 2.3 FPGA Hardware Project

[Switch to 中文](../../zh/rf-development-guide/04-fpga-hardware-project.md)

> This chapter is translated from the Chinese source PDF. Figures and UI screenshots retain their original labels so that they match the hardware and software.  
> Source PDF: `RFEVM216开发板射频开发指南s.pdf`  
> Source pages: 18-22

<a id="page-18"></a>
## Source PDF page 18

Step Attenuator Settings.  
RF-DAC  
Enable Real Time Ports: Enable RF-DAC Fast Shutdown and pl_event ports.  
Enable Real Time NCO Ports: In the DUC, the mixer frequency and phase can be modified in real time. Selecting this option will enable the real-time NCO ports of the RF-DAC.  
Output Current: Choose RF-DAC output currents of 20mA and 32mA. In 20mA mode, DAC_AVTT is 2.5V. In 32mA mode, DAC_AVTT is 3.0V.  
Variable Output Current Mode (Gen3): When the variable output current mode is off, the output current is set by the output current option. In 20mA mode, DAC_AVTT is 2.5V. In 32mA mode, DAC_AVTT is 3.0V. After enabling the variable output mode, the output current can be set on a per-chip basis through the Variable Output Current field in the RF-DAC tab. DAC_AVTT is set to 3.0V.  
Enable Real Time Variable Output Power Ports (Gen3): Enable real-time variable output power ports (third generation). If this option is selected, a real-time VOP signal interface will be added for each enabled RF-DAC, allowing real-time updating of output power.  
2.3 FPGA Hardware Project Introduction  
The FPGA hardware project is built using Vivado 2021.2 and includes the PL logic part and PS processor configuration part. The LMK04828 clock chip, Axi-Lite configuration of AD/DA cores, and Axi-Lite read/write of PS-PL interaction registers are configured via SPI.  
When opening the project in Vivado, the Source interface is as follows:

---

<a id="page-19"></a>
## Source PDF page 19

File Analysis:   
File Name Hierarchy Function   
adaloop_top 0 Top-level file, instantiates submodules   
system_wrapper 1 BD wrapper file, includes PS and RF converter modules   
user_control 1 Register read/write module (currently not used)   
dds_complier_0 1 DDS IP core, generates CW test source for RF-DAC   
ila_0/ila_1 1 Chipscope, observes AD signals   
We open the BD file system in Vivado software, and the interface is shown as follows

### Figures

![RFEVM216 Development Board RF Development Guide, page 19, figure 1](../../assets/rf-development-guide/page-019-image-01.jpg)

---

<a id="page-20"></a>
## Source PDF page 20

There are three main modules inside: Zynq UltraScale+ MPSoC, usp_rf_data_converter_0, and up_axi modules.   

Module Name and Function:  
- Zynq UltraScale+ MPSoC: PS part, which includes the peripheral configuration of PS.
- usp_rf_data_converter_0: RF converter module, including initialization configuration for AD/DA.
- up_axi: Module for PS to read and write PL registers via the axi_lite bus.

The configuration of the Zynq UltraScale+ MPSoC IP core can refer to the IPI design section in the "RFEVM216 Development Board FPGA Basic Tutorial" to configure related parameters.  

RF Converter Configuration:  
usp_rf_data_converter_0 is the AD/DA hard IP configuration module of RFSoC, used to configure clock links, AD/DA modes, and MTS synchronization mode. Most of the parameters here can be further configured through Vitis/SDK.  

The configuration interface is as follows:  
RF-ADC Configuration:  
The default setting is mixer mode, RF real input, baseband IQ output. Other parameters such as frequency range

### Figures

![RFEVM216 Development Board RF Development Guide, page 20, figure 1](../../assets/rf-development-guide/page-020-image-01.jpg)

---

<a id="page-21"></a>
## Source PDF page 21

Decimation factor and other coefficients can all be configured a second time.   
RF-DAC Configuration  
The default setting is mixer mode, with baseband IQ input and RF real output. Other parameters, such as frequency range and decimation factor, can all be configured a second time.

### Figures

![RFEVM216 Development Board RF Development Guide, page 21, figure 1](../../assets/rf-development-guide/page-021-image-01.jpg)

![RFEVM216 Development Board RF Development Guide, page 21, figure 2](../../assets/rf-development-guide/page-021-image-02.jpg)

---

<a id="page-22"></a>
## Source PDF page 22

System Clocking Configuration  
The third-generation RFSoC supports multiple tiles sharing a reference clock, which makes the implementation of MTS multi-channel synchronization more convenient. This design uses this mode. Four transmit channels share the Bank230 reference clock, and four receive channels share the Bank225 reference clock. The ADC/DAC sampling rate is 2.4576 GHz, achieved by phase-locked multiplication of the 245.76 MHz reference clock output from the LMK04828 clock chip.  
Clock Out (MHz) is set to 153.6 MHz. The calculation and matching method for the axi_stream bus clock are as follows:  
- ADC/DAC sampling rate is 2.4576 GHz;
- DAC0 has tenfold interpolation. On the bus, 2 samples per clock cycle, so the bus clock is 2.4576 / 10 = 245.76 MHz (note that the ADC IQ bus is combined here, so one clock still corresponds to one sample);
- ADC has tenfold decimation, with 2 samples per bus clock (note that the ADC IQ bus is combined here, so one clock still corresponds to one sample), bus clock is 2.4576 / 10 = 245.76 MHz.
In the design, an MMCM is used to multiply the 153.6 MHz output from the ADC/DAC IP to 245.76 MHz to provide a synchronized clock for the baseband system.

### Figures

![RFEVM216 Development Board RF Development Guide, page 22, figure 1](../../assets/rf-development-guide/page-022-image-01.jpg)
