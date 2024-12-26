This is a passion project I’ve wanted to pursue for a while:). If you find any errors, please let me know!

<p align="center">
  <img src="https://github.com/user-attachments/assets/3e2c3925-b929-40fb-822a-9deeb70dd5db"/>
</p>

# Some background 
Before we start, let's clarify a few things. There are many microcontrollers that work well with FreeRTOS, and even ZephyrRTOS. I am using the [Nordic Semiconductor nRF52DK](https://www.nordicsemi.com/Products/Development-hardware/nRF52-DK), specifically the [nrf52832 (PCA10040) version](https://www.nordicsemi.com/Products/nRF52832), After wasted my time on my thesis with the newer nRF53DK, I realized it was more complex than necessary. Instead of investing more time learning a new board, I’m using my existing skills to set up FreeRTOS on a simpler Nordic board.


## What is ZephyrRTOS and FreeRTOS?
[ZephyrRTOS](https://docs.zephyrproject.org/latest/index.html) and [FreeRTOS](https://www.freertos.org/Documentation/02-Kernel/07-Books-and-manual/01-RTOS_book) are both real-time operating systems (RTOS) used for embedded systems development. ZephyrRTOS is an open-source, scalable OS designed for resource-constrained devices, supporting various hardware architectures and offering features like native networking stacks and device drivers. FreeRTOS, also open-source, is known for its simplicity and minimal footprint, making it widely adopted in small microcontroller applications. While FreeRTOS focuses on a lightweight kernel for basic scheduling and task management, Zephyr provides a more feature-rich environment with support for multiple communication protocols and file systems.








# Installing Segger Embedded Studio (SES)
We could use the Visual Studio nRF extension, but keep in mind that it primarily focuses on ZephyrRTOS, while FreeRTOS is a third-party platform. This means we'd have to manually link certain files, CMake, and GCC to get FreeRTOS working. Instead, we’re going to simplify the process by installing [Segger Embedded Studio](https://www.segger.com/downloads/embedded-studio/).

<p align="center">
  <img src="https://github.com/user-attachments/assets/45944928-68a0-471b-a072-977cfdd68481"/>
</p>



# Installing drivers and files for FreeRTOS nrf52832 (PCA10040)

First, we need to install the [nRF5 SDK](https://www.nordicsemi.com/Products/Development-software/nRF5-SDK/Download). As of September 29th, 2024, you'll need to download a compatible version of the nRF5 SDK. I'll be using version 17.1.0, as it is the latest available. Here's how to get started:

<p align="center">
  <img src="https://github.com/user-attachments/assets/8392edf5-61b5-4b6e-ac50-a0d952d07f00"/>
</p>

The next step is to determine which **SoftDevice** to use. Since we're working with the *nRF52832 (PCA10040)*, we need to select a SoftDevice that is compatible with our board and fits our project requirements. To find the available options, scroll down the page to see the choices listed for this board:

<p align="center">
  <img src="https://github.com/user-attachments/assets/cbac46ba-e2c8-4510-b3f7-7ebd350c4f1b"/>
  <img src="https://github.com/user-attachments/assets/cef6a60a-edd6-4aac-91a6-e8a74fbdb9e2"/>
  <img src="https://github.com/user-attachments/assets/3962151f-552c-4759-b85c-d8705ae9100a"/>
  <img src="https://github.com/user-attachments/assets/44dcbe3e-7b1d-4279-9da9-1c92b365727d"/>

</p>

I will be selecting **SoftDevice S132** since I don't need ANT and prioritize performance and BLE. Just remember to select only the SoftDevice that fits your needs, and avoid choosing multiple options. Once you've made your selection, scroll down until you see the download option, and click on it.

<p align="center">
  <img src="https://github.com/user-attachments/assets/15d83cd1-aea8-4fa4-857d-a934d92980f0"/>
</p>

Once you have downloaded the files, you should see two folders. Extract both. We'll focus on the **nRF5_SDK folder** and naviate to the following directories:
- *examples>peropheral>blinky_freertos*
- *examples>peropheral>blinky_rtc_freertos*

Copy both of these folders and save them in a secure location. I'll be placing them in my project folder.

# Using the example FreeRTOS file from nRF5_DK folder
I will be using the **blinky_freertos** sample. Open Segger Embedded Studio, click on *Open Existing Application*, and locate the **blinky_freertos** folder. In that folder, find the file with the ***.emProject*** extension. Follow this directory path to locate the project file:

<p align="center">
  <img src="https://github.com/user-attachments/assets/cc7d717b-dce8-481f-a149-8974b9101bba"/>
  Directory Path: ~/nRF5_SDK_17.1.0/examples/peripheral/blinky_freertos/pca10040/blank/ses/
</p>

Where you should get the following:
<p align="center">
  <img src="https://github.com/user-attachments/assets/e020bde9-2199-4119-b34e-a056eceae7ef"/>
</p>



## Configuring the Target Board
If you have selected the *PCA10040* you should be fine as long as you are using the same board, *nRF52832*.

# Optional: BLE Integration with FreeRTOS
This next step is optional, but why have a Nordic board and not take advantage of its BLE features? For this, you'll need to download [nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-Desktop) We're going to use it to flash the board with the **SoftDevice** file. Once downloaded, open the application and install the **Programmer** tool from within the app. As shown in the image, disregard any other applications I’ve installed in nRF Connect for Desktop.


<p align="center">
  <img src="https://github.com/user-attachments/assets/05383bb7-85fc-486f-b547-f41c98b631bf"/>
</p>


Make sure your nRF52DK is connected, select device, find the board, and drag the **SoftDevice** file. And Flash the board. You are done!


# Flashing your nRF52DK on SES

## Connecting the board through J-Link
First, we need to ensure that the nRF52DK is connected in SES. To do this, check the SES menu:
<p align="center">
  <img src="https://github.com/user-attachments/assets/d415a6cd-8bb2-4b0e-8156-acccf1648a80"/>
</p>


<p align="center">
  <img src=""/>
</p>


In the **SES** menu, select **Target**, then choose **Connect J-Link**:
<p align="center">
  <img src="https://github.com/user-attachments/assets/8f3fe78a-b8e0-48f3-8702-e15dbf773127"/>
</p>




Next, check the bottom of the screen where it says **Output**. It should display either *Connecting J-Link using USB* or *Target connection has been lost*:
<p align="center">
  <img src="https://github.com/user-attachments/assets/4f80d3c8-22be-4617-bd4c-92095f9bdecb"/>
</p>

## Building the Project
Go to **Build** then select **Build Solution**:
![image](https://github.com/user-attachments/assets/50dc698a-96f0-4f2e-b9d0-f46cc43d4043)

Where the **Output** should state:










