---
platform: Atmel Studio7
device: Atmel SAMG55J19
language: c
---

Run a simple C sample on SAM G55 Xplained Pro device running Atmel Studio7
===
---

# Table of Contents

-   [Introduction](#Introduction)
-   [Step 1: Prerequisites](#Prerequisites)
-   [Step 2: Prepare your Device](#PrepareDevice)
-   [Step 3: Build and Run the Sample](#Build)

<a name="Introduction"></a>
# Introduction

**About this document**

This document describes how to connect SAM G55 Xplained Pro device running Atmel Studio7 with Azure IoT SDK. This multi-step process includes:
-   Configuring Azure IoT Hub
-   Registering your IoT device
-   Build and deploy Azure IoT SDK on device

<a name="Prerequisites"></a>
# Step 1: Prerequisites

You should have the following items ready before beginning the process:

-   Computer with Git client installed and access to the
    [azure-iot-sdks](https://github.com/Azure/azure-iot-sdks) GitHub
    public repository.
-   Required software
    -   A computer with the [Atmel Studio 7.0](http://www.atmel.com/tools/atmelstudio.aspx#download) or later installed.
-   Required hardware:
    - [SAM G55 Xplained Pro Evaluation Kit](http://www.atmel.com/tools/ATSAMG55-XPRO.aspx)
    - [ATWINC1500-XPRO WiFi extension board](http://www.atmel.com/tools/atwinc1500-xpro.aspx)
-   Download and install [DeviceExplorer](https://github.com/Azure/azure-iot-sdks/releases/download/2015-11-13/SetupDeviceExplorer.msi).
-   [Set up your IoT hub](https://github.com/Azure/azure-iot-sdks/blob/master/doc/setup_iothub.md).

#### Create a device on IoT Hub
-   With your IoT hub configured and running in Azure, follow the instructions in **"Create Device"** section of [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdks/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md).

#### Write down device credentials
-   Make note of the Connection String for your device by following the instructions in **"Get device connection string or configuration data"** section of [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdks/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md).

<a name="PrepareDevice"></a>
# Step 2: Prepare your Device
- This section shows you how to set up a development environment for the Azure IoT device SDK with the SAMG55 and WINC1500 board.
 - Make sure : you should connect a WINC1500 to "EXT1" port on SAMG55 board.
-  'If you need to setup your SAMG55 device, please refer to the "Getting Started" instructions here. [here](<http://www.atmel.com/tools/ATSAMG55-XPRO.aspx?tab=documents>) .

## How to update firmware and Flash the root certificate of the Azure IoT hub host
-  Please convert ms.der to ms.cer with following steps on Windows pc.
    -  Download ms.der file from [Azure cert](https://github.com/Azure/azure-iot-sdks/tree/master/c/certs)
    -  Open ms.der by double-clinking then you can see a window with title "Certificate"
    -  Select "Details" tab -> click "Copy to File" -> click "Next" button of "Certificate Export Wizard" window
    -  Select "DER encoded binary x.509(.CER)" -> click "Next" button -> enter file name to text field and save it in your pc
-  Open Atmel Studio7 and search for the Firmware Update Project from the ```File -> New -> Example Project...``` menu in Atmel Studio.
    -  Select ```SAM G, 32-bit``` from ```Device Family:``` and Type ```winc1500``` to input text field.
    -  Select the appropriate ```WINC1500 Firmware Update Project (vxx.x.x)``` project corresponding to your Xplained Pro board and then press OK button to import firmware update project and related documentation. (for example, ```WINC1500 Firmware Update Project(v19.4.4) - SAMG55 Xplained Pro```)
        - Copy your certificate files (.cer) in the src/firmware/Tools/root_certificate_downloader/crt folder 
(The section “3. Root Certificates Update Procedure” of “Atmel-AN004-Firmware-Update-Procedure-for-WINC1500-WiFi-Module-using-a-SAM-Xplained-Pro.pdf”)
        - Just run “samg55_xplained_pro_firmware_update.bat” (that is located in  “src/samg55_xplained_pro_firmware_update.bat”)
    -  For detailed procedure for updating firmware and flashing the root certificate of the Azure IoT hub host, please refer the ```Atmel-AN004-Firmware-Update-Procedure-for-WINC1500-WiFi-Module-using-a-SAM-Xplained-Pro.pdf``` document. (This document is located in 'src/doc' on the project created on previous step)

<a name="Build"></a>
# Step 3: Build and Run the sample

<a name="Load"></a>
## 3.1 Build SDK and sample

<a name="buildrunapp"/>
## Build and Run the sample project via Atmel Studio7: 
1. Open Atmel Studio7 and search for the MS Azure IoT project from the File -> New -> Example Project... menu in Atmel Studio.
    - Select SAM G, 32-bit from Device Family: and Type winc1500 to input text field.
    - Select the MS Azure IoT project corresponding to your Xplained Pro board and then press OK button to import MS Azure IoT project
2. Open the ```simplesample_http.c``` file in the Atmel Studio7.
    - Locate the following code in the ```simplesample_http.c```: 
    ```static const char* connectionString = "[device connection string]";``` .
    - Replace ```[device connection string]``` with the device connection string you noted in [Step 1](#Step-1:-Prerequisites) and save the changes.
3. In ```main.h```, update the following line with your WiFi accesspoint's SSID and password:
   ```
   #define MAIN_WLAN_SSID                  "your_AP_SSID" /**< Destination SSID */
   ```
   
   ```
   #define MAIN_WLAN_PSK                   "password" /**< Password for Destination SSID */
   ```
4. Build the project, which can be accessed via ```Build -> Build Solution   F7``` .
5. Upload a binary to SAMG55 board, which can be accessed via ```Debug -> Continue   F5``` .

## 3.2 Send Device Events to IoT Hub:

-   On Windows, refer "Monitor device-to-cloud events" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdks/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) to see the data your device is sending.

-   If you are running other OS, please use the JavaScript tool [iot-hub explorer tool](https://github.com/Azure/azure-iot-sdks/tree/master/tools/iothub-explorer/doc)

## 3.3 Receive messages from IoT Hub

-   On Windows, refer "Send cloud-to-device messages" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdks/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) for instructions on sending messages to device.

-   If you are running other OS, please use the JavaScript tool [iot-hub explorer tool](https://github.com/Azure/azure-iot-sdks/tree/master/tools/iothub-explorer)
