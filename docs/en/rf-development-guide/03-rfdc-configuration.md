# 2.2 RF Data Converter Configuration

[Switch to 中文](../../zh/rf-development-guide/03-rfdc-configuration.md)

> This chapter is translated from the Chinese source PDF. Figures and UI screenshots retain their original labels so that they match the hardware and software.  
> Source PDF: `RFEVM216开发板射频开发指南s.pdf`  
> Source pages: 7-17

<a id="page-7"></a>
## Source PDF page 7

All Tiles have dedicated clock input pins, but only the clock pins of three ADC Tiles (Bank 224/226/227) and three DAC Tiles (Bank 228/230/231) are directly connected to the LMK04828 clock chip. The clock pins of BANK225 and BANK229 are routed to the MCX interface on the baseboard, which can be provided externally. The detailed connection relationships are shown in the following table:  

ADC/DAC Tile Signal Name Clock Output Source LMK04828  
ADC Tile 224 ADC_REFCLK_N2/P2_R SDCLKOUT9  
ADC Tile 225 RF_ADC_CLK_N/P  
ADC Tile 226 ADC_REFCLK_N1/P1_R DCLKOUT0  
ADC Tile 227 ADC_REFCLK_N3/P3_R SDCLKOUT13  
DAC Tile 228 DAC_REFCLK_N1/P1_R DCLKOUT6  
DAC Tile 229 RF_DAC_CLK_N/P  
DAC Tile 230 DAC_REFCLK_N0/P0_R DCLKOUT10  
DAC Tile 231 DAC_REFCLK_N3/P3_R DCLKOUT8  

2.2 RF Data Converter Configuration Guide  

The RFSoC RF data converter IP core provides a configurable wrapper that allows the RF-ADC and RF-DAC blocks to be used for IP integrator designs.  

For specific details, please refer to the official documentation:  
https://docs.xilinx.com/r/en-US/pg269-rf-data-converter  

Here, taking the RFEVM216 (xczu49dr) development platform as an example, the relevant configuration of the IP is introduced.  

Basic IP Configuration

---

<a id="page-8"></a>
## Source PDF page 8

Basic Page  
Presets  
The Vivado IDE IP core configuration interface provides a way to save and apply preset configurations. From the preset menu, several fixed configurations are available.  
ADC: R2C Multi x2 DAC: C2R Multi x2 (Beta): The RF-ADC is configured to use real-to-imaginary data in x2 multi-band mode, and the RF-DAC is configured to use imaginary-to-real data in x2 multi-band mode.  
DAC: C2C Multi 2x2 (Beta): Uses imaginary-to-imaginary data in 2x2 multi-band mode on a single RF-DAC block.  
DAC: C2R Multi 2x2 (Beta): Uses imaginary-to-real data in 2x2 multi-band mode on a single RF-DAC block.  
DAC: C2R Multi x4 (Beta): Uses imaginary-to-real data in 1x4 multi-band mode on a single RF-DAC block.  
Converter Setup  
The converter setup menu provides Advanced and Simple options for setting up IP configuration.

### Figures

![RFEVM216 Development Board RF Development Guide, page 8, figure 1](../../assets/rf-development-guide/page-008-image-01.jpg)

---

<a id="page-9"></a>
## Source PDF page 9

Advanced: All chips are configured independently.  
Simple: Users can see configuration options for individual RF-ADC and RF-DAC blocks. After setting up the chip configuration information, the RF-ADC configuration can be applied to any RF-ADC on the device by selecting a chip from the given chip list. Similarly, the RF-DAC configuration can be applied to any RF-DAC chip. It is possible to switch from Simple to Advanced settings without losing configuration information. However, switching from Advanced to Simple is not possible. Only downward compatibility is supported.  
RF-ADC Chip Settings  
These parameters are common to every RF-ADC in the chip.  
Link Coupling: This determines whether the input signal of the RF-ADC is AC-coupled or DC-coupled. Typical applications use AC coupling, but DC coupling is also supported for certain applications (such as Zero IF). When DC coupling mode is selected, the common-mode voltage of the external driving circuit needs to be aligned with the internal common-mode voltage of the RF-ADC using the externally driven VCM pin. The VCM pin can only be used for DC.

### Figures

![RFEVM216 Development Board RF Development Guide, page 9, figure 1](../../assets/rf-development-guide/page-009-image-01.jpg)

---

<a id="page-10"></a>
## Source PDF page 10

Coupling mode: If AC coupling mode is selected, it can maintain floating. (Currently, RFEVM216 motherboard is designed for AC coupling mode)  
Converter Band Mode: Each RF-ADC can operate independently (single-band mode) or work with other converters (multi-band mode). The following modes are available for RF-ADC.  
Enable ADC: Choose whether to enable the selected converter on the selected chip.  
Invert Q Output: This can only be set when I/Q output data is selected and the fine-tune mixer is enabled. When set, the mixer's product output is negative. This allows generation of -Q data.  
Dither: Choose whether dithering is enabled for the selected chip. Dithering should be enabled unless the sampling rate is below 0.75 times the maximum sampling rate of the RF-ADC.  
Enable TDD Real Time Ports (Gen 3): Enable TDD real-time ports. Once enabled, the tdd_mode port will be added to the IP. This can achieve power saving by disabling part of the RF-ADC.  
Digital Output Data: Set the data type of the selected converter on the chip. This parameter is only configurable when the converter is enabled. Valid values are Real/IQ. When converter 0 is set to I/Q, converter 1 must also be enabled. When converter 2 is set to I/Q, converter 3 must also be enabled, otherwise the configuration is invalid.  
Decimation Mode: Set the decimation value for the selected converter on the chip. This parameter is only configurable when the converter is enabled. Values 1x, 2x, 3x, 4x, 5x, 6x, 8x, 10x, 12x, 16x, 20x, 24x, 40x can be selected from the drop-down menu. When the converter is not enabled, this value is off.  
Samples per AXI4-Stream Word: Set the number of samples per cycle. This parameter is configurable when a specific converter is enabled. Valid values range from 1 to 12 and can be selected from the drop-down list. The range depends on the selected sampling rate, to  

AXI4-Stream clock remains within the specification range. The required AXI4-Stream clock is the input of the IP core and displays values based on the selected bus width.   
Observation Channel: Enable and set the observation channel.   
Mixer Type: Set the type of mixer to use (coarse, fine). The available options depend on the selection of the digital output data field of the converter.   
Mixer Mode: Set the mixer mode of the selected converter. This parameter is only available when enabled

---

<a id="page-11"></a>
## Source PDF page 11

The converter can be configured. The selection of the mixer mode depends on the type of mixer and the format of the selected digital output data. When real data output is selected, the mixer is bypassed. When I/Q data output is selected, the mixer can be set to read I/Q or I/Q to I/Q.  

Coarse Mixer Frequency: Sets the frequency of the coarse mixer. This parameter is configurable when the mixer type is set to coarse. Valid options are Fs/2, Fs/4, and -Fs/4.  

Fine Mixer Frequency: Sets the frequency of the fine mixer. This parameter is valid only when the mixer type is set to fine. The valid frequency range is -10GHz to 10GHz.  

Fine Mixer Phase: Sets the phase of the fine mixer. This parameter is valid only when the mixer type is set to fine. The valid range is -180 to 180.  

Nyquist Zone: Selects operation in even or odd Nyquist zones.  

Calibration Mode: Choose a different calibration optimization scheme based on the characteristics of the input signal. Auto mode (third generation) is suitable for all input frequencies. Mode 1 is the optimal input frequency Fsamp/2 (Nyquist) ±10%. Mode 2 is the optimal range for input frequency output.

---

<a id="page-12"></a>
## Source PDF page 12

RF-DAC Tile Configuration  
These parameters apply to every RF-DAC in a tile.  
Multi Tile Sync: When enabled, the block is included in a multi-tile sync group. RF-DAC Tile0 must be enabled and appear in the group together with Converter 0 of the tile configured to enable this option.  
Variable Output Current (Gen3): When variable output current mode is enabled, the output current is set according to the specifications in DC and AC Switching. DAC_AVTT must be set to 3.0V.  
Link Coupling: This determines whether the RF-DAC output signal is AC-coupled or DC-coupled. In DC-coupling mode, the common-mode voltage is fixed. In this mode, the VOP range is reduced.  
RF-DAC Converter Configuration

### Figures

![RFEVM216 Development Board RF Development Guide, page 12, figure 1](../../assets/rf-development-guide/page-012-image-01.jpg)

---

<a id="page-13"></a>
## Source PDF page 13

Common  
Enable DAC: Choose whether to enable the selected converter in the selected chip. Values can be TRUE or FALSE.  
Invert Q Output: When enabled, the Q output of the converter is inverted. This can only be set when “I/Q output data” is checked. The subsequent analog mixer must implement subtraction: 1 x cos(f) - Q x sin(f), so a -Q signal (negative quadrature) option is provided so that the external mixer can perform addition, I x cos(f) + (-Q)sin(f).  
Inverse Sinc Filter: Choose whether to enable the Sinc inverse filter. This parameter can only be configured when the converter is enabled. Values can be TRUE or FALSE. This applies to both Nyquist regions, based on Analog Settings → Nyquist Region selection.  
Enable TDD Real Time Ports (Gen3): When enabled, the tdd_mode port will be added to the IP. This function can be realized by shutting down parts of the RF-DAC.  
Digital Output Data: Set the data type of the selected converter in the selected chip. This parameter can only be configured when the converter is enabled. Valid values are Real and I/Q. When converter 0 is set to I/Q, converter 1 must also be enabled; when converter 2 is set to I/Q, converter 3 must also be enabled, otherwise the configuration is invalid.  
Decimation Mode: Set the decimation value for the selected converter in the selected chip. This parameter can only be configured when the converter is enabled. Select values from the drop-down menu: 1x, 2x, 3x, 4x, 5x, 6x, 8x, 10x, 12x, 16x, 20x, 24x, 40x. When the converter is not enabled, this value is off.  
Samples per AXI4-Stream Word: Set the number of samples per word. When a specific converter is enabled, this parameter is configurable. Valid values range from 1 to 12 and can be selected from the drop-down list. The range depends on the chosen sampling rate to  

Keep the AXI4-Stream clock within the specification range. The required AXI4-Stream clock is an input to the IP core and shows values based on the selected bus width.   
Datapath Mode (Gen3) data path mode: Select the RF-DAC data path mode. The following options are available. These modes apply to the digital data path, and you can use Analog Settings → Nyquist Region to select output of the data from either the first or second Nyquist region.   
DUC 0 to Fs/2: Full Nyquist DUC mode.

---

<a id="page-14"></a>
## Source PDF page 14

DUC 0 to Fs/4: Half-Nyquist DUC mode using a low-pass IMR filter.   
DUC Fs/4 to Fs/2: Half-Nyquist DUC mode using a high-pass IMR filter.   
No DUC 0 to Fs/2: DU bypass mode.   
Mixer Settings   
Mixer Type: Set the type of mixer to use. Valid options are bypassed, coarse, and fine. Available options depend on the selection of the converter's digital output data field.   
Mixer Mode: Set the mixer mode of the selected converter. This parameter can only be configured when the converter is enabled. The choice of mixer mode depends on the mixer type and the format of the selected digital output data. When real data output is selected, the mixer is bypassed. When I/Q data output is selected, the mixer can be set to real I/Q or I/Q to I/Q.   
Coarse Mixer Frequency: Set the frequency of the coarse mixer. This parameter is configurable when the mixer type is set to coarse. Valid options are Fs/2, Fs/4, and -Fs/4.   
Fine Mixer Frequency: Set the frequency of the fine mixer. This parameter is only valid when the mixer type is set to fine. Valid range: -10 GHz to 10 GHz.   
Fine Mixer Phase: Set the phase of the fine mixer. This parameter is only valid when the mixer type is set to fine. Valid range: -180 to 180.   
Analog Settings   
Nyquist Zone: Select operation in even or odd Nyquist zones.   
Decode Mode: The RF-DAC decoder can be optimized for low signal-to-noise ratio or high linearity.

---

<a id="page-15"></a>
## Source PDF page 15

System Clock Configuration  
AXI4-Lite Interface Configuration  
AXI Clock Frequency (MHz): The core requires information on the AXI4-Lite clock input frequency to ensure the correct timing of the power-up sequence of the RF-ADC and RF-DAC blocks. The clock speed should be entered in megahertz.  
Chip Clock Settings  
The sampling rate and clock frequency are set in this section. These settings are shared by each converter on the chip.  
Sampling Rate (GSPS): Sets the sampling rate for each chip. It is configurable when at least one converter on the chip is enabled. The valid values depend on the selected device and package.  
Max Fs (GSPS): Provides the maximum sampling rate for each chip as a reference.  
PLL: Choose whether to use or bypass the PLL on the chip. It is configurable when at least one converter on the chip is enabled. To dynamically reconfigure the PLL using the RF DC driver API, the PLL must be enabled in the Vivado IDE. Valid values are True or False.  
Reference Clock (MHz): Sets the clock input frequency for the chip. It is configurable when the PLL and at least one converter on the tile are enabled. Its value depends on the sampling rate of the tile. A drop-down list provides a value based on the selected sampling rate. To achieve the best phase noise performance, it is recommended to use the correct reference frequency at the PLL input.

### Figures

![RFEVM216 Development Board RF Development Guide, page 15, figure 1](../../assets/rf-development-guide/page-015-image-01.jpg)

---

<a id="page-16"></a>
## Source PDF page 16

PLL Reference Clock: Sets the PLL input clock frequency, if the PLL is enabled for a specific tile.  
Reference Clock Divider: The reference clock divider, sets the divider on the phase-locked loop reference clock input.  
Fabric Clock (MHz): This is the clock frequency provided on the AXI4-Stream clock input of the selected chip. The required frequency is determined by the sampling rate and the configuration of the converter. Since all AXI4-Stream ports on a chip share a common AXI4-Stream clock, all converter configurations on the chip must require the same clock frequency.  
Clock Out (MHz): Sets the frequency of the on-chip output clock. This clock can be used to drive AXI4-Stream clock inputs. It is configurable when at least one converter in the tile is enabled. These values depend on the tile's sampling rate. A dropdown list provides values based on the selected sampling rate.  
Clock Source (3rd Generation): Sets the clock source for each chip. For third-generation devices with only dual RF-DACs, the clock source for each enabled RF-DAC must be set to an even block.  
Distribute Clock (3rd Generation): Sets whether the chip will distribute the clock to other chips on the device. Off: Does not distribute the clock.  
Input Refclk: When the PLL is enabled, the input reference clock is forwarded from the tile. If the PLL is not enabled, the input sampling clock is distributed.  
PLL Output: When the PLL is enabled, the clock output from the PLL is forwarded from the tile.  
PLL Summary Settings  
The PLL summary provides information about the frequency and divider settings of enabled PLLs.  
Vco (MHz): The frequency of the voltage-controlled oscillator.  
Fb Div: Feedback divider setting.  
M: Output divider setting.  
R: Reference clock divider setting.

---

<a id="page-17"></a>
## Source PDF page 17

Advanced Configuration  
RF Analyzer: The RF analyzer provides a hardware test system. The system includes data stimulus and capture blocks configured for this IP core instance.  
PL Clock Frequency (MHz): If multiple devices are synchronized, the PLL clock must be provided and the PL SYSREF sent to the system. To accurately capture SYSREF, the frequency must be an integer multiple common to both RF-ADC and RF-DAC AXI4-Stream clocks.  
RF-ADC  
Enable Real Time Ports: Enables RF-ADC Over Threshold, Over Voltage, Over Range, and pl_event ports.  
Enable Cal Freeze Ports: Enables calibration freeze logic. Calibration is frozen when analog input overvoltage or the related int_cal_freeze input is asserted.  
Auto Cal Freeze: Automatic calibration freeze. If this option is selected, calibration will be frozen when the analog input is out of range in addition to the manual calibration freeze process.  
Enable Real Time NCO Ports: Enables real-time NCO ports. The frequency and phase of the mixer NCO in the DDC can be modified in real time. Selecting this option enables the real-time NCO interface for the RF-ADC.  
Enable Real Time Digital Step Attenuation Ports (Gen3): Enables real-time digital step attenuation ports (third generation). If this option is selected, the digital attenuation can be changed via the real-time DSA signal interface.

### Figures

![RFEVM216 Development Board RF Development Guide, page 17, figure 1](../../assets/rf-development-guide/page-017-image-01.jpg)
