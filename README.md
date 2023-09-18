![Microchip Logo](images/microchip.jpg) 

# dsPIC33CK Curiosity CRC Basic Code Example v1.0.0

The code example uses MPLAB(R) Code Configurator Melody CRC Driver to configure CRC using the standard CRC-16-CCITT settings and calculate the hardware CRC result. The hardware CRC computation is then compared with a software implementation to verify results. The result is displayed on Tera Term.

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
- Any terminal program, like Tera Term (https://ttssh2.osdn.jp/index.html.en) or the MPLAB Data Visualizer

## Hardware Used

### Required Hardware

- [dsPIC33CK Curiosity Development Board (dsPIC33CK256MP508)](https://www.microchip.com/en-us/development-tool/DM330030)

## Hardware Setup

1. Connect the board to the PC using a USB cable.

![Hardware Setup Image](images/hardware_setup.jpg)

## Software Setup

### Terminal Setup
1. Launch the desired terminal program. 
2. Create a new connection (Tera Term: File -> New Connection, Data Visualizer: Serial Port list on the left side).
3. Select the correct COM Port from the dropdown menu on Tera Term or the list on the left on the Data Visualizer.
4. Verify that the serial port settings match the ones below (Setup -> Serial port on Tera Term, settings icon next to the source dropdown in the input section on the Data Visualizer):

![Tera Term Serial Port Settings](images/teraterm_serial_port_menu.JPG)

### MPLAB® X IDE Setup
1. Launch MPLAB® X IDE and load the dspic33ck-curiosity-crc-basic project.
2. Build and program the device. 

## CRC Settings

This code example uses the default settings for CRC-16-CCITT. These are as follows:

![CRC Settings in MCC Melody Builder GUI](images/demo_CRC_settings.JPG)

### Online Calculator

Online calculators can be used to test different configurations and try different settings. Most developers compare results with an online calculator for comparison purposes. An example that was used in the development of this code example is the [Online Calculator by Sven Reifegerste (Zorc)](http://www.zorc.breitbandkatze.de/crc.html).

For this code example, the calculation performed by the MCC Melody CRC Driver can be replicated with the online calculator by the following steps:
- Select "CRC-CCITT" button. 
- Enter "%38%37%36%35%34%33%32%31" in the "Data sequence."
  - Note: Putting "%" before a byte tells this calculator that it is in hexadecimal. Do not include spaces or leave out the "%", as the calculator will pass it as a string.
- Click the "compute" button.
  
The result should be 0x9B4D, matching the calculation performed by the MCC Melody CRC Driver.

## Operation

Once the project is built and the device is programmed, the terminal program will print the results of both the hardware and software calculations.

![Results printed on Tera Term](images/teraterm_output.JPG)