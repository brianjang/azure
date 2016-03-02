---
platform: Atmel Studio7
device: Atmel SAMG55J19
language: c
---

Run a simple C sample on Atmel SAMG55 and WINC1500 device
===
---

# Table of Contents

-   [Introduction](#Introduction)
-   [Step 1: Prerequisites](#Step-1-Prerequisites)
-   [Step 2: Prepare your Device](#Step-2-PrepareDevice)
-   [Step 3: Build and Run the Sample](#Step-3-Build)

<a name="Introduction"></a>
# Introduction

**About this document**

This document describes how to connect Atmel SAMG55 device with Azure IoT SDK. This multi-step process includes:
-   Configuring Azure IoT Hub
-   Registering your IoT device
-   Build and deploy Azure IoT SDK on device

<a name="Step-1-Prerequisites"></a>
# Step 1: Prerequisites

You should have the following items ready before beginning the process:

-   Computer with Git client installed and access to the
    [azure-iot-sdks](https://github.com/Azure/azure-iot-sdks) GitHub public repository.
-   A computer with the Atmel Studio 7.0 or later installed.
    - [Atmel Studio Download](http://www.atmel.com/tools/atmelstudio.aspx#download)   
-   Required hardware:
    - [SAM G55 Xplained Pro Evaluation Kit](http://www.atmel.com/tools/ATSAMG55-XPRO.aspx)
    - [ATWINC1500-XPRO WiFi extension board](http://www.atmel.com/tools/atwinc1500-xpro.aspx)
-   [Setup your IoT hub][lnk-setup-iot-hub]
-   [Provision your device and get its credentials][lnk-manage-iot-hub]

<a name="Step-2-PrepareDevice"></a>
# Step 2: Prepare your Device

- This section shows you how to set up a development environment for the Azure IoT device SDK with the SAMG55 and WINC1500 board.
-  If you need to setup your SAMG55 device, please refer the getting started instructions [here](<http://www.atmel.com/tools/ATSAMG55-XPRO.aspx?tab=documents>) .

## how to update firmware and Flash the root certificate of the Azure IoT hub host
-  Step 1. Open Atmel Studio7 and search for the Firmware Update Project from the “File -> New -> Example Project..." menu in Atmel Studio.
-  Step 2. Select "SAM G, 32-bit" from "Device Family:" and Type "winc1500" to input text field.
-  Step 3. Select the appropriate “WINC1500 Firmware Update Project (vxx.x.x)” project corresponding to your Xplained Pro board and then press OK button to import firmware update project and related documentation. (for example, WINC1500 Firmware Update Project(v19.4.4) - SAMG55 Xplained Pro)
-  Step 4. for detailed procedure for updating firmware and flashing the root certificate of the Azure IoT hub host, please refer the "Atmel-AN004-Firmware-Update-Procedure-for-WINC1500-WiFi-Module-using-a-SAM-Xplained-Pro.pdf" document. (this document is located in src/doc from the Step 3)

<a name="Step-3-Build"></a>
# Step 3: Build and Run the sample

<a name="buildrunapp"/>
## Build and Run the sample project via Atmel Studio7: 
1. double click "Ateml_Azure_EXAMPLE.atsln" : **```TBD```**
2. Open the ```simplesample_http.c``` file in the Atmel Studio7.
3. Locate the following code in the ```simplesample_http.c```: 
    ```static const char* connectionString = "[device connection string]";``` .
4. Replace ```[device connection string]``` with the device connection string you noted [earlier](#Step-1-Prerequisites). Save the changes.
5. In ```main.h```, update the following line with your WiFi accesspoint's SSID and password:
   ```
   #define MAIN_WLAN_SSID                  "your_AP_SSID" /**< Destination SSID */
   ```
   
   ```
   #define MAIN_WLAN_PSK                   "password" /**< Password for Destination SSID */
   ```
6. Build the project, which can be accessed via ```Build -> Build Solution   F7``` .
7. upload a binary to SAMG55 board, which can be accessed via ```Debug -> Continue   F5``` .

## Monitor device data and send messages

-   See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application and how to send cloud-to-device messages to the application.



[lnk-setup-iot-hub]: ../setup_iothub.md
[lnk-manage-iot-hub]: ../manage_iot_hub.md
