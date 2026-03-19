# HC-SR04 Distance Sensor Board for QB1

The HC-SR04 is a low-cost ultrasonic distance sensor with sub-centimeter precision and a maximum range of 4 meters. Unfortunately, it needs to operate at 5V for best performance, and its output must be converted to 3.3V in order to interface with the ESP32 without damaging it. This board provides a safe, reliable 5v/3.3V interface between the ESP32 and an HC-SR04. The board also provides a physical mounting surface for the HC-SR04, and a second level converter that can be used to connect another HC-SR04 that is mounted elsewhere. 

## Required components

| Count | Description |
|---|---|
| 1 | HC-SR04 module|
| 1 | 15 pin male header, 2.54mm pin spacing, angled |
| 2 | 100k Ohm resistor, through hole, axial |
| 2 | 51k Ohm resistor, through hole, axial |
| 4 | Single pin male header, straight |
| 1 | (Optional) 4-pin male header, 2.54mm spacing, angled | 

## Assembly

The board supports two different orientations for the HC-SR04:
* Straight mount so that the HC-SR04 and board occupy a single cube face. This is the most common orientation.
* Edge mount so the board can be mounted in one of the side faces and the HC-SR04 points in the direction of the top face. This orientation allows the HC-SR04 to point in the direction of the top face, without the complications associated with mounting the board on the top face. 

Take note of the order in which the components must be placed and soldered---the HC-SR04 covers some of the other components, so it must be placed last. To assemble:

1. Place and solder the resistors as shown in the silk screen on the back of the board, and the 15-pin header on the front of the board.  
1. If the second interface will be used to connect a second HC-SR04 to the QB1, place and solder the 4-pin angled header.
1. Attach the HC-SR04 and related components
  * For straight mount, start by placing and soldering the single pin headers on the front side of the board, as shown in the silk screen. These headers are not connected, and are only used for structural support. Using wire cutters, cut the header pins so that only 3-4mm extends above the plastic part. Next, place and solder the HC-SR04 in the U1 position on the same side of the board, with the sensor pointing toward the nearest edge of the board. Bend the HC-SR04 back toward the board so that the single-pin header pins go through the holes in the HC-SR04 module board, and the HC-SR04 module board rests against the plastic part of the headers. Cut the excess pin length from the HC-SR04 connector.
  * For edge mount, place and solder the HC-SR04 module in the U2 position on the back of the board, with the sensor pointing away from the board. Cut the excess pin length from the HC-SR04 connector.
  
The peripheral board mounts to the main board in the inside position, in order to accommodate the depth of the sensor module. 

## Operation

For the HC-SR04 mounted to the peripheral board, the trigger pin is connected to TRIG1, and and the echo pin is connected to ECHO1. For the optional external HC-SR04, these signals are TRIG2 and ECHO2. See the silk screen on the board for the connection between these signals and QB1 peripheral pins. 

See the [ESPHome](https://esphome.io/components/sensor/ultrasonic/) page on ultrasonic distance sensors for more information about the HC-SR04 and how to use it with ESPHome. 
