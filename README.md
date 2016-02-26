---
platform: Atmel
device: SAMG55
language: c
---

Run a simple C sample on Atmel SAMG55 device
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
-   Required hardware:
    - SAMG55 board
    - WINC1500 shield
-   [Setup your IoT hub][lnk-setup-iot-hub]
-   [Provision your device and get its credentials][lnk-manage-iot-hub]

<a name="Step-2-PrepareDevice"></a>
# Step 2: Prepare your Device

-  Connect the SAMG55 using the USB cable.
-  If you need to setup your SAMG55 device, please refer the getting started instructions [here](<http://www.atmel.com/tools/ATSAMG55-XPRO.aspx?tab=documents>) .

<a name="Step-3-Build"></a>
# Step 3: Build and Run the sample

<a name="setup"/>
## Setup the development environment

This section shows you how to set up a development environment for the Azure IoT device SDK for C on Atmel Studio.

1. In the Atmel Studio, select File->New->Example Project.

<a name="buildrunapp"/>
## Run the sample

1. Open the file **c/serializer/samples/simplesample_http/simplesample_http.c** in a text editor.

2. Locate the following code in the file:
    ```
   static const char* connectionString = "[device connection string]";
    ```
3. Replace "[device connection string]" with the device connection string you noted [earlier](#Step-1-Prerequisites). Save the changes.

5. Save your changes and build the samples. To build your sample project.

[lnk-setup-iot-hub]: ../setup_iothub.md
[lnk-manage-iot-hub]: ../manage_iot_hub.md
