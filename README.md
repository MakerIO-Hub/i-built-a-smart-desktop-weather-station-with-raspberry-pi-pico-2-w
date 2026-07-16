# I Built a Smart Desktop Weather Station with Raspberry Pi Pico 2 W! 

SmartStation Pi Setup Guide

This guide is prepared with the Waveshare display shield design in mind, which plugs directly onto the Raspberry Pi Pico. Since the MicroSD card slot on the display module uses the **GP22** pin, the DHT11 sensor has been assigned to the **GP26** pin to prevent any potential pin conflicts.

## 1\. Required Hardware Components

- **1 x Raspberry Pi Pico W** (Wireless-enabled version)
- **1 x Waveshare 2.8inch ResTouch LCD Shield** (320x240 for Pico, SPI, integrated ST7789)
- **1 x DHT11 Temperature and Humidity Sensor**
- **1 x Passive Buzzer** (Two-pin, PWM compatible)
- **2 x Tactile Push Buttons** (For menu control)
- **1 x Breadboard** and jumper wires
- **1 x 5V 1A USB Power Adapter** and Micro-USB cable
- **2 x 10k Ohm Resistors**

## 2\. Hardware Assembly and Pin Wiring Diagram

The Waveshare 2.8" LCD display plugs directly onto the Pico; no extra wiring is required for the screen. You will need to place the other external components (sensor, buzzer, and buttons) on the breadboard and connect them to the male pin headers on the sides of the Waveshare board using jumper wires.

### Physical Pin Mapping Table

| **External Component** | **Component Pin** | **Pico W GPIO Number** | **Pico Physical Pin No** | **Connection Purpose**           |
| ---------------------- | ----------------- | ---------------------- | ------------------------ | -------------------------------- |
| **DHT11 Sensor**       | VCC               | 3.3V (or 5V)           | Pin 36                   | Power supply                     |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **DHT11 Sensor**       | GND               | GND                    | Pin 38                   | Ground                           |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **DHT11 Sensor**       | DATA / OUT        | GP22                   | Pin29                    | Temperature & Humidity Data Read |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **Passive Buzzer**     | (+) Signal Pin    | GP28                   | Pin 34                   | Volume and Audio Control Signal  |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **Passive Buzzer**     | (-) Ground Pin    | GND                    | Any GND pin              | Ground                           |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **Left Button (B1)**   | Pin 1             | GP2                    | Pin 4                    | Value Change / Page Navigation   |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **Left Button (B1)**   | Pin 2             | GND                    | Any GND pin              | Ground                           |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **Right Button (B2)**  | Pin 1             | GP3                    | Pin 5                    | Confirm / Quick Alarm Toggle     |
| ---                    | ---               | ---                    | ---                      | ---                              |
| **Right Button (B2)**  | Pin 2             | GND                    | Any GND pin              | Ground                           |
| ---                    | ---               | ---                    | ---                      | ---                              |

**Important Assembly Note:** When mounting the Raspberry Pi Pico onto the female socket of the Waveshare display board, ensure that the direction of the Pico's USB port matches the USB alignment markings on the Waveshare board (usually on the side of the SD card slot). The Pico must not be plugged in backwards.

## 3\. Software Setup Steps

### Step 1: Flashing MicroPython Firmware to Pico W

- Install the **Thonny IDE** on your computer.
- While holding down the white **BOOTSEL** button on the Pico W, plug the Micro-USB cable into your computer. Your computer will detect the Pico as an external USB storage drive (RPI-RP2).
- Download the latest .uf2 firmware file for the Pico W from the official MicroPython website.
- Drag and drop the downloaded .uf2 file onto the Pico drive. Once the copy process finishes, the device will restart automatically.

**Note:** The SmartStation Pi V1.zip file on GitHub contains a compatible UF2 file named PI_PICO_W-20251209-v1.27.0.uf2.

### Step 2: Creating and Uploading the config.py File

- Open the Thonny IDE. Make sure that **MicroPython (Raspberry Pi Pico)** is selected as the interpreter in the bottom-right corner.
- Open a new file in Thonny and paste the following configuration code:

\# config.py

WIFI_ADI = "YOUR_WIFI_NAME" # wifi_name

WIFI_SIFRESI = "YOUR_WIFI_PASSWORD" # wifi_password

SEHIR = "Izmir" # city

API_KEY = "YOUR_OPENWEATHER_API_KEY" # api_key

SAAT_DILIMI = 3 # time_zone

VARSAYILAN_ALARM_SAAT = 7 # default_alarm_hour

VARSAYILAN_ALARM_DAKIKA = 30 # default_alarm_minute

VARSAYILAN_SES_SEVIYESI = 3 # default_volume_level

- Customize the fields with your credentials, click **Save As**, select **Raspberry Pi Pico** as the target, and save the file as config.py.

### Step 3: Uploading the main.py File

- Open another blank page in Thonny.
- Copy the complete code of the updated, conflict-free, and stable main.py and paste it into this page. _(Ensure the page is entirely blank beforehand so no old code remnants remain)._
- Click the save button, select **Raspberry Pi Pico** as the destination, and save the file as main.py.

## 4\. Initial Run and Testing

- Once the setup is complete, restart the device by unplugging and replugging the USB cable, or simply press the **Run (F5)** button in Thonny.
- The screen will first display a startup screen featuring the "**SMARTSTATION PI**" logo in golden-yellow tones and "**DEVELOPED BY HTEKIN.COM**" in white.
- The bottom line of the screen will show CONNECTING WI-FI... followed by WI-FI CONNECTED. The device will then fetch the current time from the network and load the analog clock interface.
