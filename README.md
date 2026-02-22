# Schematics for Programmable DC-DC Power Supply with I2C Interface

## About

The repository contains a schematic for the Programmable Power Supply.

## Specifications
- Controller: Texas Instruments [BQ25758S](https://www.ti.com/product/BQ25758S)
- Input voltage: 5V (4-6V - hardware power good window)
- Input current: up to 5A (hardware limited)
- Output voltage: programmable by I2C in controller defined range (3.3 - 26V)
- Output current: up to 5A (hardware limited)
- Switching frequency: 250kHz

## Schematics Structure
The device is complex enough for the schematics to be split into several pages, one for each functional block.
- Controller and Power Stage - consists of the BQ25758S controller, the power MOSFETs, and the inductor
- Input Filter and Sensor - a set of input capacitors and the input current sense resistor connected according to 4-point probes (Kelvin) method
- Output Filter and Sensor - the same for output circuit
- Master Switch - an input protection and an electronically controllable power switch
- Digital I/O and Indication - digital interface between controller and I2C host, contains as well a status LED, a power good LED, and an independent voltage regulator for the digital circuit
- Programming - a set of resistors to define controller's operating mode and HW limits for voltage and current
For now the pages contain mainly just network and hierarchical labels.

## Major Networks and Busses
- **`VIN`** - positive input voltage. The master switch page should contain an input connector and protection circuit (fuse, TVS diode) after which the network starts. As well is used to power the digital I/O and indication block
- **`VINP`** - positive input voltage after the master switch itself (goes to the input filter)
- **`EN`** - master switch control signal (should be high to turn the switch on and low to turn it OFF)
- **`VINN`** - output of the input filter
- **`VOUT`** - the output voltages bus (contains power stage output and whole device output networks, goes to the output filter)
- **`CSIN`** - the input current sensor bus (goes to `ACN` and `ACP` pins of the controller)
- **`CSOUT`** - the output current sensor bus (goes to `SRN` and `SRP` pins)
- **`I2C`** - I2C bus itself (connected to `SCL` and `SDA` pins)
- **`GPIO`** - groups digital I/O lines: interrupt, power good, status, and chip enable
- **`PROG`** - groups the rest of analog input lines which should be connected to the programming block to set operating mode and limits for the controller
