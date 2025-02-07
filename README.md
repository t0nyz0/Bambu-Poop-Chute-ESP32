# Bambu Poop Conveyor for ESP32 
:arrow_right:	:arrow_right:	:poop: :arrow_right: :arrow_right: :poop: :arrow_right: :arrow_right:

### For more detailed project information visit: https://t0nyz.com/projects/bambuconveyor

## Overview 

The Bambu Conveyor is an application designed to manage the waste output of a [Bambu Labs printer](https://bambulab.com/en/x1). It utilizes the MQTT protocol to monitor the printer's status and control a motor that moves waste material away from the printing area. Supports X1, currently testing A1 and P1 compatibility. See settings menu.


## List of some supplies
- Breakout board for ESP32: https://amzn.to/4dyjsx0
- ESP32 board: https://amzn.to/4fBjh5L
- 12 Volt power supply: https://amzn.to/3AfIm6a
- Motor Controller: https://amzn.to/3yBPqcM
- 12V 10RPM Motor: https://amzn.to/3M24VOd
- Resistors (I use 1k Ohm): https://amzn.to/4cqCi8e
- Wires: https://amzn.to/46EAtn3
- LEDs sourced from this kit: https://amzn.to/4dH5Dw7
  

# Conveyor Makerworld files

- **Conveyor:** https://makerworld.com/en/models/148083#profileId-161573
- **ESP32 Housing:** https://makerworld.com/en/models/1071359#profileId-1061316
- **Conveyor Extension:** https://makerworld.com/en/models/249714#profileId-359905


## Features

- **WiFi and MQTT Connectivity:** Connects to a local WiFi network and communicates with the printer via MQTT
- **Motor Control:** Activates a motor to manage the printer's waste output based on the printer's status
- **Web Server:** Hosts a web server to provide manual control and configuration of the system
- **Stage Monitoring:** Monitors various stages of the printer to determine when to activate the motor

# Bambu Poop Conveyor - Setup & Installation Guide  

## Setup  

## Flashing the ESP32

To install the firmware, use an ESP32 flashing tool.

1. Download the latest `.bin` release from [GitHub Releases](#).
2. Connect your ESP32 to your computer via USB.
3. Use `ESP-Flasher` or `esptool.py` to flash the firmware.

 **Note:** The port (`/dev/cu.usbserial-0001`) in the command below may be different on your system.  
 Use `ls /dev/cu.*` on macOS or `COMx` on Windows to find the correct port.
   
```cp
esptool.py --chip esp32 --port /dev/cu.usbserial-0001 --baud 115200 write_flash 0x1000 Bambu-Poop-Conveyor-v1.3.0.bin
```

5. Wait for the flashing process to complete.
6. Restart the ESP32.


## Configuring via Web Interface

Once flashed, the ESP32 starts in AP Mode:

1. Connect to the **"BambuConveyor"** WiFi network.
2. Open a browser and go to **[192.168.4.1/config](http://192.168.4.1/config)**.
3. Enter your WiFi and MQTT credentials.
4. Click **Save**. The ESP32 will reboot and connect to your WiFi.

For troubleshooting, open an issue on GitHub or check the discussions tab.


## Usage

### Web Server

The application hosts a web server to provide manual control and configuration. Access the following URLs for different functionalities:

- **Root URL:** Opens Configuration page (`/`)
- **Control URL:** Manual motor control page (`/control`)
- **Config URL:** Configuration page to update settings (`/config`) 
- **Logs URL:** Log history page (`/logs`)
- **Manual Run URL:** Opening this URL runs the motor manually (`/run`)

### FAQ / Troubleshooting

*What do the flashing lights mean when its first turned on?*
- Flashing yellow only = Connecting to WiFi
- Solid Green = We are connected to Wifi and MQTT printer
- Red Light on bootup = No Wifi / No MQTT (Solid red also when conveyor is running)
- Green light / Yellow flashing = Wifi connected / Attempting to connect to printer
- Green light / Yellow solid = Wifi conncted / Issue connecting to printer via MQTT / Will reattempt connection after 5 seconds

*The ESP32 doesnt connect to the printer*
- Double check that your printer is setup with Access Code and LAN only mode is **OFF** [See Bambu Wiki](https://wiki.bambulab.com/en/knowledge-sharing/enable-lan-mode)
- Double check your SN matches the settings you put in
- Make sure your printer has good Wifi signal
- Make sure the ESP32 has good Wifi signal
- Reach out to me if you still have issues


## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

For more detailed project information visit: https://t0nyz.com/projects/bambuconveyor
