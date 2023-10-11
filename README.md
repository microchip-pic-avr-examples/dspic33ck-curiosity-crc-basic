![Microchip Logo](images/microchip.jpg) 

# dsPIC33CK Curiosity CRC Basic Code Example

The code example uses MPLAB® Code Configurator Melody CRC Driver to configure CRC using the standard CRC-16-CCITT settings and calculate the hardware CRC result. The hardware CRC computation is then compared with a software implementation to verify results. The result is displayed on the terminal.

## Related Documentation

[MCC Melody CRC API Reference](https://onlinedocs.microchip.com/v2/keyword-lookup?keyword=CRC_16BIT_MELODY_DRIVER&version=latest&redirect=true)

## Software Used 

### Required Software

- MPLAB® X IDE **6.15** or newer (https://www.microchip.com/MPLABXIDE)
- MPLAB® XC16 Compiler **2.10** or a newer compiler (https://www.microchip.com/xc16)
- MPLAB® Code Configurator (MCC) **5.5.7** or newer (https://www.microchip.com/mcc)
- MPLAB® Code Configurator (MCC) Melody **2.6.1** or newer (https://www.microchip.com/melody)
- CRC Driver **1.0.3** or newer (MCC Content Manager)
- CRC PLIB **1.3.0** or newer (MCC Content Manager)
- UART Driver **1.8.0** or newer (MCC Content Manager)
- UART PLIB **1.4.1** or newer (MCC Content Manager)
- Any terminal program, like the MPLAB® Data Visualizer (https://www.microchip.com/datavisualizer) or Tera Term (https://ttssh2.osdn.jp/index.html.en)

## Hardware Used

### Required Hardware

- [dsPIC33CK Curiosity Development Board (dsPIC33CK256MP508)](https://www.microchip.com/en-us/development-tool/DM330030)

## Hardware Setup

1. Connect the board to the PC using a USB cable.

![Hardware Setup Image](images/hardware_setup.jpg)

## Software Setup

### Terminal Setup (Data Visualizer)

1. Launch the MPLAB® Data Visualizer.

![Data Visualizer Icon](images/data_visualizer_icon.JPG)

2. Find the correct COM Port from the list on the left and click the play button.

![COM Port list withplay button highlighted](images/dv_COM_select_play_highlighted.JPG)

3. Select the "Send to Terminal" button.

![Send to Terminal button](images/dv_data_capture_menu.JPG)

4. Click on the settings icon next to the source dropdown in the input section.

![Source Settings Icon](images/dv_source_settings_button.JPG)

5. Verify that the serial port settings match the following:

![Source Settings Menu](images/dv_source_settings.JPG)

### Terminal Setup (Tera Term)
1. Launch Tera Term
2. Go to File -> New Connection.
3. Select the "Serial" option and select the correct COM Port from the dropdown menu.

![COM port selection](images/tera_term_COM_port_selection.JPG)

4. Go to Setup -> Serial port and ensure that the settings match the following:

![Tera Term Serial Port Settings](images/tera_term_serial_port_menu.JPG)

### MPLAB® X IDE Setup
1. Launch MPLAB® X IDE and load the dspic33ck-curiosity-crc-basic project.
2. Build and program the device. 

## CRC Settings

The following settings are used in the calculation of CRC values:

- Shift direction: The direction the data is shifted through the registers. Can start with the most significant bit (MSB) or the least significant bit (LSB)
- Initial Value: The initial value of the CRC result. Can theoretically be anything, but traditionally is either zero (0x0000 for 16-bit or 0x00000000 for 32-bit) or -1 (0xFFFF for 16-bit or 0xFFFFFFFF for 32-bit).
- Reverse: The result of the CRC calculation can be reversed immediately after calculation. The value is true (perform reverse) or false (no reverse).
- Final XOR Value: The value XOR'd with the CRC result after the calculation and any reverses. Can theoretically be anything, but traditionally is either zero (0x0000 for 16-bit or 0x00000000 for 32-bit) or -1 (0xFFFF for 16-bit or 0xFFFFFFFF for 32-bit).
- Polynomial: Generator polynomial used in the calculation of the CRC value. Many effective polynomials exist, but some of the most common are CRC-16-CCITT (0x1021) and CRC-32 (0x04C11DB7).

For CRC-16-CCITT, the settings are as follows:

- Shift Direction: MSB
- Initial Value: -1 (0xFFFF)
- Reverse: No Reverse
- Final XOR Value: 0 (0x0000)
- Polynomial: 0x1021

### Online Calculator

Online calculators can be used to test different configurations and try different settings. Most developers compare results with an online calculator for comparison purposes. An example that was used in the development of this code example is the [Online Calculator by Sven Reifegerste (Zorc)](http://www.zorc.breitbandkatze.de/crc.html).

| Setting | MCC Melody | Online Calculator | Register | API | 
| --- | --- | --- | --- | --- |
| CRC Order | Word Width (Bits) | CRC order (1..64)| CRCCONH (CRCCONHbits.PLEN) | Register value set in CRC_Initialize() |
| Polynomial | Pre Defined Polynomial / Value | CRC polynom (hex) | CRCXORL (and CRCXORH for 32 bits) | Register value set in CRC_Initialize() |
| Initial Value | Initial Value | Initial value (hex) | CRCWDATL (and CRCWDATH for 32 bits) | CRC_SeedSet() |
| Final XOR | No setting in MCC Melody | Final XOR value (hex) | Not stored in a register | CRC_CalculationResultXORGet(), Input in CRC_CalculationResultGet() |
| Shift Direction | Data -> Shift Direction | reverse data bytes | CRCCONL (CRCCONLbits.LENDIAN) | Register value set in CRC_Initialize() | 
| Reverse | register value set in  | reverse CRC result before Final XOR | Not stored in a register | CRC_CalculationResultReverseGet(), Input in CRC_CalculationResultGet() | 
| Data | Not visible in the MCC Melody UI | Data sequence | Fed into CRCDATL | No API |

For this code example, the calculation performed by the MCC Melody CRC Driver can be replicated with the online calculator by the following steps:
- Select "CRC-CCITT" button.
- Enter the folowing for "data sequence": %38%37%36%35%34%33%32%31
- Click the "compute" button.
  
The result should be 0x9B4D, matching the calculation performed by the MCC Melody CRC Driver.

## Operation

Once the project is built and the device is programmed, the terminal program will print the results of both the hardware and software calculations.

![Results printed on Tera Term](images/tera_term_output.JPG)