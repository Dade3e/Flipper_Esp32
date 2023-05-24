Original Marauder code
https://github.com/justcallmekoko/ESP32Marauder/releases/tag/v0.10.4

Original Deauth code
https://github.com/SpacehuhnTech/esp8266_deauther/releases/tag/2.6.1

Hi,
I use ***Esp-wroom-32***, and to save pcap on flipper zero sd:
- Software:
  - Update Arduino ide for recompile marauder esp32 firmware: Arduino Ide Version: 2.1.0;
  - And I configure it with this guide: https://github.com/justcallmekoko/ESP32Marauder/wiki/arduino-ide-setup ;
  - In the marauder project (version 0.10.3), in ***config.h***, uncomment ```#define WRITE_PACKETS_SERIAL```;
  - ***uncomment*** ```#define GENERIC_ESP32``` and comment the others;
  - ADD in ```//// SD DEFINITIONS```:
    ```
    #ifdef GENERIC_ESP32
      #define SD_CS 5
    #endif
    ```
  - in ***esp32_marauder.ino***, modify Serial1 with the serial you want to use: ex. Serial2 in my case: 
    ```
    #ifdef WRITE_PACKETS_SERIAL
        // Starts a second serial channel to stream the captured packets
        Serial2.begin(115200);
      #endif
    ```
  - In ***Buffer.cpp*** modify all Serial1.write in ***void Buffer::forceSaveSerial()*** function  with your Serial: Serial2

 - Hardware: I connect: 
     - Esp32 RX0 => pin13/TX Flipper zero, 
     - ESP32 TX0 0> pin14/RX, 
     - RX2 => pin15/C1, 
     - TX2 => pin16/C0,
     - Vin ESP32 pin to 5V Flipper zero pin, to be enabled in the main GPIO section,
     - GND Esp32 pin to GND Flipper zero pin

I think this is all :/
