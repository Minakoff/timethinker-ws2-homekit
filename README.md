This firmware does NOT require anything else in order to work.
You don't need HomeBridge running on a Raspberry-Pi or an MQTT server, since HomeKit runs natively are enough a Wi-Fi connection and an Apple Device.

![](https://github.com/Minakoff/timethinker-ws2-homekit/blob/master/images/socket.jpg)

### History
I bought several Timehinker WS2 devices on Aliexpress. HomeKit support was announced out of the box, but in fact I got a problem - the socket stopped responding in the Home app after one or two days of normal work. At the same time it works well through a native application (that did not suit me). 
Communication with technical support did not affect the situation - they remotely updated the firmware, but this did not help. Having disassembled the device, I found it is based on the ESP8266 chip similar to Sonoff Basic devices, but alternative GPIOs were used for relay, LED and button. Thus, I took the firmware from Gruppio (https://github.com/Gruppio/Sonoff-Homekit) and adapted (in fact, I simply changed the GPIO numbers) to those used by TimeThinker WS2. 
Thus, I am sure that the device has lost the warranty, however, my tests have shown that work has stabilized in HomeKit for many days and finally it has become possible to fully use the device.

### Compatible Devices
This Software is currently tested on: Timethinker WS2

### Web Page Controller
For control your device a non Apple device just navigate to its IP address and a web page will allow you to turn it on or off

### Rest APIs
A full set of Rest APIs are available:
* **/on**
* **/off**
* **/toggle**
* **/state**

All the request are in **GET** and are relative to the IP address of your device.
In order to turn on the switch at IP 192.168.0.22 you can: `$ curl 192.168.0.22/on`

---

## Installation Instructions

![](https://github.com/Minakoff/timethinker-ws2-homekit/blob/master/images/wiring.png)
![](https://github.com/Minakoff/timethinker-ws2-homekit/blob/master/images/wiringbig.png)

### Flash the Timethinker WS using esptool.py:
 1) Unplug your Timethinker WS2 device from the power line _(or you can burn your PC)_
 2) Short IO_0 and GND with a piece of wire as shown
 3) Connect your device to a serial adapter @ 3.3v (GND, RX, TX, +3.3v) as shown
 4) Run the `flash.sh` script 
 
### or flash using ESP8266Flasher (Windows users):
 1) Unplug your Timethinker WS2 device from the power line _(or you can burn your PC)_
 2) Short IO_0 and GND with a piece of wire as shown
 3) Connect your device to a serial adapter @ 3.3v (GND, RX, TX, +3.3v) as shown
 4) Use ESP8266Flasher.exe (rboot.bin @ 0x0; blank_config.bin @ 0x1000; timethinker-ws2.bin @ 0x2000; baudrate 115200; flash size 8MByte; flash speed 40MHz, SPI mode DOUT)
 5) Hit Flash(F) button

### Add device to Home app
 1) Connect your iPhone or iPad to the new wifi network `TimeThinkerWS2-xxx`
 2) Wait for the Captive Portal and select your WiFi network
 3) Insert your WiFi Password
 4) Open the `Home` app
 5) Click the `+` symbol
 6) Click `I don't have the code...`
 7) Select the TimeThinkerWS2-xxx Switch 
 7.1 If the TimeThinkerWS2-xxx does not appear on top of the page try to press the device button a couple of times and kill the Home App
 9) Confirm that you want to add the device
 10) Insert the Password that is `11111111`

Done! 

---

This project would not have existed without:
https://github.com/Gruppio/Sonoff-Homekit
https://github.com/maximkulkin/esp-homekit
https://github.com/maximkulkin/esp-homekit-demo
https://github.com/maximkulkin/esp-wifi-config
