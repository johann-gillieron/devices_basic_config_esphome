# Devices basic configuration for esphome
This is the basics configurations I use for some devices on ESPHome, to connect multiple sensors and dashboard to Home Assistant more easily without having to copy all the settings every time.

## Prerequisites
In order to be able to use the configuration, you need to have a Home Assistant with the plugin ESPHome installed (see: [Getting Started with ESPHome and Home Assistant](https://esphome.io/guides/getting_started_hassio)) <br>
If you follow the tutorial, at the end: the WiFi credentials is writed in the file called "secrets", you need to add these two definitions in the file:
 - ota_password: "Your-Ota-Password"
 - default_ap_password: "Your-default-AP-Password"

## Screens
For all the screens, you can use LVGL (Light and Versatile Graphics Library) to construct your own interface (see: [LVGL Graphics)](https://esphome.io/components/lvgl/)). <br>
The example provided show a simple layout with just "Hello World!" displayed on the center of the screen.

### ESP32-3248S035C 
Specifications:
- Size: 3.5inch
- Resolution : 320x480px
- Touchscreen : capacitive
- Vendor: aliexpress [3.5 Inch 320*480 Smart Display for Arduino](https://www.aliexpress.com/item/1005005099586799.html?spm=a2g0o.order_list.order_list_main.573.680b1802NdgzE3)

The configuration file is for a display on landscape mode.

You need to add on your "secret" file in ESPHome this definition:
 - api_encryption_key_ESP32_3248S035C_example: "The-encryption-Key-generate-by-ESPHome-for-the-device"

### ESP32 JC2432W328C
Specifications:
- Size: 2.8inch
- Resolution : 240x320px
- Touchscreen : capacitive
- Vendor: aliexpress [Guition ESP32 4M FLASH 2.8-inch](https://www.aliexpress.com/item/1005006732002132.html?spm=a2g0o.order_list.order_list_main.11.680b1802NdgzE3)

The configuration file is for a display on landscape mode.

You need to add on your "secret" file in ESPHome this definition:
 - api_encryption_key_JC2432W328C_example: "The-encryption-Key-generate-by-ESPHome-for-the-device"

### ESP32-8048S050
Specifications:
- Size: 5inch
- Resolution : 800x480px
- Touchscreen : capacitive
- Vendor: aliexpress [ESP32-S3 HMI 8M PSRAM 16M Flash Arduino](https://www.aliexpress.com/item/1005006625220768.html?spm=a2g0o.order_list.order_list_main.22.680b1802NdgzE3)

The configuration file is for a display on landscape mode.

You need to add on your "secret" file in ESPHome this definition:
 - api_encryption_key_ESP32_8048S050_example: "The-encryption-Key-generate-by-ESPHome-for-the-device"

 ## Smart socket
 ### myStrom Switch Zero
Specifications:
- Communication: WiFi 2.4 Ghz
- Maximum power : 2000W
- Power consumption measurement : none
- Vendor: Digitec [myStrom Switch Zero](https://www.digitec.ch/fr/s1/product/mystrom-switch-zero-prise-intelligente-23109396)
- Production: **End of life**

**⚠️ WARNING⚠️**<br>
**Flashing the device with a custom firmware means will *<u>NO LONGER</u>* be able to use the manufacturer apps and cloud and the warranty void. Be absolutely sure that you are never going to use them again!**

To flash the socket with a custom firmawre you need first to dismantle the plug to have access to the MCU and next you need to use a FTDI (Usb to serial converter) to make the first flashing of the plug:<br>
*(The tutorial is coming soon)*

The example works as it is because the functionalities of this smart plug are limited to a relay for powered up or down a devices.

 ### Hombli smart socket swiss
Specifications:
- Communication: WiFi 2.4 Ghz
- Maximum power : 2500W
- Power consumption measurement : current, voltage, power and energy
- Vendor: Digitec [Hombli Smart Swiss Socket](https://www.digitec.ch/fr/s1/product/hombli-smart-swiss-socket-prise-intelligente-14374534)

**⚠️ WARNING⚠️**<br>
**Flashing the device with a custom firmware means will *<u>NO LONGER</u>* be able to use the manufacturer apps and cloud and the warranty void. Be absolutely sure that you are never going to use them again!**

To flash the socket, no need to dismantle the socket, you need to follow [this tutorial](https://digiblur.com/2023/08/19/updated-tuya-cloudcutter-with-esphome-bk7231-how-to-guide/) to cute the access to Tuya cloud.

**⚠️ WARNING⚠️<br>Calibration involves working with electrical systems. If you are not experienced or qualified to handle electrical components, *<u>do not attempt this procedure</u>*. Improper handling may result in electric shock, equipment damage, or inaccurate sensor readings.**

After flashing the device, you need to calibrate the sensors for the power measurement using [this tutorial at the end of the page](https://esphome.io/components/sensor/hlw8012.html). <br>
To make the process as easy as possible, the settings are all available on the example file:
- voltage_divider: "voltage_divider factor"
- current_resistor: "current_resistor factor"
- current_multiply: "current_multiply factor"
- update_interval_time: "the time you want to refresh value"