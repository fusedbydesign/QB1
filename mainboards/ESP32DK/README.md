# QB1 ESP32 Dev Kit Main Board

The ESP32 Dev Kit Main Board adapts a 30-pin ESP32 dev dev to the QB1. This is the main component required to build a QB1 using an ESP32 dev kit. 

## Printed Circuit Board

The easiest way to get the PCB is to order a batch using this [PCBWay project](https://www.pcbway.com/project/shareproject/QB1_Main_Board_for_ESP32_Development_Kit_a3892956.html). You can also get an assembled board, but the board has been designed to make DIY component sourcing and assembly very easy.  


## Required components

| Count | Description |
|---|---|
| 7 | Female header with 2.54mm spacing, 15-pin |

## Assembly

* Solder 15-pin female header connectors to the locations on indicated for the ESP32 dev kit, and also to any peripheral locations that will be used. Note that connectors for the dev kit go on the bottom of the board, while the connectors for the peripherals go on the top. Use the PCB silk screen as a guide, and only place connectors where the holes are surrounded by a border on the silk screen.  
* Solder additional connectors for power and reset connections, as needed. In many cases, these connectors are unnecessary. These connectors are only necessary if you want to add a poer source or reset switch without using one of the peripheral spots.  

## Enclosure

Print or otherwise obtain the [enclosure bottom](https://makerworld.com/en/models/2543156-qb1-bottom-for-esp32-dev-kit-main-board) to incorporate this main board into a QB1. To complete the enclosure, you will also need a top piece and window pieces/blanks. All QB1 enclosure pieces are available in [this collection](https://makerworld.com/en/collections/23142249-qb1).

## Operation

### Power

Power can be supplied to this board through the USB connector on the development kit, or by a power supply peripheral. When powering by USB, the USB power supply must provide at least 2A for the full power configuration, or 1A for low power configuration. See the [QB1 specification](/spec) for more information about power configurations. 

### Connectors

This main board has four peripheral connectors labeled EB1-5. EB5 is in the center of the board, and it can be used to wire up a peripheral mounted to the top plate. All connectors are wired to different host pins for PIO, except for EB2 and EB5, which share the same host pins for PIO. So peripherals that use (the same) PIO pins cannot operate in EB2 and EB5 at the same time. 

### Pin Mapping

| Pin # | Connector | Host |
|---|---|---|
| 1 | AUX | Not Connected |
| 2 | S | D25 |
| 3 | MOSI | D23 |
| 4 | MISO | D19|
| 5 | CLK | D18 |
| 6 | EN | EN |
| 7 | SCL | D22 |
| 8 | SDA | D21 |
| 9 | 3V3 | 3V3 |
| 10 | GND | GND |
| 11 | VIN | VIN |


| Pin # | Connector | Host EB1 | Host EB2 | Host EB3 | Host EB4 | Host EB5 |
|---|---|---|---|---|---|---|
| 12 | PIO4 | D12 | D4 | D2 | D15 | D4 |
| 13 | PIO3 | D36 | D39 | D34 | D35 | D39 |
| 14 | PIO2 | D27 | D13 | D14 | D33 | D13 |
| 15 | PIO1 | D16 | D17 | D26 | D32 | D17 |
