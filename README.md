# 8 Port LED Distro
![8 Port LED Distro Version 1](./8_Port_LED_Distro_V1_sm.jpg)

This document will serve as a place to answer questions about the 8 Port LED Distro.

## What is it?
This is an 8 port ESP32 based LED distro board running WLED. Distributing both power and data in 1 board. The WT32-ETH01 provides support for Wi-Fi or ethernet connections. It can be used with either 5v or 12v or 24v LED pixels. Also includes a USB-C port for easy programming.

## Where can I get one?
You can purchase the 8 Port LED Distro in our [Tindie store](https://www.tindie.com/products/27884/).

## How can i hook up a relay?
On the board by the usb-c connector there is a header labeled H1 with 5V, IO32 and GND. IO32 can be used as an output to control an external relay. I would follow this tutorial https://esp32io.com/tutorials/esp32-relay and connect 5V for DC+, GND to DC-, and IO32 to IN. You will have to do some configuration in WLED to tell it what port the relay is on.

## Can a realy be used to turn the board on and off?
No a relay can not be used to turn the board on and off.  There is only 1 input power source for the board if you use a realy to turn the power off the esp32 will also turn off and you will not have a way to tell the relay to turn the board back on.  I personally use the kasa smart plugs to turn my controllers on and off. https://www.amazon.com/Kasa-Smart-Required-Certified-EP10P4/dp/B091FXLMS8 way less wiring hassle and has a really nice web interface for scheduling. I have mine turn on at dusk and off at 11pm every night.

## Where can I get the gerber files for this project?
Sorry, but this is not currently an open source project.
