# 2.5 Running the Demo

[Switch to 中文](../../zh/rf-development-guide/06-running-the-demo.md)

Set the DAC current to be sent. 40500 (uA) is the maximum output transmit power, the minimum is 2250 uA, corresponding to a dynamic range of 25 dB
SettingsPtr.Attenuation = 0;
SettingsPtr.DisableRTS = 1;
uint32_t txatt_ua;
for (int i = 0; i < 4; i++)
for (int j = 0; j < 4; j++) {
    txatt_ua = round(40500 / pow(10, ((double)txatt[i * 2 + j] / 1000) / 20));
    Status = XRFdc_SetDACVOP(&RFdcInstPtr, i, j, txatt_ua);
    printf("tile=%d,block=%d,XRFdc_SetDACVOP=%d,Status=%d\n", i, j, txatt_ua, Status);
    Status = XRFdc_SetDSA(&RFdcInstPtr, i, j, &SettingsPtr);
    Status = XRFdc_GetDSA(&RFdcInstPtr, i, j, &SettingsPtr);
    Status = XRFdc_SetDither(&RFdcInstPtr, i, j, 1);
    printf("tile=%d,block=%d,Attenuation=%f,Status=%d\n", i, j, SettingsPtr.Attenuation, Status);
}

5. MTS synchronization

Perform cross-tile synchronization in RFdcDcp_Example.
Status = -1;
while (Status != XRFDC_SUCCESS) {
    // Status = ChangeSampleFreq(&RFdcInstPtr, sample_rate);
Status = qmc_settings(&RFdcInstPtr, XRFDC_ADC_TILE);
mdelay(100);
Status = RFdcDcp_Example(&RFdcInstPtr, &lmk04828_spi);
if (Status != XRFDC_SUCCESS) {
    printf("RFdcDcp initial failed\n");
}
}

## 2.5 Running the demo routine

1. Connect the 12V DC power supply, plug in the Type-C debug cable, and power on the board;
2. Run the application directly in Vitis;

Note: Vitis projects are quite sensitive to paths. When a Vitis project is copied to another path, compilation or downloading may show some errors. A simple solution is to delete the rfevm216_plf in Vitis, create a new platform with the name rfevm216_plf, and use the default parameters. For the XSA file, select the file under the project.

3. Open the serial debug terminal, with the serial port configured as: baud rate 115200, 8 data bits, 1 start bit, 1 stop bit;

The serial output information is as follows:

![RFEVM216 RF development guide illustration](../../assets/rf-development-guide/page-029-image-01.jpg)

[No extractable text on this page.]

![RFEVM216 RF development guide illustration](../../assets/rf-development-guide/page-030-image-01.jpg)

[No extractable text on this page.]

![RFEVM216 RF development guide illustration](../../assets/rf-development-guide/page-031-image-01.jpg)

[No extractable text on this page.]

![RFEVM216 RF development guide illustration](../../assets/rf-development-guide/page-032-image-01.jpg)

[No extractable text on this page.]

![RFEVM216 RF development guide illustration](../../assets/rf-development-guide/page-033-image-01.jpg)

4. Loop back TX0 and RX0 through the loopback RF cable, and observe the RF loopback results through Chipscope

![RFEVM216 RF development guide illustration](../../assets/rf-development-guide/page-034-image-01.jpg)

Note: The sampling points of each channel were observed here.

![RFEVM216 RF development guide illustration](../../assets/rf-development-guide/page-035-image-01.jpg)
