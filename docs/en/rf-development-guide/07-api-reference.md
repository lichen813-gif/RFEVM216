# Appendix A: API Reference

[Switch to 中文](../../zh/rf-development-guide/07-api-reference.md)

Appendix A - API Introduction
For detailed API information, please refer to the official documentation:
https://docs.xilinx.com/r/en-US/pg269-rf-data-converter
Here, only commonly used APIs are introduced.
Configuring RFDC Operating Status
XRFdc_SetMixerSettings
Function: Passes Mixer/NCO settings to update the corresponding block-level registers. Updates the driver structure with the new values.
Function Prototype:
u32 XRFdc_SetMixerSettings(XRFdc *InstancePtr, u32 Type, u32 Tile_Id, u32 Block_Id, XRFdc_Mixer_Settings *MixerSettingsPtr);
Parameter Description and Values:
*InstancePtr  Pointer to the driver instance
Type         RF-ADC or RF-DAC        RF-ADC: 0 ; RF-DAC: 1
Tile_Id      RF-ADC/RF-DAC tile number    0~3
Block_Id     RF-ADC/RF-DAC block number within the tile    0~3
*MixerSettingsPtr  Pointer to the XRFdc_Mixer_Settings structure for passing Mixer/NCO settings
XRFdc_SetQMCSettings
Function: QMC settings are populated into the corresponding registers. Updates the driver structure with the new values.
Function Prototype:
u32 XRFdc_SetQMCSettings(XRFdc *InstancePtr, u32 Type, u32 Tile_Id, u32 Block_Id, XRFdc_QMC_Settings *QMCSettingsPtr);
Parameter Parameter Description Values
*InstancePtr Pointer to the driver instance
Type RF-ADC or RF-DAC RF-ADC: 0; RF-DAC: 1
Tile_Id RF-ADC/RF-DAC tile number 0~3
Block_Id RF-ADC/RF-DAC block number within the tile 0~3
*QMCSettings Pointer to the XRFdc_QMC_Settings structure used to update the corresponding registers
XRFdc_SetFabClkOutDiv
Function: Use this API to set the PL clock output divider.
Function prototype:
u32 XRFdc_SetFabClkOutDiv(XRFdc *InstancePtr, u32 Type, u32 Tile_Id, u16 FabClkDiv);
Parameter Parameter Description Values
*InstancePtr Pointer to the driver instance
Type RF-ADC or RF-DAC RF-ADC: 0; RF-DAC: 1
Tile_Id RF-ADC/RF-DAC tile number 0~3
Block_Id RF-ADC/RF-DAC block number within the tile 0~3
FabClkDiv PL clock divider set for the tile
Valid values for the clock divider:
Macro Description
XRFDC_FAB_CLK_DIV1 Divided by 1
XRFDC_FAB_CLK_DIV2 Divided by 2
XRFDC_FAB_CLK_DIV4 Divided by 4
XRFDC_FAB_CLK_DIV8 Divided by 8
XRFDC_FAB_CLK_DIV16 Divided by 16
Configuring ADC Related Work Status
XRFdc_SetDecimationFactor
Function: This API function sets the decimation factor for the requested RF-ADC and updates the FIFO write width according to the decimation factor.
Function Prototype:
u32 XRFdc_SetDecimationFactor(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32 DecimationFactor);
Parameter Description and Values
*InstancePtr Pointer to the driver instance
Tile_Id RF-ADC tile number 0~3
Block_Id RF-ADC block number within the tile 0~3
DecimationFactor Decimation factor set for the RF-ADC
Valid decimation factors:
Macro Description
XRFDC_INTERP_DECIM_OFF Interpolation is OFF
XRFDC_INTERP_DECIM_1X 1X Decimation factor
XRFDC_INTERP_DECIM_2X 2X Decimation factor
XRFDC_INTERP_DECIM_3X 3X Decimation factor
XRFDC_INTERP_DECIM_4X 4X Decimation factor
XRFDC_INTERP_DECIM_5X 5X Decimation factor
XRFDC_INTERP_DECIM_6X 6X Decimation factor
XRFDC_INTERP_DECIM_8X 8X Decimation factor
XRFDC_INTERP_DECIM_10X 10X Decimation factor
XRFDC_INTERP_DECIM_12X 12X Decimation factor
XRFDC_INTERP_DECIM_16X 16X Decimation factor
XRFDC_INTERP_DECIM_20X 20X Decimation factor
XRFDC_INTERP_DECIM_24X 24X Decimation factor
XRFDC_INTERP_DECIM_40X 40X Decimation factor
XRFdc_SetFabRdVldWords
Function: This API function sets the requested RF-ADC read PL data rate by writing to the corresponding registers.
Function prototype:
u32 XRFdc_SetFabRdVldWords(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32 FabricRdVldWords);
Parameter Description Value
*InstancePtr Pointer to the driver instance
Tile_Id RF-ADC tile number 0~3
Block_Id RF-ADC block number within the tile 0~3
FabricRdVldWords PL data rate set by the RF-ADC
XRDdc_SetDSA
Function: Sets the DSA value and updates the corresponding block-level registers.
Function prototype:
u32 XRFdc_SetDSA(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, XRFdc_DSA_Settings *SettingsPtr);
Parameter Description Value
*InstancePtr Pointer to the driver instance
Tile_Id RF-ADC tile number 0~3
Block_Id RF-ADC block number within the tile 0~3
*SettingsPtr Pointer to XRFdc_DSA_Settings used to pass the DSA settings.
Configure DAC Related Working Status
XRFdc_SetInterpolationFactor
Function: This API function sets the interpolation factor for the requested RF-DAC and updates the FIFO read width based on the interpolation factor.
Function Prototype:
u32 XRFdc_SetInterpolationFactor(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32 InterpolationFactor);
Parameter Description and Values:
*InstancePtr: Pointer to the driver instance
Tile_Id: RF-DAC tile number 0~3
Block_Id: RF-DAC block number within the tile 0~3
InterpolationFactor: Interpolation factor to set for the RF-DAC
Valid Interpolation Factor Values:
Macro Description
XRFDC_INTERP_DECIM_OFF Interpolation is OFF
XRFDC_INTERP_DECIM_1X 1X interpolation factor
XRFDC_INTERP_DECIM_2X 2X interpolation factor
XRFDC_INTERP_DECIM_3X 3X interpolation factor
XRFDC_INTERP_DECIM_4X 4X interpolation factor
XRFDC_INTERP_DECIM_5X 5X interpolation factor
XRFDC_INTERP_DECIM_6X 6X interpolation factor
XRFDC_INTERP_DECIM_8X 8X interpolation factor
XRFDC_INTERP_DECIM_10X 10X interpolation factor
XRFDC_INTERP_DECIM_12X 12X interpolation factor
XRFDC_INTERP_DECIM_16X 16X interpolation factor
XRFDC_INTERP_DECIM_20X 20X interpolation factor
XRFDC_INTERP_DECIM_24X 24X interpolation factor
XRFDC_INTERP_DECIM_40X 40X interpolation factor
XRFdc_SetFabWrVldWords
Function: This API function sets the requested write structure data rate of the RF-DAC by writing to the corresponding registers.
Function prototype:
u32 XRFdc_SetFabWrVldWords(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32 FabricWrVldWords);
Parameters Description Range
*InstancePtr Pointer to the driver instance
Tile_Id RF-DAC tile number 0~3
Block_Id RF-DAC block number within the tile 0~3
*FabricDataRatePtr Configured structure data rate of the RF-DAC
XRFdc_SetDACVOP
Function: VOP uA current is used to update the corresponding block-level registers, dynamically adjusting signal strength.
Function prototype:
u32 XRFdc_SetDACVOP(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32 uACurrent);
Parameters Description Range
*InstancePtr Pointer to the driver instance
Tile_Id RF-DAC tile number 0~3
Block_Id RF-DAC block number within the tile 0~3
uACurrent Current, in μA 2250 μA~40500 μA
Note: For ES1 silicon, the current range is 6425 μA to 32000 μA (values will be rounded to the nearest increment); for production silicon, the range is 2250 μA to 40500 μA (data will be rounded to the nearest
increment).
