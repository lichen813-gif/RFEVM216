# 4.7 SD Card Read/Write TXT Text Experiment

[Switch to 中文](../../../zh/fpga-tutorial/04-ps-peripherals/07-sd-card.md)

[Back to chapter overview](index.md)

The SD card interface on the RFEVM216 board is designed for a small card, which can connect a Micro SD card (also called a TF card). The MPSoC internally integrates two SD card controllers, and the Xilinx Vitis standalone environment has already ported the FATFS (called xilffs in Vitis) file system. FATFS is a completely open-source and free FAT file system module, specifically designed for small embedded systems. It is entirely written in standard C language, so it has good hardware platform independence and can be easily ported to various embedded processors. Therefore, after adding the xilffs library in Vitis, you can use the API functions provided by FATFS in your program to operate the SD card.
Users do not need to worry about the internal structure of FATFS or the complex FAT protocol; they only need to call a series of application interface functions provided by the FATFS module, such as f_open, f_read, f_write, and f_close. This makes reading/writing files as simple as on a PC.

## 4.7.1 Hardware Design

There is an SD card interface on our RFEVM216 development board, which can connect a Micro SD card (TF card). The schematic is shown in the figure below:

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-141-image-01.jpg)

Figure 15 Micro SD Card Schematic
From the above figure, it can be seen that the SD card has four data lines (SDIO_DAT0~SDIO_DAT3), which are connected to the pins of the MPSoC. In the figure, the SDIO_DETECT signal is the TF card detection signal, used to indicate whether the development board has a TF card connected. When the development board does not have a TF card connected, this signal is high; when the development board has a TF card connected, this signal is low, indicating that the development board already has a TF card connected.

## 4.7.2 Software Design

Add the xilffs library to the BSP library files.
Double-click platform.spr, select Board Support Package, and click Modify BSP Settings...

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-142-image-01.jpg)

Enable the "xilffs" library and click "OK"
After adding the FATFS library, operations on the TF card will be much simpler. We only need to call the FATFS library functions in the program.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-143-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-143-image-02.jpg)

After adding is complete, recompile the platform
Create a new application File->New->Application Project
Click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-144-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-144-image-02.jpg)

Click Next

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-145-image-01.jpg)

Set the application name, then click 'Next'

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-146-image-01.jpg)

Click 'Next'

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-147-image-01.jpg)

Here we choose Empty Application (C) as the template, and click 'Finish'

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-148-image-01.jpg)

Here we can see the newly created application project.
Next, create a new source file "main.c" for the application project.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-149-image-01.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-149-image-02.jpg)

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-150-image-01.jpg)

In the newly created main.c file, we enter the following code:

#include "xparameters.h"

#include "xil_printf.h"

#include "ff.h"

#include "xstatus.h"

#define FILE_NAME "WE5G.txt" // Define the file name

const char src_str[30] = "www.v3t.com.cn"; // Define the text content
// main function
int main()
{

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-151-image-01.jpg)

int status, len;
char dest_str[30] = "";
static FATFS fatfs;
FIL fil; // file object
UINT bw; // number of bytes written returned by f_write function
UINT br; // number of bytes read returned by f_read function
// Register a workspace (mount partition filesystem)
// Before using any other file functions, you must use the f_mount function to register a workspace for each used volume
status = f_mount(&fatfs, "1:/", 1); // mount SD card
if (status != FR_OK) {
xil_printf("\r\nUnable to mount FATfs\r\n");
return -1;
}
xil_printf("Success to open SD card!\r\n");
len = strlen(src_str); // calculate string length
// Open a file, if it does not exist, create a file
status = f_open(&fil, "1:/WE5G.txt", FA_OPEN_ALWAYS | FA_WRITE | FA_READ);
if (status != FR_OK) {
xil_printf("Unable to open file!\r\n");
return -1;
}
xil_printf("Success to open file.\r\n");
// Move the read/write pointer of the opened file object 0: point to the beginning of the file
f_lseek(&fil, 0);
// Write data to the file
f_write(&fil, (void*) src_str, len, &bw);
xil_printf("write file return:%d.\r\n", bw);
// SD card data reading
// sd_read_data(FILE_NAME, (u32)dest_str, len);
f_lseek(&fil, 0);
f_read(&fil, (void*)dest_str, len, &br);
f_close(&fil);
xil_printf("read file return:%d.\r\n", bw);
// Compare whether the written string and the read string are equal
if (strcmp(src_str, dest_str) == 0)
    xil_printf("src_str is equal to dest_str, SD card test success!\r\n");
else
    xil_printf("src_str is not equal to dest_str, SD card test failed!\r\n");
return 0;
}
In the main function, the implemented functionality is to read and write TXT files on the TF card and compare whether the written data and the read data are consistent. The program first calls the f_mount() function to mount the TF card. Next, based on the length of the string to be written, it uses the f_write() function and the f_read() function to write to and read from the TXT file on the TF card, then compares the written and read values and prints the comparison result.

## 4.7.3 Download Verification

First, we connect the download cable (USB to Type-C cable) to the JTAG interface of the development board, with the other end connected to the computer. Next, insert the TF card. Finally, turn on the power switch of the development board.
Right-click the application project, select Run As -> Launch Hardware (Single Application Debug).
Open the serial terminal. After the download is complete, you can check the serial output:
From the above figure, it can be seen that the displayed written characters and the read characters are consistent, indicating that the TF card read/write test was successful.
Next, remove the TF card from the development board slot, and use a card reader to connect it to the USB port of the computer. At this time, the file contents on the TF card can be seen as shown in the figure below.

![RFEVM216 FPGA tutorial illustration](../../../assets/fpga-tutorial/page-153-image-01.jpg)

Open the "WE5G.txt" text file, and you can see the content of the text, as shown in the figure below:

## 4.7.4 Reference Documents

http://elm-chan.org/fsw/ff/00index_e.html
