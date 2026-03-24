# HC-SR04 Distance Sensor Peripheral Board for QB1

The HC-SR04 is a low-cost ultrasonic distance sensor with sub-centimeter precision and a maximum range of 4 meters. Unfortunately, it needs to operate at 5V for best performance, and its output must be converted to 3.3V in order to interface with the ESP32 without damaging it. This board provides a safe, reliable 5v/3.3V interface between the ESP32 and an HC-SR04. The board also provides a physical mounting surface for the HC-SR04, and a second level converter that can be used to connect another HC-SR04 that is mounted elsewhere. 

> [!TIP]
> There are other distance sensors that can interface more easily with the QB1 without level conversion. There are also HC-SR04P modules that can be powered using 3.3v, but the maximum range will be slightly reduced. Be prepared to test multiple distance sensors to find the ones that work best for your application.

## Printed Circuit Board

The easiest way to get the PCB is to order a batch using this [PCBWay project](https://www.pcbway.com/project/shareproject/QB1_peripheral_board_for_HC_SR04_distance_sensor_22c7cf84.html). Due to the options for mounting the sensor module, and the unusual way the module is mounted in some options, DIY assembly is highly recommended. Assembly only requires a few through hole components and some basic soldering skills. 

## Required components

| Count | Description |
|---|---|
| 1 | [HC-SR04 module](https://amzn.to/4rNMYFK)|
| 1 | 15 pin male header, 2.54mm pin spacing, angled |
| 2 | 100k Ohm resistor, through hole, axial |
| 2 | 51k Ohm resistor, through hole, axial |
| 4 | Single pin male header, straight |
| 1 | (Optional) 4-pin male header, 2.54mm spacing, angled | 

Component notes:
* For the angled header, you can use commonly-available [breakaway header](https://amzn.to/4sulC8Q) and break it to the correct size. Ensure the header has a short post (the straight part---approximately 3mm long) and a longer tail (the bent part---approximately 6mm long after the bend). The post of the header is soldered to the board and the connector sits 4-5mm off the board. These dimensions ensure a proper fit using the face plate for this connector. Other connectors may be used by modifying the face plate.
* Any [resistors](https://amzn.to/4bEVNeX) with 5% or smaller tolerance and at least 1/4 watt power capacity will work. You can modify the resistance to match the resistor values you have available, as long as the ratio remains approximately 1:2. For example, a 47k Ohm reistor can be used instead of 51k. Increasing the resistance (while maintaining a ratio of 1:2) is not recommended, but the values can be lowered to a minimum of 1k/2k, if desired. The value of 51k/100k was chosen to give acceptable performance in most environments while minimizing power draw. If the sensor will be used in an environment with a large amount of electromagnetic interference, then lower resistance values may give more reliable performance, at the expense of slightly more power draw.

## Assembly

The board supports two different orientations for the HC-SR04:
* Straight mount so that the HC-SR04 and board occupy a single cube face. This is the most common orientation.
* Edge mount so the board can be mounted in one of the side faces and the HC-SR04 points in the direction of the top face. This orientation allows the HC-SR04 to point in the direction of the top face, without the complications associated with mounting the board on the top face. 

Take note of the order in which the components must be placed and soldered---the HC-SR04 covers some of the other components, so it must be placed last. To assemble:

1. Place and solder the resistors as shown in the silk screen on the back of the board, and the 15-pin header on the front of the board.  
1. If the second interface will be used to connect a second HC-SR04 to the QB1, place and solder the 4-pin angled header.
1. Attach the HC-SR04 module and related components
  * For straight mount, start by placing and soldering the single pin headers on the front side of the board, as shown in the silk screen. These headers are not connected, and are only used for structural support. Next, bend the pins on the HC-SR04 module to make them straight, then place the HC-SR04 module, ensuring the pins on the single headers extend through the mounting holes at the corners of the module. With the module seated flush against the base of the headers, solder the module pins to the board. Finally, cut the excess pin length from the module pins and single pin headers using wire cutters. 
  * For edge mount, place and solder the HC-SR04 module in the U2 position on the back of the board, with the sensor pointing away from the board. Cut the excess pin length from the HC-SR04 connector.
  
The peripheral board mounts to the main board in the inside position, in order to accommodate the depth of the sensor module. 

## Enclosure 

Print or otherwise obtain the [face plate](https://makerworld.com/en/models/2567128-qb1-face-plate-for-hc-sr04-peripheral-board) to incorporate this peripheral board into a QB1. To complete the enclosure, you will also need other pieces from [this collection](https://makerworld.com/en/collections/23142249-qb1).

## Operation

For the HC-SR04 mounted to the peripheral board, the trigger pin is connected to TRIG1, and and the echo pin is connected to ECHO1. For the optional external HC-SR04, these signals are TRIG2 and ECHO2. See the silk screen on the board for the connection between these signals and QB1 peripheral pins. 

See the [ESPHome](https://esphome.io/components/sensor/ultrasonic/) page on ultrasonic distance sensors for more information about the HC-SR04 and how to use it with ESPHome. 
