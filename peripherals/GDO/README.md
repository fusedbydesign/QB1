# Garage Door Opener Board for QB1

The Garage Door Opener (GDO) board allows the QB1 to directly interface with Chamberlain/Liftmaster garage door openers that cannot be controlled with dry contacts. 

This peripheral is inspired by the [ratgdo](https://ratcloud.llc), and it is designed to be compatible with [ratgdo firmware](https://paulwieland.github.io/ratgdo/flash.html). If you want to connect your garage door opener to your home automation system, please consider buying a ratgdo board. Some models even include additional components that make it easy to solve additional garage sensing/control problems (car presense, parking distance) with the ratgdo. 

The schematic and technical information used to develop this project is due to the [rat-ratgdo project](https://github.com/Kaldek/rat-ratgdo). 

> [!CAUTION]
>Assembling this peripheral is somewhat challenging because it is necessary to obtain and solder surface mount components. The soldering is possible with a normal soldering iron with a fine tip. Search on YouTube for instructional videos. You will probably also want additional tools such as a vise, a desk-mounted magnifying glass, and tweezers. 

> [!NOTE]
> A detailed BOM, PCBWay project (assembled or PCB only), and 3D-printed face plate are coming soon. 


## Required components

| Count | Description |
|---|---|
| 1 | 3-pin male JST-XH PCB connector, through hole, straight |
| 1 | 2N7002 transistor, surface mount, SOT-23 |
| 2 | AO3400A transistor, surface mount, SOT-23 |
| 3 | 10k Ohm resistor, surface mount, 0805 |
| 1 | 15-pin male header with 2.54mm spacing, angled |
| 1 | (Optional) 2-pin male header with 2.54mm spacing, straight| 
| 1 | (Optional) 2-pin jumper with 2.54mm spacing | 

It is also necessary to obtain a wire to connect the peripheral to the terminals on the garage door opener. The best way to do this is to crimp a female JST-XH connector onto one end of a ribbon or set of wires, and leave the other end bare so the wires can be attached to the terminals on the garage door opener. See the board silk screen to determine the proper connections. 

## Assembly

1. Place and solder the the surface mount components on the front side of the board. 
1. Place and solder the 3-pin JST connector, after selecting the appropriate location. 
  * To allow the peripheral to be installed in a side face of the QB1 (the most common mounting), the connector should placed in the location marked J4 on the back side of the board.
  * The connector can be soldered in other positions, or even left off the board, to support less common methods of mounting the board and connecting to the garage door opener. 
1. Place and solder the 15-pin angled header on the front side of the board. The board may not have silk screen markings to indicate the correct side of the board for the header. It should be placed on the same side as the surface mount components.  
1. (Optional) place and solder the 2-pin male jumper at position J2 on the front of the board. 

The 2-pin male header is used to optionally connect the CTRL signal from the garage door opener to the QB1 AUX line. This optional connection can be made by placing a jumper on the header. The connection allows other peripherals to use the CTRL signal (e.g. to make a power supply).

The peripheral board mounts to the main board in the outside position, which allows the JST-XH connector to sit flush with the window. 


## Operation

The easiest way to use the GDO peripheral is to start with the appropriate [ratgdo firmware](https://paulwieland.github.io/ratgdo/flash.html) and modify the configuration so that the firmware communicates with the GDO using the correct pins. See the silk screen on the peripheral board for the connection between the GDO and QB1 connector. 

The ESPHome ratgdo firmware is available on github, and there is also a convenient [downloader](https://ratgdo.github.io/esphome-ratgdo/). Any firmware that uses the correct host SoC family (e.g. ESP32 for the QB1 ESP32 dev kit main board) should work after the pins are correctly configured. The ESPHome configuration can then be modified to enable additional peripherals on the device.   


