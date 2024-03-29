# VideoWebServer_for_CameraCar
## Introduction
I installed a front view camera in a N-Guage train which can transmit the video image over WiFi. Newly released small ESP32 S3 based module "XIAO ESP32 S3 Sense" made it available in N-Guage train which has has a very limited space to install necessary hardware. 
Users are able to view the front view video image from a running train by Web server which runs on the ESP32 S3 processor over WiFi. The system is powered by a 3.7V battery installed in the car. 
I made two prototypes. In these prototypes, the system was installed in a very common box car which is 98 mm length. The car does not have a motor to run. Thus, the car has to be connected in front of an engine. 

## Hardware
### Base Processor Module
Seeed Studio XIAO ESP32 S3 Sense is used for the base processor module. The module has WiFi, OV2540 Camera Interface, Microphone, Battery input with battery charing circuit, USB interface and micro SD Card interface. OV2540 Camera module comes with the product, but was replaced with a longer cable one. Micro SD card interface or Microphone is not used in the Camera Car use at this moment. 

XIAO ESP32 S3 Sense can be obtained form Amazon.
* https://www.amazon.com/gp/product/B0C69FFVHH/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1

Product introduction by the maker is seen here.
* https://www.seeedstudio.com/XIAO-ESP32S3-Sense-p-5639.html

Please refer the following tutrial page for the general usage of XIAO ESP32S3 Sense Camera.
* https://www.seeedstudio.com/XIAO-ESP32S3-Sense-p-5639.html
* https://github.com/limengdu/SeeedStudio-XIAO-ESP32S3-Sense-camera

### Camera Module
OV2640 camera module with 120 mm wire is used raplacing the OV2640 camera module attached in XIAO ESP32 S3 Sense. It is to install a camera on the front of the box car and XIAO ESP32 S3 Sense module on the other side of car so that USB-C connector is exposed to the back side of the box car.

The OV2640 module I used was obtained from form Amazon here.
* https://www.amazon.com/gp/product/B08XLWLGG6/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1

### Battery
A 3.7V Lithium-Ion battery is used to supply a power to the modules. As XIAO ESP32 S3 Sense hasa charging circuit to the Lithium-Ion battery, it is possible to charge it by USB power input.
A 350 mAh battery can operate the video transmission for about 15 min.

### USB port
USB port with USB-C connector faces to the rear wall of the box car. It is mainly to install a new sketch to the processor, but it can be used to input power to the processor as well as charge the 3.7V battery. 
In future, I want to supply 5V DC power through the USB port from a track power.

## Installation to a Box Car
### Box Car for the installation
The system was installed in a box car with 98mm length x 19mm wide x 31mm height (including wheels) which is commonly sold.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/43e6fed7-295a-48c7-b18c-608b4e93ded8" width="480">

### Wiring
The additioinal wirings made in the system were.
* DC input from 3.7V battery. Wires from battery case soldered to BAT+ and BAT- terinal.
* An external LED connection. Connected to D1 and GND. The LED works as a headlight of the car.

### OV2640 Camera
Camera itself is installed on the front panel of the box car. The flat cables goes to inside of the box car via an open hole. 
The flat calbes is connected to camera module connector of the XIAO ESPS3 Sense.

### WiFi Antenna
The antenna is not embedded to the processor module. The antenna is installed externally via tiny coax cable. 

In prototype 1, I used the antenna that came with XIAO ESP32 S3 Sense. To get the better WiFi connectivity, the antenna was installed on top ot the box car.
I don't recommend to connect and disconnect the coax cable, place and peel off the sheet antenna many times. The WiFi connection will not be stable enough.

In prototype 2, an antenna with higher gain was used and it showed much better WiFi connectivity, and video frame rate was dramatically increased as a result. The antenna used here is "2.4G/5G/5.8G Dual Band Omni PCB Antenna with IPX Connector". I strongly recommend to replace the antenna with higher gain. 

* https://www.amazon.com/dp/B08CR8FTL5?psc=1&ref=ppx_yo2ov_dt_b_product_details

### Install XIAO ESP32 S3 Sense
#### Prototype 1

After the necessqry wired were conencted, XIAO ESP32 Sense module placed at the rear side of the box car. The box car is not enough wide to put the module inside. 
XIAO ESP32 Sense module, a camera module and other components are placed in the frame of the box car.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/a707a0a1-afe6-49d2-8045-bddec181d753" width="640">

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/49879dda-303b-4eda-9baf-38a9fd2318f6" width="480">

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/1cdcb9f6-6c28-4157-b5a7-3e492f90ddd1" width="480">

#### Prototype 2

XIAO ESP32 Sense module, a camera module and other components are placed on the in the bsse of the box car.

1) Make a base board by cutting a universal soldering circuit board.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/9a18d84b-f158-4eea-982b-84dbf32efc0a" width="640">

2) Solder 2.54mm header pins to XIAO ESP32 Sense module to place the module to the base board.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/cf3114ec-80e5-4cbc-9c5f-345a3c95f432" width="640">

3) Solder cables from 3.7V Li-Ion battery + to Bat+, - to Bat-, Solder cable to + of LED. Place XIAO ESP32-S3 Sense module to the base board.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/8ee68db9-af19-4b5e-a295-e358fd308beb" width="640">

4) Place LED for a headlight.
5) Place dummy connector (black in the picture with header pins. OV2640 camera will be placed here later. 

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/0d0f19e4-ccca-4a41-92fa-737d5f196bc4" width="640">

6) Place OV2640 camera module with 120mm cable to dummy connector (it is gray color one in the picture at last.) The flat cable go underneath the gray dummy connector.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/26740ebe-884a-4b28-91fa-952a9b8b4d59" width="540">

7) The flat cable of OV2640 camera module is connected to the camera module interface of XAIO ESP32-S3 Sense.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/191c2c72-bd7e-4b4a-be23-fc850dfcc934" width="640">

8) To place the battery holder, another circuit board was placed on top of the base board using header pins in between.
9) Exteral antenna was placed on the battery holder.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/25f444ef-bea4-4c5b-9ec4-b5934dd6a911" width="640">

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/82c2d08d-4f60-41f0-86e9-ec2e4baa4830" width="480">

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/edfcb256-f47c-4fa8-98bd-e9aaa978e298" width="480">

10) Then, a frame with wrapping is placed over.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/ee989e54-2c66-41c1-a1a3-07f504cd4089" width="640">

11) Here is the frame with wrapping.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/772a7b67-2b2d-4d76-b578-766506fa17b7" width="480">

### External view
#### Prototype 1

Side View
To cover the cut on the side of box car, I made a panel which was made from a beer can, and put it on the side of box car body.

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/ea20210a-1556-4009-b24e-23f3d437de88" width="640">

Front View

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/91616201-11c6-492a-839f-f078b38e25c7" width="480">

Read View

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/153cfbc2-171b-4357-819b-eef7bef053fa" width="480">

#### Prototype 2

Side View

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/fcf5838b-498d-46c8-bbc6-e64daa8c1777" width="640">

Front View

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/83d9c860-b502-4d48-8bbe-c629c4ff793d" width="480">

Rear View

<img src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/fbf9573a-26ea-4dc7-a823-a04f5abd89c1" width="480">


## Software
### Preparation of IDE
First, please install necessary libraries and set-up Arduino IDE following the Software Preparation section of the following tutrial.
* https://wiki.seeedstudio.com/xiao_esp32s3_getting_started/

### Customization to your WiFi network
1. Download sketch
   Download the sketches from the repository here.
   
2. Change WiFi SSID and Password
   
   Change WiFi SSID and Password to the ones in your network.
   
   Two sets of SSID and Password can be configured. They are for the case the camera car is used on own layout or a layout in other place such as model train club.
   The softare switches the SSID automatically from one to another if the connectios is not establishsed in 50 tries.

   If only one SSID configuration is enough, please use same SSID name and passowrd for both.

### Customizing Web Server HTML
HTML code for the Camera Web Server exist as a binary code in index_ov2640_html_gz[] part of camera_html.
The portion is a HEX format of binary code that original HTML after zipped by GZIP. 
The way to get the binary HEx format from text based HTML is introduced in the following site.
* https://robotzero.one/esp32-cam-custom-html/

CytberChef online tool introduced in above site makes the binary file in HEX format.

Then, you need to change index_ov2640_html_gz_len to the newly created HTML. One byte of binary consist of 5 characters of HEX string including commma foe the separator. So, index_ov2640_html_gz_len becomes total string length devided by 5.

index_ov2640_headlight_html.txt in the repository is the original HTML used in my video Camera Car webserver.
I added "Headlight button" on top of the menu.

## Operation
### Basic Operation
The Web Server access uses the video streaming feature by SpeedStudio which is introduced in the tutorial page of XIAO ESP32S3 Sense Camera shown in Base Processor Module section.
The operation is easy. Just access to http://<"IP address"> via an Web Brower and click "Tuen On Video" on the bottom of the menu.
The camera configuration is available through the bottuns and windows in the menue. They are same as the original example VideoWebServer application by SpeedStudio.
One modification is to add Head Light button on top. It turns on/off the head light LED.

<img width="589" alt="20230920_Model_Train1" src="https://github.com/ktomoma/VideoWebServer_for_CameraCar/assets/131932595/fae3b555-38bc-41e5-9519-db3fe6aa2927">

Captured Video Image (Click the video thumbnail below)

The layout itself is still under building.

[![Video on WebServer_for_CameraCar](http://img.youtube.com/vi/2yf1QeSd02I/0.jpg)](https://www.youtube.com/watch?v=2yf1QeSd02I)

### SNMP MIB
The system supports SNMP agent and has following MIB onjects.
The default access password is public for SNMP GET and private for SNMP SET. They are mainly for a trouble shooting in case the video streaming does not come smoothly by checking WiFi signal strength and video frame rate.

OID = .1.3.6.1.4.1.4998.3.1.1.0, ReadWrire, It reports SSID ID which is in use. Also, if setting another value either 0 or 1, switch SSID.

OID = .1.3.6.1.4.1.4998.3.1.2.0, ReadOnly, It reports SSID Name which is in use. 

OID = .1.3.6.1.4.1.4998.3.1.3.0, ReadOnly, It reports WiFi signal stlength. 

OID = .1.3.6.1.4.1.4998.3.1.4.0, ReadOnly, It reports video frame rate in 1000th of the rate. 10000 represents 10 frames per sec.

OID = .1.3.6.1.4.1.4998.3.1.5.0, ReadWrire, It reports the status of head light LED, true (on) or false (off).

OID = .1.3.6.1.4.1.4998.3.1.6.0, ReadWrire, If setting 1, it resets WiFi with same SSID.


Eaxmple output.

~ % snmpwalk -c public -v 2c 192.168.1.38 1.3.6.1.2.1

SNMPv2-MIB::sysDescr.0 = STRING: Video Cam Car 3 - VideoWebServer_for_CameraCar3_v010.ino

DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (2578) 0:00:25.78

SNMPv2-MIB::sysContact.0 = STRING: ktomoma@mac.com

SNMPv2-MIB::sysName.0 = STRING: XIAO ESP32S3 Sense

SNMPv2-MIB::sysLocation.0 = STRING: Warrenville IL, USA

SNMPv2-SMI::enterprises.4998.3.1.1.0 = INTEGER: 0

SNMPv2-SMI::enterprises.4998.3.1.2.0 = STRING: "ssid1"

SNMPv2-SMI::enterprises.4998.3.1.3.0 = INTEGER: -55

SNMPv2-SMI::enterprises.4998.3.1.4.0 = INTEGER: 10416

SNMPv2-SMI::enterprises.4998.3.1.5.0 = INTEGER: 0

SNMPv2-SMI::enterprises.4998.3.1.6.0 = INTEGER: 0


### Serial Console Output
There is serial console output for debugging purpose. If the system is faling to connect WiFi, the serial console output reports the status of WiFi connection.

### Known Issues
MIB for SSID Name (OID = .1.3.6.1.4.1.4998.3.1.2.0) is not updated when SSID is changed by setting another SSID ID in OID = .1.3.6.1.4.1.4998.3.1.1.
