# QB1 Specification

The QB1 specification governs the physical and electrical characteristics of QB1 and its peripherals. The specification ensures that compliant peripherals will fit in the enclosure and will not interfere with other peripherals. 

## Electrical Specification

### Peripheral Connector Pins

The 15-pin peripheral connector has the following pin connections:

| Pin # | Name | Description |
|---|---|---|
| 1 | AUX | Auxiliary connection shared between all peripherals, not connected to ESP32 |
| 2 | S | Shared connection between all peripherals and connected to ESP32 |
| 3 | MOSI | SPI MOSI |
| 4 | MISO | SPI MISO |
| 5 | CLK | SPI CLK |
| 6 | EN | ESP32 enable pin which allows the peripheral to reset the ESP32 |
| 7 | SCL | I2C SCL |
| 8 | SDA | I2C SDA |
| 9 | 3V3 | 3.3V power|
| 10 | GND | Ground |
| 11 | VIN | 5V power|
| 12 | PIO4 | Peripheral I/O 4 |
| 13 | PIO3 | Peripheral I/O 3 |
| 14 | PIO2 | Peripheral I/O 2 |
| 15 | PIO1 | Peripheral I/O 1 |

The mapping between these pins and ESP32 pins is not part of the spec, and is specific to each main board implementation. This mapping can be found in the main board documentation. 

#### AUX

The AUX pin is intended to carry power/signals between all peripherals without using the host. For example, it could carry an analog signal or higher voltage/current power. The use of this pin is not governed by the spec. 

#### S

The S pin carry a signal that is shared between all peripherals and the host. The use of this pin is not governed by the spec.

#### SPI Pins

The MOSI, MISO, and CLK pins are used to construct a SPI bus controlled by the host. The slave select (SS) should be implemented using a PIO pin, so it will be different for each peripheral. A spec-compliant peripheral should only use the MOSI, MISO and CLK pins as a full duplex, single-width SPI bus.  

#### I2C Pins

The SCL and SDA pins are used to construct an I2C bus controlled by the host.  A spec-compliant peripheral should only use these pins as an I2C bus. The spec does not govern how addresses are assigned, and peripherals should support address changes to allow multiple peripherals of the same type to be attached at the same time. 

#### Power Pins

The 3V3 pin provides 3.3V during operation. The VIN pin may provide 5V, or it may be unconnected, depending on the configuration. The user must ensure that only one power supply is connected to either VIN or 3V3, originating from the main board or a peripheral. When 5V is supplied to VIN, the main board will produce 3.3V and supply it to the 3V3 pin.  

#### PIO Pins

The peripheral I/O (PIO) pins are used to make a separate connection between the host and each peripheral in a standardized way. For example, two peripherals can be installed that both use PIO1 and PIO2 to communicate directly with the host. These pins will be mapped to different host pins for each peripheral location. 

The PIO pins have the following features and allowed uses:

| PIO # | Input to host | Output from host | Internal pull-up | Analog input to host | Capacitive touch input to host | 
|:---:|:---:|:---:|:---:|:---:|:---:|
| PIO 1 | X | X | X |   |   |
| PIO 2 | X | X | X | X | X |
| PIO 3 | X |   |   |   |   |
| PIO 4 | (1) | X | (1) | (1) | (1) |

1. PIO 4 supports input to the host with pull-up, analog, and touch, but it may also be connected to strapping pins on the host, requiring it to be in a high-impedance state during host boot. This pin shall only be used as an input to the host after the host has booted. 
 

### Power

The specification allows two power configurations:
* In the full power configuration, power is supplied to both the 5V and 3.3V volt rails. All spec-compliant peripherals can be used in this configuration.
* In the low power configuration, power is only fully supplied to the 3.3V rail. This configuration should be used when the device is powered by a battery, or otherwise has power limitations. Peripherals should work in low power mode, if possible, but this mode will not support peripherals that require 5V. A low power device may supply power to the 5V rail, but attached peripherals must not draw power from this rail.  

#### Supply

A compliant power source should supply one of the following to the QB1 main board:
* 5V at 2A (full power)
* 3.3V at 1A (low power)

#### Draw

A compliant peripheral should draw at most:
* 5V at 200mA
* 3.3V at 100mA

A single peripheral may draw from both power rails simultaneously. In order to support the low power configuration, a peripheral should not draw power from the 5V rail. 

If a peripheral requires more power than allowed by the spec, it should power itself and also act as a power supply to the QB1. For example, the peripheral could accept 5V at 3A, use 1A for its purposes, and provide the remaining 2A to the QB1 via VIN. The power supply could also send power to other peripherals using AUX, but the use of AUX for this purpose is outside of the spec. 

## Physical Specification

The physical specification is a set of dimensions that affect peripheral fit.

| Dimension | Value | Notes| 
|---|---|---|
| A | 3.8 mm | Distance from peripheral board to window plate when board is mounted in the outside position |
| B | 12.5 mm | Distance from peripheral board to window plate when board is mounted in the inside position | 
| C | 2 mm | Window plate thickness |
| D | 50 mm | Usable window height and width |
| E | 34 mm | Usable window height above main board connector |
| F | 62 mm | Maximum peripheral board width |
| G | 38 mm | Maximum distance from top of main board connector to top of peripheral board |
| H | 6 mm  | Maximum distance from top of main board connector to bottom of peripheral board |
| I | 2.4mm | Maximum peripheral board thickness |

Additional notes:
* When a peripheral board is mounted in the inside position, it may interfere with adjacent boards if it is wider than 40mm. 
* A peripheral board mounted in the inside position of the top plate may interfere with boards mounted in side plates that are taller than 28mm from the top of the main board connector. 
* A peripheral board mounted in the outside position of the top plate may interfere with boards mounted in side plates that are taller than 36mm from the top of the main board connector. 
* Dimensions related to peripheral boards assume a board thickness of 1.6 mm. For thinner/thicker boards, adjust dimensions accordingly. 
* The spec does not govern the use of space behind the peripheral board. For best results, peripherals should use space toward the center of the usable window area, and provide options that help prevent interference with nearby peripherals (e.g. multiple face plates that place the peripheral in slightly different positions).