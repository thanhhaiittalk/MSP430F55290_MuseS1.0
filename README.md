# Project MuseS - Museum System

# Project abstract 
Developed a device that automatically performs presentations of the artifacts in the museum close to visitors.This device has the ability to scan Beacon attached on artifacts and play an audio file that fits the Beacon ID. 
![Alt text](image/finished.jpg?raw=false)

![Alt text](image/sket.png?raw=false)

## System hardware architecture
    -Microcontroller: MSP430F5529.
    -Audio board: DFplayer Mini.
    -Bluetooth board and Beacon: HM10 BLE.
    -LCD: N5110.
    -Battery: Lithium Ion.

![Alt text](image/image1.png?raw=false)

## System software architecture
    
    Demo/
    | CORTEX_STM32F103_Keil/
    | | Beacon
    | | DFplayer_Mini_mp3
    | | PCD8544 (LCD)
    | | TEST_ONLY.ino (main)
   
 
