# 8 Port LED Distro
![8 Port LED Distro Version 1](./img/8_Port_LED_Distro_V1andV2.png)

This document will serve as a place to answer questions about the 8 Port LED Distro.

## What is it?
This is an 8 port ESP32 based LED distro board running WLED. Distributing both power and data in 1 board. The WT32-ETH01 provides support for Wi-Fi or ethernet connections. It can be used with either 5v or 12v or 24v LED pixels. Also includes a USB-C port for easy programming.

## Where can I get one?
You can purchase the 8 Port LED Distro in our [Tindie store](https://www.tindie.com/products/27884/).

## What's new in version 2?
- All the components of the WT32-ETH01 have been moved down to the main PCB.
- A new step up/down converter is used to turn 5v, 12v and 24v into 5v needed for the level shifter.
- Improved circuit for making the 3.3v needed by the ESP32 and the ethernet port.
- H1 Header now has 3 GPIO ports so a digital microphone like the INMP441 can be connected.
- H2, H3, and H4 headers are inputs.  They can be used for buttons and temperature sensors.
- Doubled up positive traces for the fuses and phoenix connectors.  There are now 1oz traces on both the top and bottom of the PCB.
- The Ethernet jack now faces up away from the PCB.  The PCB can be put up against something and you can still plug in the ethernet.
- The GPIO mapping for the LED ports has been rearranged.  It should be easier to remember what they are.

## How do I hook up a relay?
On the board by the USB-C connector there is a header labeled H1 with 5V, IO32 and GND. IO32 can be used as an output to control an external relay. I would follow this tutorial https://esp32io.com/tutorials/esp32-relay and connect 5V for DC+, GND to DC-, and IO32 to IN. You will have to do some configuration in WLED to tell it what port the relay is on.

## Can a relay be used to turn the board on and off?
No, a relay can not be used to turn the board on and off.  There is only 1 power input for the board if you use a relay to turn the power off the esp32 will also turn off and you will not have a way to tell the relay to turn the board back on.  I personally use the kasa smart plugs to turn my controllers on and off. https://www.amazon.com/Kasa-Smart-Required-Certified-EP10P4/dp/B091FXLMS8 way less wiring hassle and has a really nice web interface for scheduling. I have mine turn on at dusk and off at 11pm every night.

## Can the USB-C connector be used to power the board?
No, the USB-C connector can only be used for programing the board.  When you plug into the USB-C connector the board will go into bootloader mode.  WLED will not run when the board is in bootloader mode.

## What are the dimensions of the board?
- Version 1: 110mm x 70mm x 30mm
- Version 2: 110mm x 70mm x 25mm

## Where can I get the STL files for the CG1500 / DIN rail mount?
STL files can be found on thingiverse https://www.thingiverse.com/thing:5599003

## I want to make my own mount, what is the hole spacing?
The holes are 3mm x 3mm.  The spacing from outside edge to outside edge is 105mm x 65mm.
![hole spacing](./img/din_rail_holes.png)

## What are the GPIO pin assignment:

| Port | PCB v1 | PCB v2 |
| ---- | ------ | ------ |
| LED1 | GPIO15 | GPIO1 |
| LED2 | GPIO14 | GPIO2 |
| LED3 | GPIO12 | GPIO3 |
| LED4 | GPIO4 | GPIO4 |
| LED5 | GPIO2 | GPIO5 |
| LED6 | GPIO17 | GPIO12 |
| LED7 | GPIO5 | GPIO14 |
| LED8 | GPIO33 | GPIO15 |

## How do I use audio reactive WLED?
- Download and install this image which is built with ethernet and audio reactive: https://github.com/bobko69/8PortLEDDistro/blob/main/files/WLED_0.14.0-b1_ESP32_Ethernet_AudioReactive.bin
- Wire up your microphone.  This example is for an INMP441 and PCB v2.

| INMP441 | 8 Port LED Distro |
| ------- | ----------------- |
| VDD | 3.3v |
| GND | GND |
| SD | GPIO17 |
| L/R | GND |
| WS | GPIO32 |
| SCK | GPIO33 |

- Configure WLED, goto Settings/UserMods, scroll down to the AudioReactive section.
Place a check next to Enabled, Select 'Generic I2s' for type, set I2S SD to 17, Set I2S WS to 32, set I2S SCK to 33, set squelch to 10, set gain to 30, and press the 'Save' button.
![WLED settings](./img/wled_sound_reactive.png)

## Where can I get the gerber files for this project?
Sorry the files are not available.  This is not an open source project.

## How do I compile WLED for this board?
- Follow the PlatformIO compilation guide at [WLED's compilation guide doc](https://kno.wled.ge/advanced/compiling-wled/)
- Open `platformio.ini`
- Make sure that `esp32_eth` is uncommented as `default_envs`
- From here on, you should be able to to build & upload to the board

## How do I update the firmware?

There are a couple of ways to update the firmware on the board.  None of them use the Arduino IDE.

- The easiest way is to connect the board to a computer with the USB-C port and on the computer navigate to [install.wled.me](https://install.wled.me/). Select the version of firmware you want to install and make sure to check 'my board has ethernet'.  Press the Install button and follow the rest of the prompts.

- If you have built or downloaded an image, and if the board is connected to your wifi or ethernet network, from a computer navigate to the WLED page in the board. Click the config button, then click the security and updates button, then click the manual OTA update button.  From here you will be able to select an image file to install.
![WLED update page](./img/WLED_update_page.png)

- The last way is to connect the board to a computer with the USB-C port and use [esptool](https://github.com/espressif/esptool) to flash the new firmware.  It is a command line tool.  Here is an example command we use when we flash the firmware on the boards: 
```
.\esptool-v4.2.1-win64\esptool.exe write_flash 0x10000 ./WLED_0.14.0-b0_ESP32_Ethernet.bin
```
