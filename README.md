This is a side passion I been wanting to do for a while:). If you fine any errors, please let me know!!!

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

# Using the sample file for FreeRTOS nRF52DK















