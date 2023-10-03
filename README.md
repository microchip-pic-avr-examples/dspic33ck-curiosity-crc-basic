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

This code example uses the following default settings for CRC-16-CCITT:

| Setting | MCC Melody | Online Calculator | Firmware |
| --- | --- | --- | --- |
| CRC Order | ![CRC Order in MCC Melody](images/crc_settings_table_images/crc_order_mcc_melody.JPG) | ![CRC Order in Online Calculator](images/crc_settings_table_images/crc_order_online_calc.JPG) | ![CRC Order in Firmware](images/crc_settings_table_images/crc_order_firmware.JPG) | 
| Polynomial | ![Polynomial in MCC Melody](images/crc_settings_table_images/polynomial_mcc_melody.JPG) | ![Polynomial in Online Calculator](images/crc_settings_table_images/polynomial_online_calc.JPG) | ![Polynomial in Firmware](images/crc_settings_table_images/polynomial_firmware.JPG) | 
| Initial Value | ![Initial Value in MCC Melody](images/crc_settings_table_images/initial_value_mcc_melody.JPG) | ![Initial Value in Online Calculator](images/crc_settings_table_images/initial_value_online_calc.JPG) | ![Initial Value in Firmware](images/crc_settings_table_images/initial_value_firmware.JPG) | 
| Final XOR | ![Final XOR in MCC Melody](images/crc_settings_table_images/final_xor_mcc_melody.JPG) | ![Final XOR in Online Calculator](images/crc_settings_table_images/final_xor_online_calc.JPG) | ![Final XOR in Firmware](images/crc_settings_table_images/final_xor_firmware.JPG) |
| Shift Direction | ![Shift Direction in MCC Melody](images/crc_settings_table_images/shift_direction_mcc_melody.JPG) | ![Shift Direction in Online Calculator](images/crc_settings_table_images/shift_direction_online_calc.JPG) | ![Shift Direction in Firmware](images/crc_settings_table_images/shift_direction_firmware.JPG) | 
| Reverse | ![Reverse in MCC Melody](images/crc_settings_table_images/reverse_mcc_melody.JPG) | ![Reverse in Online Calculator](images/crc_settings_table_images/reverse_online_calc.JPG) | ![Reverse in Firmware](images/crc_settings_table_images/reverse_firmware.JPG) | 
| Data | Not visible in the MCC Melody UI | ![Data in Online Calculator](images/crc_settings_table_images/data_online_calc.JPG) | ![Data in Firmware](images/crc_settings_table_images/data_firmware.JPG) | 

![CRC Settings in MCC Melody Builder GUI](images/demo_CRC_settings.JPG)

### Online Calculator

Online calculators can be used to test different configurations and try different settings. Most developers compare results with an online calculator for comparison purposes. An example that was used in the development of this code example is the [Online Calculator by Sven Reifegerste (Zorc)](http://www.zorc.breitbandkatze.de/crc.html).

For this code example, the calculation performed by the MCC Melody CRC Driver can be replicated with the online calculator by the following steps:
- Select "CRC-CCITT" button. This will set all of the settings to their desired values:
  - CRC order should be 16, since we are using a 16-bit polynomial.
  - CRC polynom should be set to "1021," which is the hex value for the CRC-16-CCITT polynomial.
  - Initial value should be set to "FFFF," which is the hex value for -1, the standard for CRC-16-CCITT.
  - Final XOR value should be set to zero, the standard value for CRC-16-CCITT.
  - The reverse data bytes checkbox sets the shift direction. Unchecked leads to using the MSB direction, which is the standard for CRC-16-CCITT.
  - The reverse CRC result before Final XOR checkbox sets whether the CRC result will be reversed after calculation. Unchecked leads to no reverse being performed, which is the standard for CRC-16-CCITT.
- Enter "%38%37%36%35%34%33%32%31" in the "Data sequence."
  - Note: Putting "%" before a byte tells this calculator that it is in hexadecimal. Do not include spaces or leave out the "%", as the calculator will pass it as a string.
- Click the "compute" button.
  
The result should be 0x9B4D, matching the calculation performed by the MCC Melody CRC Driver.

## Operation

Once the project is built and the device is programmed, the terminal program will print the results of both the hardware and software calculations.

![Results printed on Tera Term](images/tera_term_output.JPG)