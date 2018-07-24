Project abstract: This system was developed for using by visitors in museums, heritage sites or exhibitions. The system performs automatically presentations of the artifacts in the museum or the objects in the exhibition close to visitors. The system included a portable device used by visitors and Beacons were attached on objects. The device (we call it eDocent) collects and processes ID, RSSI (Received Signal Strength Indicator) of Beacons nearby; based on that, the device will automatically present for visitors.

System Architecture
Figure 1 represents a block diagram of the total system. From left to right, one can remark the LCD 5110 that is used as display unit. Next, the Microcontroller board is connected to HM10 Bluetooth Board for scanner and a MP3 player board for playing MP3 file and reading SD card. The last is the Beacon node, it’s actually a HM10 board but it was configured as Beacon (sleep mode, non-connectable, Beacon mode on)
Beacon node
iBeacon is a new technology described by Apple Inc. as "a new class of low-powered, low-cost transmitters that can notify nearby devices of their presence". The technology enables a smartphone or other device to perform actions when in close proximity to a Beacon.
One application is an indoor positioning system, which helps devices determine their approximate location or context. Beacon technology works using the Bluetooth Low Energy (BLE) technology, also known as Bluetooth Smart. Beacon uses Bluetooth low energy proximity sensing to transmit a universally unique identifier picked up by a compatible device (like the eDocent). 
In this project, we use HM10 BLE modules as Low-Cost Beacons. The HM-10 is a readily available Bluetooth 4.0 module based on the Texas Instruments CC2540 or CC2541 Bluetooth low energy (BLE) System on Chip (SoC). When configured as Beacon, the HM-10 draws an average of about 0.18 mA. The battery pack shown has a capacity of about 1800 mAh which would last 10,000 hours, or more than a year.

Figure 2: HM10 BLE Module
Beacon nodes doesn’t save any data except a universally unique identifier, eDocent read this ID and perform actions. Based on the RSSI value of the Beacon node, it is possible to create a "virtual fence", so that when the visitor in close to the artifact at a certain distance (about 4-7m), it will allow for doing actions.

Chart 2: Measurement RSSI result
Microcontroller
We choose the m430f5529 from Texas Instruments, the ultra-low-power microcontroller. The TI msp430 family of ultra-low-power microcontrollers consists of several devices featuring peripheral sets targeted for a variety of applications. The architecture, combined with extensive low-power modes, is optimized to achieve extended battery life in portable measurement applications. The msp430f5529 is not a high performance chip yet but still meets of the project, it is very suitable for portable device like the eDocent.
Some important Parametrics:
CPU: MSP430
Frequency (MHz): 25
Non-volatile Memory (KB): 128
RAM (KB): 10
SPI: 4
UART: 2
Active Power (uA/MHz): 404   
Standby Power (LPM3-uA): 2.5
But the MSP430F5529 chip just ran at 25MHz, it’s still good for our algorithm applied as well as stable control the HM10 module and MP3 board.  
For programming, we use Code Composer Studio. Code Composer Studio is an integrated development environment (IDE) that supports TI's Microcontroller and Embedded Processors portfolio. Code Composer Studio comprises a suite of tools used to develop and debug embedded applications. It includes an optimizing C/C++ compiler, source code editor, project build environment, debugger, profiler, and many other features.

3: Code Composer Studio interface


Figure 4: Chip MSP430F5529
1. HM10 – BLE module
On the scanning function, we use the HM 10 module which is configured in master mode. HM10 communicate with the microcontroller through UART, HM10 is easy to program, firmware of HM10 also support AT command. When the microcontroller request HM10 scan Beacon (send “AT+DISI?” through UART), it will receive a string include ID and RSSI.

Figure 6: Received string after requesting scan
Ex: OK+DISISOK+DISC:4C000215:74278BDAB64445208F0C720EAF059935:00010004C5:D43639DAF7E3:-056OK+DISCE
This string includes:
 OK+DISI: Begin scan.
 OK+DISC: Detect a beacon
4C000215:74278BDAB64445208F0C720EAF059935:00010004C5:D43639DAF7E3 : ID string, this ID includes small parts:
4C000215: FAC ID (8 characters)
74278BDAB64445208F0C720EAF059935: Beacon ID (32 characters)
0001: Major ID (4 characters - Major ID was configured by developer)
0004: Minor ID (4 characters - Minor ID was configured by developer)
D43639DAF7E3: MAC ID (12 characters)
-056: RSSI value
OK+DISCE: end of  scanning session.
All Beacons in the gallery that has the general content have the same Major ID and each beacons has a specific Minor ID. Base on Major ID and Minor ID, the eDocent can introduce visitor to both general and specific content of each object. The eDocent uses MAC ID in cases of objects have separate content; in this case, each Beacon has an unique MAC ID.


Figure 7: Module HM10 (SMD)
1. LCD and MP3 board
The DFPlayer Mini is designed to be very compact and suitable for use on portable devices. It also comes with an SD card slot supporting up to 32GB. All media data is stored in this SD card.
The LCD N5110 uses the SPI interface with the microcontroller, LCD help visitors to know some basic information such as the name of the object, the language and the notification.
 
4. The Circuit
After testing and programming as well as selecting the appropriate hardware, we begin design circuit, use Proteus software to design the schematic as well as drawing PCB to do the circuit. Experimenting with 5 versions, the circuit is also stable.

Figure 11: The Schematic

Figure 412: The PCB layout
5. The Design
The team uses 3D printing technology to create a product exterior. Inspired by the cassette tape and the 4-button gamepad associated with childhood, the design of the product is a mix of modern and nostalgic, with the spirit of the museum, when history is brought back the present. 

Figure 10: 3D model was designed on SketechUp
                                                     
Figure 11: Finished Product
