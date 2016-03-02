Run a simple C sample on SAM G55 Xplained Pro device running Atmel Studio7
===
---

# Table of Contents

-   [Introduction](#Introduction)
-   [Step 1: Prerequisites](#Prerequisites)
-   [Step 2: Prepare your Device](#PrepareDevice)
-   [Step 3: Build and Run the Sample](#Build)
-   [Tips](#tips)

# Instructions for using this template

-   Replace the text in {placeholders} with correct values.
-   Delete the lines {{enclosed}} after following the instructions enclosed between them.
-   It is advisable to use external links, wherever possible.
-   Remove this section from final document.

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
-  If you need to setup your SAMG55 device, please refer the getting started instructions [here](<http://www.atmel.com/tools/ATSAMG55-XPRO.aspx?tab=documents>) .

## how to update firmware and Flash the root certificate of the Azure IoT hub host
-  Step 1. Open Atmel Studio7 and search for the Firmware Update Project from the ```File -> New -> Example Project...``` menu in Atmel Studio.
-  Step 2. Select ```SAM G, 32-bit``` from ```Device Family:``` and Type ```winc1500``` to input text field.
-  Step 3. Select the appropriate ```WINC1500 Firmware Update Project (vxx.x.x)``` project corresponding to your Xplained Pro board and then press OK button to import firmware update project and related documentation. (for example, ```WINC1500 Firmware Update Project(v19.4.4) - SAMG55 Xplained Pro```)
-  Step 4. for detailed procedure for updating firmware and flashing the root certificate of the Azure IoT hub host, please refer the ```Atmel-AN004-Firmware-Update-Procedure-for-WINC1500-WiFi-Module-using-a-SAM-Xplained-Pro.pdf``` document. (this document is located in src/doc from the Step 3)

<a name="Build"></a>
# Step 3: Build and Run the sample

<a name="Load"></a>
## 3.1 Build SDK and sample

-   Open a PuTTY session and connect to the device.

-   Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by issuing the following commands from the command line on your board:
{{***Keep the command set based on your OS and remove the rest.***}}

    {{**Debian or Ubuntu**}}

        sudo apt-get update

        sudo apt-get install -y curl libcurl4-openssl-dev uuid-dev uuid g++ make cmake git unzip openjdk-7-jre

    {{**Fedora**}}

        sudo dnf check-update -y

        sudo dnf install libcurl-devel openssl-devel libuuid-devel uuid-devel gcc-c++ make cmake git unzip java-1.7.0-openjdk

    {{**Any Other Linux OS**}}

        Write equivalent commands on the target OS

    {{***If any other software is required, please specify here the command(s) for installing same.***}}

-   Download the Microsoft Azure IoT Device SDK for C to the board by issuing the following command on the board::

        git clone https://github.com/Azure/azure-iot-sdks.git

-   Edit the following file using any text editor of your choice:
    {{***Keep the file based on your protocol(s) and remove the rest.***}}

    {{**For AMQP protocol:**}}

        azure-iot-sdks/c/iothub_client/samples/iothub_client_sample_amqp/iothub_client_sample_amqp.c

    {{**For HTTPS protocol:**}}

        azure-iot-sdks/c/iothub_client/samples/iothub_client_sample_http/iothub_client_sample_http.c

-   Find the following place holder for IoT connection string:

        static const char* connectionString = "[device connection string]";

-   Replace the above placeholder with device connection string you obtained in [Step 1](#Step-1:-Prerequisites) and save the changes.

-   On the board, run the following command to build and install Apache Proton library:

        sudo ./azure-iot-sdks/c/build_all/linux/build_proton.sh --install /usr
        chmod +x ./azure-iot-sdks/c/build_all/linux/build_paho.sh
        ./azure-iot-sdks/c/build_all/linux/build_paho.sh

-   Assuming everything went OK on the build_proton.sh, you can now build the SDK samples using the following command:

        sudo ./azure-iot-sdks/c/build_all/linux/build.sh

## 3.2 Send Device Events to IoT Hub:

-   Run the sample by issuing following command:
{{***Keep the command set based on your protocol(s) and remove the rest.***}}

    {{**If using AMQP protocol:**}}

        ~/cmake/iothub_client/samples/iothub_client_sample_amqp/linux/iothub_client_sample_amqp

    {{**If using HTTPS protocol:**}}

        ~/cmake/c/iothub\_client/samples/iothub_client_sample_http/linux/iothub_client_sample_http

-   On Windows, refer "Monitor device-to-cloud events" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdks/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) to see the data your device is sending.

-   If you are running other OS, please use the JavaScript tool [iot-hub explorer tool](https://github.com/Azure/azure-iot-sdks/tree/master/tools/iothub-explorer/doc)

## 3.3 Receive messages from IoT Hub

-   On Windows, refer "Send cloud-to-device messages" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdks/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) for instructions on sending messages to device.

-   If you are running other OS, please use the JavaScript tool [iot-hub explorer tool](https://github.com/Azure/azure-iot-sdks/tree/master/tools/iothub-explorer/doc)

<a name="tips"></a>
# Tips

- If you just want to build the serializer samples, run the following commands:

  ```
  cd ./c/serializer/build/linux
  make -f makefile.linux all
  ```
