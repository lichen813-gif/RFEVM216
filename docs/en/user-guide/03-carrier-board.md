# 3. Carrier Board

[Switch to 中文](../../zh/user-guide/03-carrier-board.md)

## 3.1 Introduction

The carrier board provides:

- 1 M.2 interface
- 1 USB 3.0 interface
- 1 Gigabit Ethernet interface
- 1 JTAG and UART Type-C interface
- 1 Micro SD card slot
- 1 DisplayPort interface
- 2 QSFP28 optical interfaces
- 2 sets of PL expansion IO x8 and 1 set of PS expansion IO
- 4 user LEDs
- 1 FMC+ expansion interface

## 3.2 M.2 Interface

The RFEVM216 development board is equipped with a standard PCIe x2 M.2 interface for connecting M.2 SSDs. The M.2 interface uses an M-key slot, supports PCIe only, and does not support SATA. Users

![RFEVM216 user guide illustration](../../assets/user-guide/page-020-image-01.jpg)

When choosing an SSD, you need to choose a PCIe type SSD.
The PCIe signal is directly connected to the BANK505 PS MGT transceiver of the ZU47DR, with 2 TX signals and RX signals connected to the MGT's LANE0 and LANE1 in a differential signal manner. The PCIe clock is provided by a 100MHz differential clock. The M.2 circuit design schematic is shown below:
Figure 15 M.2 Interface Design Schematic
Table 8 M.2 Interface Zynq Pin Assignment
Signal Name Zynq Pin Number
M.2 Connector J19
Pin Number Name
MGT_TX0_N AH36 47 PETn0
MGT_TX0_P AH35 49 PETp0
MGT_TX1_N AG38 35 PETn1
MGT_TX1_P AG37 37 PETp1
MGT_RX0_N AJ42 41 PERn0
MGT_RX0_P AJ41 43 PERp0
MGT_RX1_N AH40 29 PERn1
MGT_RX1_P AH39 31 PERp1
MGT_CLK0_N AF35
MGT_CLK0_P AF34

![RFEVM216 user guide illustration](../../assets/user-guide/page-021-image-01.jpg)

## 3.3 USB 3.0 Interface

The RFEVM216 carrier board has one USB 3.0 interface, supporting both HOST and SLAVE operation modes, with a data transfer rate of up to 5.0 Gb/s. USB 3.0 connects directly to an external Type-A interface, while USB 2.0 connects via the ULPI interface to an external USB3320C chip, enabling high-speed USB 3.0 and USB 2.0 data communication.
The USB 3.0 connection diagram is as follows:
Figure 16 USB 3.0 Interface Diagram
Table 9 USB Interface Pin Assignment
Signal Name | Pin Name | Zynq Pin Number | Notes
USB_TX_N | BANK505_MGT_TX2_N | AF40 | USB 3.0 Data Transmit Negative
USB_TX_P | BANK505_MGT_TX2_P | AF39 | USB 3.0 Data Transmit Positive
USB_RX_N | BANK505_MGT_RX2_N | AG42 | USB 3.0 Data Receive Negative
USB_RX_P | BANK505_MGT_RX2_P | AG41 | USB 3.0 Data Receive Positive
USB_DATA0 | BANK502_PS_MIO56 | N29 | USB 2.0 Data Bit0
USB_DATA1 | BANK502_PS_MIO57 | R29 | USB 2.0 Data Bit1
USB_DATA2 | BANK502_PS_MIO54 | N28 | USB 2.0 Data Bit2
USB_DATA3 | BANK502_PS_MIO59 | T30 | USB 2.0 Data Bit3

![RFEVM216 user guide illustration](../../assets/user-guide/page-022-image-01.jpg)

USB_DATA4 BANK502_PS_MIO60 U28 USB2.0 Data Bit4
USB_DATA5 BANK502_PS_MIO61 T28 USB2.0 Data Bit5
USB_DATA6 BANK502_PS_MIO62 V28 USB2.0 Data Bit6
USB_DATA7 BANK502_PS_MIO63 T29 USB2.0 Data Bit7
USB_STP BANK502_PS_MIO58 R30 USB2.0 Stop Signal
USB_DIR BANK502_PS_MIO53 N30 USB2.0 Data Direction Signal
USB_CLK BANK502_PS_MIO52 P28 USB2.0 Clock Signal
USB_NXT BANK502_PS_MIO55 P29 USB2.0 Next Data Signal
USB_RESET_N BANK501_PS_MIO35 C33 USB2.0 Reset Signal

## 3.4 Gigabit Ethernet Interface

The RFEVM216 carrier board has one gigabit Ethernet interface connected to the PS end. The Ethernet chip uses TI's DP83867ISR chip to provide network communication services for the user. The Ethernet PHY chip on the PS end is connected to the Zynq PS BANK502 MIO. The DP83867 chip supports 10/100/1000 Mbps network transmission rates and communicates with the MAC layer of the Zynq system via the RGMII interface. The connection diagram of the gigabit Ethernet PHY chip is shown in the figure below:
Figure 17 Ethernet Connection Diagram
Table 10 DP83867ISR PHY Connected to XCZU49DR RFSoC

![RFEVM216 user guide illustration](../../assets/user-guide/page-023-image-01.jpg)

Signal Name Pin Name Pin Number
DP83867 PHY U48
Pin Number Pin Name
PHY_TX_CLK BANK502_PS_MIO64 U30 29 GTX_CLK
PHY_TXD0 BANK502_PS_MIO65 V30 28 TX_D0
PHY_TXD1 BANK502_PS_MIO66 V29 27 TX_D1
PHY_TXD2 BANK502_PS_MIO67 W28 26 TX_D2
PHY_TXD3 BANK502_PS_MIO68 Y29 25 TX_D3
PHY_TX_CTRL BANK502_PS_MIO69 W29 37 TX_CTRL
PHY_RX_CLK BANK502_PS_MIO70 AA28 32 RX_CLK
PHY_RXD0 BANK502_PS_MIO71 AB28 33 RX_D0
PHY_RXD1 BANK502_PS_MIO72 AC28 34 RX_D1
PHY_RXD2 BANK502_PS_MIO73 AA29 35 RX_D2
PHY_RXD3 BANK502_PS_MIO74 Y30 36 RX_D3
PHY_RX_CTRL BANK502_PS_MIO75 AC29 38 RX_CTRL
PHY_MDC BANK502_PS_MIO76 AB30 16 MDC
PHY_MDIO BANK502_PS_MIO77 AA30 17 MDIO
PS_POR_B BANK501_PS_MIO26 A34 43 RESET_N

## 3.5 Micro SD Card Slot

The RFEVM216 carrier board includes a Micro SD card interface to provide users access to SD card storage,
used for storing the BOOT program, Linux operating system kernel, file system, and other user data files.
The SD card IO signals are connected to the MIO signals of PS BANK501, and the connection diagram between PS and the SD card connector is as shown below:
Figure 18 SD Card Connection Diagram
Table 11 SD Card Pin Assignment
Signal Name	Pin Name	Pin Number	Remark
SDIO_CLK	BANK501_PS_MIO51	M31	SD Clock Signal
SDIO_CMD	BANK501_PS_MIO50	M30	SD Command Signal
SDIO_DAT0	BANK501_PS_MIO46	J31	SD Data Bit0
SDIO_DAT1	BANK501_PS_MIO47	L32	SD Data Bit1
SDIO_DAT2	BANK501_PS_MIO48	M32	SD Data Bit2
SDIO_DAT3	BANK501_PS_MIO49	K31	SD Data Bit3
SDIO_DETECT	BANK501_PS_MIO45	L30	SD Card Detect Signal

## 3.6 DP Display Interface

The RFEVM216 carrier board has one mini DisplayPort output display interface for displaying video images. The interface supports the VESA DisplayPort V1.2a output standard.
The DisplayPort data transmission channels are directly driven out by the BANK505 PS MGT of the RFEVM216. The LANE3 signals of the MGT are connected to the DP connector using differential signals. The DisplayPort auxiliary channel is connected to the PS MIO pins. The schematic diagram of the DP output interface design is as follows.

![RFEVM216 user guide illustration](../../assets/user-guide/page-025-image-01.jpg)

Table 12 DisplayPort and Zynq Pin Assignment
Signal Name  Pin Name  Pin Number  Remarks
GT0_DP_TX_P  PS_MGT_TX3_P  AE37  DP Data Transmit Positive
GT0_DP_TX_N  PS_MGT_TX3_N  AE38  DP Data Transmit Negative
PS_MGT_DP_CLK_P  PS_MGT_CLK3_P  AB34  DP Reference Clock Positive
PS_MGT_DP_CLK_N  PS_MGT_CLK3_N  AB35  DP Reference Clock Negative
DP_AUX_OUT  BANK501_PS_MIO27  B34  DP Auxiliary Data Output
DP_AUX_IN  BANK501_PS_MIO30  C34  DP Auxiliary Data Input
DP_OE  BANK501_PS_MIO29  B33  DP Auxiliary Data Output Enable
DP_HPD  BANK501_PS_MIO28  A33  DP Hot-Plug Detection Signal

## 3.7 Optical Fiber Interface

The RFEVM216 carrier board has 2 QSFP28 fiber-optic interfaces. These 2 fiber-optic interfaces are connected to the GTY transceivers on BANK130 and BANK131 of Zynq. The two reference clocks for BANK130 are provided by the LMK04828 chip (configurable) on the RFSOM216 SoM board and the differential crystal oscillator on the carrier board (156.25MHz). The reference clock for BANK131 is provided by the differential crystal oscillator on the carrier board (156.25MHz).
The connection diagram of the QSFP28 interface is shown below:

![RFEVM216 user guide illustration](../../assets/user-guide/page-026-image-01.jpg)

Figure 19 Optical Fiber Design Diagram
Table 13 J12 QSFP Interface Pin Assignment
Signal Name Zynq Pin Name Zynq Pin Number Remarks
QSFP_RX0_N MGTYRXN0_130 L42
QSFP_RX0_P MGTYRXP0_130 L41
QSFP_RX1_N MGTYRXN1_130 J42
QSFP_RX1_P MGTYRXP1_130 J41
QSFP_RX2_N MGTYRXN2_130 G42
QSFP_RX2_P MGTYRXP2_130 G41
QSFP_RX3_N MGTYRXN3_130 F40
QSFP_RX3_P MGTYRXP3_130 F39

![RFEVM216 user guide illustration](../../assets/user-guide/page-027-image-01.jpg)

QSFP_TX0_N MGTYTXN0_130 K39
QSFP_TX0_P MGTYTXP0_130 K38
QSFP_TX1_N MGTYTXN1_130 J37
QSFP_TX1_P MGTYTXP1_130 J36
QSFP_TX2_N MGTYTXN2_130 H39
QSFP_TX2_P MGTYTXP2_130 H38
QSFP_TX3_N MGTYTXN3_130 G37
QSFP_TX3_P MGTYTXP3_130 G36
Table 14 J14 QSFP Interface Pin Assignment
Signal Name Zynq Pin Name Zynq Pin Number Remarks
QSFP_RX0_N MGTYRXN0_131 E42
QSFP_RX0_P MGTYRXP0_131 E41
QSFP_RX1_N MGTYRXN1_131 D40
QSFP_RX1_P MGTYRXP1_131 D39
QSFP_RX2_N MGTYRXN2_131 C42
QSFP_RX2_P MGTYRXP2_131 C41
QSFP_RX3_N MGTYRXN3_131 B40
QSFP_RX3_P MGTYRXP3_131 B39
QSFP_TX0_N MGTYTXN0_131 F35
QSFP_TX0_P MGTYTXP0_131 F34
QSFP_TX1_N MGTYTXN1_131 E37
QSFP_TX1_P MGTYTXP1_131 E36
QSFP_TX2_N MGTYTXN2_131 C37
QSFP_TX2_P MGTYTXP2_131 C36
QSFP_TX3_N MGTYTXN3_131 A37
QSFP_TX3_P MGTYTXP3_131 A36
Table 15 Reference Clock Distribution
Zynq Pin Name  Zynq Pin Number  Notes
MGTREFCLK0N_130  P35  SDCLKOUT5 output of LMK04828
MGTREFCLK0P_130  P34  SDCLKOUT5 output of LMK04828
MGTREFCLK1N_130  M35  Differential output of 156.25MHz oscillator on carrier board
MGTREFCLK1P_130  M34  Differential output of 156.25MHz oscillator on carrier board
MGTREFCLK1N_131  H35  Differential output of 156.25MHz oscillator on carrier board
MGTREFCLK1P_131  H34  Differential output of 156.25MHz oscillator on carrier board
Table 16 J12 Optical Fiber Low-Speed IO Signal Handling
QSFP Low-Speed IO Signal Name  Notes  SFP Low-Speed IO Signal Name  Notes
SCL  Pull-up 3.3V  TX_FULT  Pull-up 3.3V
SDA  Pull-up 3.3V  TX_DISABLE  Grounded
ModSeIL  Pull-up 3.3V  RATE_SELECT0  Pull-up 3.3V
ResetL  Pull-up 3.3V  RATE_SELECT1  Pull-up 3.3V
ModPrsl  Pull-up 3.3V  LOS  Pull-up 3.3V
intL  Pull-up 3.3V  -  -
LPMode  Grounded  -  -
Table 17 J14 Optical Fiber Low-Speed IO Signal Handling
QSFP Low-Speed IO Signal Name  Notes  SFP Low-Speed IO Signal Name  Notes
SCL  Pull-up 3.3V  TX_FULT  Pull-up 3.3V
SDA  Pull-up 3.3V  TX_DISABLE  Grounded
ModSeIL  Pull-up 3.3V  RATE_SELECT0  Pull-up 3.3V
ResetL  Pull-up 3.3V  RATE_SELECT1  Pull-up 3.3V
ModPrsl  Pull-up 3.3V  LOS  Pull-up 3.3V
intL  Pull-up 3.3V
LPMode Grounding

## 3.8 JTAG & UART Interface

The RFEVM216 carrier board reserves a JTAG & UART interface, used for downloading and debugging FPGA programs or burning programs into flash. Here, we use FTDI's 5th generation USB device chip FT2232H, which is a USB 2.0 high-speed to UART/FIFO chip, with two multi-protocol synchronous serial engines allowing the use of JTAG. It has the ability to configure in various industrial standard serial or parallel interfaces. The JTAG & UART connection schematic is shown in the figure below:
Figure 20 JTAG & UART Connector Connection Schematic

## 3.9 GPS Module

The RFEVM216 carrier board can be equipped with the GPS module NEO-M8N, which is a high-performance GNSS receiver module with excellent positioning accuracy and sensitivity. This module uses the latest u-blox M8 chip, supporting multiple satellite systems such as GPS, GLONASS, BeiDou, and Galileo, providing global positioning data. The GPS connection schematic is shown in the figure below:
Signal Name	Pin Name	Pin Number	Remarks
UART0_TX	BANK501_PS_MIO39	J32	PS Uart Data Output
UART0_RX	BANK501_PS_MIO38	G32	PS Uart Data Input

![RFEVM216 user guide illustration](../../assets/user-guide/page-030-image-01.jpg)

Figure 21 GPS Module Connection Diagram
Table 18 GPS Module Pin Assignment
Signal Name | Pin Name | Pin Number | Remarks
PPS_1S_GPS | IO_L4N_AD12N_88 | L17 | TIMEPULSE
TXD_GPS | BANK501_PS_MIO40 | F32 | TXD_MISO
RXD_GPS | BANK501_PS_MIO41 | K32 | RXD_MOSI

## 3.10 FMC+ Interface

The RFEVM216 has an FMC+ expansion port, which can connect externally to XILINX or other FMC/FMC+ modules. The FMC+ expansion port includes 69 pairs of differential IO signals and 8 sets of GTY transceiver signals.
The 69 pairs of differential signals on the FMC+ expansion port are connected to the IOs of BANK64, 65, 66 of the Zynq chip, with a voltage standard of 1.8V, and the differential signals support LVDS data communication. The 8 sets of GTY transceiver signals are connected to BANK128 and BANK129.

## 3.11 Board-to-Board High-Speed Connector

The RFEVM216 has 2 board-end rectangular connectors, surface-mounted 80PIN, 0.8mm pitch, with a height of 5mm.

![RFEVM216 user guide illustration](../../assets/user-guide/page-031-image-01.jpg)

Table 19 J3 Connector Pin Assignment
Signal Name J3 Sequence Pin Name Pin Number Remark
HD_IO_C_P4 3 IO_L2P_AD10P_89 J12
HD_IO_C_N4 5 IO_L2N_AD10N_89 J11
HD_IO_C_P5 9 IO_L11P_AD1P_89 C10
HD_IO_C_N5 11 IO_L11N_AD1N_89 B10

![RFEVM216 user guide illustration](../../assets/user-guide/page-032-image-01.jpg)

![RFEVM216 user guide illustration](../../assets/user-guide/page-032-image-02.jpg)

HD_IO_C_P6 15 IO_L12P_AD0P_89 A10
HD_IO_C_N6 17 IO_L12N_AD0N_89 A9
HD_IO_C_P7 21 IO_L7P_HDGC_AD5P_89 E10
HD_IO_C_N7 23 IO_L7N_HDGC_AD5N_89 E9
HD_IO_C_P8 27 IO_L12P_AD0P_89 H11
HD_IO_C_N8 29 IO_L12N_AD0N_89 G10
HD_IO_C_P9 33 IO_L3P_AD9P_89 H10
HD_IO_C_N9 35 IO_L3N_AD9N_89 H9
HD_IO_C_P10 39 IO_L9P_AD3P_89 D9
HD_IO_C_N10 41 IO_L9N_AD3N_89 C9
HD_IO_C_P11 45 IO_L5P_HDGC_AD7P_89 G12
HD_IO_C_N11 47 IO_L5N_HDGC_AD7N_89 G11
Table 20 J6 Connector Pin Assignment
Signal Name J6 Sequence Pin Name Pin Number Remarks
HD_IO_B_P0 3 IO_L6P_HDGC_87 F15
HD_IO_B_N0 5 IO_L6N_HDGC_87 E14
HD_IO_B_P1 9 IO_L7P_HDGC_87 C15
HD_IO_B_N1 11 IO_L7N_HDGC_87 C14
HD_IO_B_P2 15 IO_L8P_HDGC_87 B16
HD_IO_B_N2 17 IO_L8N_HDGC_87 B15
HD_IO_B_P3 21 IO_L11P_AD9P_87 A15
HD_IO_B_N3 23 IO_L11N_AD9N_87 A14
HD_IO_B_P4 27 IO_L10P_AD10P_87 D16
HD_IO_B_N4 29 IO_L10N_AD10N_87 C16
HD_IO_B_P5 33 IO_L3P_AD13P_87 D14
HD_IO_B_N5 35 IO_L3N_AD13N_87 C13
HD_IO_B_P6 39 IO_L5P_HDGC_87 A13
HD_IO_B_N6 41 IO_L5N_HDGC_87 A12
HD_IO_B_P7 45 IO_L9P_AD11P_87 E16
HD_IO_B_N7 47 IO_L9N_AD11N_87 E15
HD_IO_B_P8 4 IO_L1P_AD15P_87 F12
HD_IO_B_N8 6 IO_L1N_AD15N_87 E12
HD_IO_B_P9 10 IO_L12P_AD8P_87 F14
HD_IO_B_N9 12 IO_L12N_AD8N_87 F13
HD_IO_B_P10 16 IO_L2P_AD14P_87 D13
HD_IO_B_N10 18 IO_L2N_AD14N_87 D12
HD_IO_B_P11 22 IO_L4P_AD12P_87 B13
HD_IO_B_N11 24 IO_L4N_AD12N_87 B12
HD_IO_C_P0 28 IO_L8P_HDGC_AD4P_89 E11
HD_IO_C_N0 30 IO_L8N_HDGC_AD4N_89 D11
HD_IO_C_P1 34 IO_L6P_HDGC_AD6P_89 F10
HD_IO_C_N1 36 IO_L6N_HDGC_AD6N_89 F9
HD_IO_C_P2 40 IO_L10P_AD2P_89 C11
HD_IO_C_N2 42 IO_L10N_AD2N_89 B11
HD_IO_C_P3 46 IO_L1P_AD11P_89 K12
HD_IO_C_N3 48 IO_L1N_AD11N_89 K11

## 3.12 Expansion IO and LED Lights

The RFEVM216 carrier board expands 2 groups of PL-side IOs (x7, x8) and one group of PS-side IOs (x8).
Figure 22 Extended IO Circuit Connection Diagram
Table 21 J9 Extended IO Pin Assignment
Signal Name	Pin Name	Pin Number	Remarks
HD_IO_A_P2	IO_L9P_AD11P_88	J14
HD_IO_A_N2	IO_L9N_AD11N_88	J13
HD_IO_A_P3	IO_L6P_HDGC_88	K15
HD_IO_A_N3	IO_L6N_HDGC_88	K14
HD_IO_A_P4	IO_L10P_AD10P_88	H13
HD_IO_A_N4	IO_L10N_AD10N_88	G13

![RFEVM216 user guide illustration](../../assets/user-guide/page-035-image-01.jpg)

HD_IO_A_P5 IO_L7P_HDGC_88 K17 Table 22 J10 Extended IO Pin Assignment Signal Name Pin Name Pin Number Remarks HD_IO_A_P6 IO_L5P_HDGC_88 L15 HD_IO_A_N6 IO_L5N_HDGC_88 L14 HD_IO_A_P7 IO_L3P_AD13P_88 N14 HD_IO_A_N7 IO_L3N_AD13N_88 M14 HD_IO_A_P8 IO_L2P_AD14P_88 N15 HD_IO_A_N8 IO_L2N_AD14N_88 M15 HD_IO_A_P9 IO_L1P_AD15P_88 N16 HD_IO_A_N9 IO_L1N_AD15N_88 M16 Table 23 J11 Extended IO Pin Assignment Signal Name Pin Name Pin Number Remarks BANK501_PS_MIO36 PS_MIO36 E31 BANK501_PS_MIO37 PS_MIO37 E32 BANK501_PS_MIO33 PS_MIO33 D32 BANK501_PS_MIO44 PS_MIO44 K30 BANK501_PS_MIO31 PS_MIO31 D33 BANK501_PS_MIO32 PS_MIO32 D34 BANK501_PS_MIO42 PS_MIO42 H31 BANK501_PS_MIO43 PS_MIO43 G31 On the RFEVM216 card, 4 user-defined LEDs can be expanded, and 4 extended IOs are routed to the 2PIN TJC3 straight pin header.
Figure 23 LED Light Expandable IO Circuit Diagram
Table 24 LED Light Expandable IO Pin Assignment
Signal Name | Pin Name | Pin Number | Remark
LEDG0 | IO_L12P_AD8P_88 | G16
LEDG1 | IO_L12N_AD8N_88 | G15
LEDG2 | IO_L8P_HDGC_88 | J16
LEDG3 | IO_L8N_HDGC_88 | H16

## 3.13 Boot Mode Configuration

The RFEVM216 development board has two 2-bit DIP switches, SWC1 and SWC2, to configure the Zynq system's boot mode. The RFEVM216 development platform supports 4 boot modes: JTAG debugging mode, QSPI flash, EMMC, and SD card boot mode. After power-on, the RFSoC chip detects the levels of (PS_MODE0~3) to determine which boot mode to use. Users can also select different boot modes via DIP switch SWC1.

![RFEVM216 user guide illustration](../../assets/user-guide/page-037-image-01.jpg)

Figure 24 PS_MODE Circuit Diagram
The start mode configuration for SWC1 and SWC2 is shown in the table below.

![RFEVM216 user guide illustration](../../assets/user-guide/page-038-image-01.jpg)

![RFEVM216 user guide illustration](../../assets/user-guide/page-038-image-02.jpg)

Table 25 Startup Mode Configuration
DIP Switch SWC1 Position
(1,2)
DIP Switch SWC2 Position
(1,2)
MODE[3:0] Startup Mode
ON, ON ON, ON 0000 JTAG
ON, ON OFF, ON 0010 QSPI
ON, OFF OFF, ON 0110 EMMC
OFF, OFF OFF, ON 1110 SD

## 3.14 RF Radio Frequency Link

The RFEVM216 supports 16 channels of 14-bit ADC with 2.5GSPS input and 16 channels of 14-bit DAC with 9.85GSPS output. Single-ended signal input and output are converted between differential and single-ended through a balun device, completing data transmission and reception.
The ADC analog front end, after passing through a limiting diode, is converted from single-ended to differential through a balun. The differential signal is directly connected to the RF-ADC pins on the SoM board. The diagram is shown below.
For the DAC link, the differential signal of RF-DAC on the SoM board is converted from differential to single-ended through a balun. The single-ended signal is connected to the MCX RF terminal through the DC module. The diagram is shown below.

![RFEVM216 user guide illustration](../../assets/user-guide/page-039-image-01.jpg)

![RFEVM216 user guide illustration](../../assets/user-guide/page-039-image-02.jpg)

## 3.15 MMCX Interface

The RFEVM216 development board supports external reference clock input/output, trigger signal input/output, etc. The actual picture is shown below.

## 3.16 Fan

The RFEVM216 generates a large amount of heat during normal operation. We have added a heat dissipation structure and a fan to the SoM board to prevent the chip from overheating. The fan speed is controlled by the PL side of the Zynq chip, and the control pin is connected to the IO on BANK88.
Signal Name | Position | Pin Number | Remarks
CLKIN2 | J27 | LMK04828 | Reference Clock Input
CLKOUT | J24 | LMK04828 | Clock Output
TRIG_IN | JA33 | H15 | Trigger Signal Input
TRIG_OUT | JA34 | H14 | Trigger Signal Output
ADC_CLK | J25 | ADC_CLK_225 |
DAC_CLK | J26 | DAC_CLK_229 |
CLK_IN0 | J23 | LMK04828 | Reference Clock Input
SYSREF_IN_P | J21 | LMK04828 | Reference Clock Input
SYSREF_IN_N | J22 | LMK04828 | Reference Clock Input

![RFEVM216 user guide illustration](../../assets/user-guide/page-040-image-01.jpg)

Signal Name Pin Name Pin Number Remarks
HD_IO_A_N5 IO_L7N_HDGC_88 K16

## 3.17 Power Supply

The power input voltage of the RFEVM216 development board is DC12V, and on the carrier board, multiple power supply chips generate +5V, +1.8V, +3.3V power supply.
The power supply design block diagram is shown in the figure below:
Figure 25 RFEVM216 Carrier Board Power Interface Section

## 3.18 Structural Dimension Diagram

![RFEVM216 user guide illustration](../../assets/user-guide/page-041-image-01.jpg)

![RFEVM216 user guide illustration](../../assets/user-guide/page-041-image-02.jpg)

Figure 26 Front view of RFEVM216

![RFEVM216 user guide illustration](../../assets/user-guide/page-042-image-01.jpg)
