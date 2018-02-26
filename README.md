# AA-NODE
AA Node

Software examples and bootloader for the arduino compatible AA Node 

https://alex2475.wixsite.com/helix-technology

# Arduino Pinout

RST - Reset on ICSP and DTR pin on FTDI via capacitor. Pulled high by R6.
D0/RX - FTDI TX
D1/TX - FTDI RX

D2 - D2 on trigger connector
D3 - D3 on left saddle connector
D4 - Data line on DS18B20 breakout
D5 - D5 on left saddle connector
D6 - D6 on left saddle connector
D7 - SPI flash chip slave select
D8 - Source for voltage sense divider. D8 must be high to get voltage reading on A0. Internal voltage ref should be Internal 1.1v 
D9 - CE on NRF24 Module
D10/SS - NRF24 module slave select
D11/MOSI - SPI Master Out Slave In, connected to NRF24, Flash Chip and ICSP
D12/MISO - SPI Master In Slave Out, connected to NRF24, Flash Chip and ICSP
D13/CLK - SPI clock, connected to NRF24, Flash Chip and ICSP

A0 - Voltage Sensor in from R2 and R3 divider
A1 - A1 on left saddle connector
A2 - A2 on left saddle connector
A3 - Data to SHA signing chip
A4/SDA - SDA on right saddle connector
A5/SCL - SCL on right saddle connector

## Power

VCC - 3v3 or lower. Over 3.3v will destroy the NRF24 Module

VIN - on RAW and left saddle connectors. Provides power to the VIN pad of the 3 pin regulator pad. 

Regulator - An external 3 pin regulator (liniar for upto 5v, switched for 5v+) can be soldered here. Should provide 3v3 on VCC

SJ2 - Solder jumper next to the FTDI connector. Selects if FTDI power should go to VCC (3.3v or less) or VIN (more than 3.3v)

C5 - Filter capacitory near battery connector

C2 - Atmega supply capacitor, 0.1uf

C4/C8 - Power capacitors near NRF24 module, 1uf + 10uf

C1 - ARef capacitor, 0.1uf

## Voltage Sense

Voltage divider between resistors R2 and R3 provides a voltage reading of VCC. Useful in battery operated scenarios. To save power this circuit must be activated by writing to the arduino pin D8 high. A small delay after pulling D8 high is recommended to allow the circuit to settle. 

The ADC reference must be set to Internal 1.1v.

Values of 1Mohm for R2 and 470Kohm for R3 will sense a maximum of 3.44v (i.e reading of 1023 on arduino A0). This equates to around 0.003v per ADC step.

## Trigger

VCC and GND pins along with arduino pin D2 are presented. The D2 is an interrupt pin on the Atmega328p, INT0. The solder jumper SJ1 can be used to select a pull up or down through resistor R5

## DS18B20

Data is connected via arduino pin D4, resistor R1 should be 4.7k.

## LED's

LED D1 is enabled through the solder jumper SJ3 and has the current limiting resistor R7. If enabled it is connected to the arduino pin D6
LED D1 is enabled through the solder jumper SJ4 and has the current limiting resistor R8. If enabled it is connected to the arduino pin D2

## Reset

Reset is connected by C3 (0.1uf) to the DTR port of the FTDI connector and to the reset pin of the ICSP connector

## SHA Signing

Tested and Validated Chip : ATSHA204A-STUCZ-T

U2 is connected in onewire mode. Resistor R4 should be 100k

## SPI Flash

Tested and Validated Chip : AT25DN512C-SSHF-B
512Kbit

Used for dualoptiboot over the air programming or general storage. Slave Select is Arduino D7.

## Ceramic Resonator

Specified Chip : CSTCE8M00G52-R0

8Mhz, 10Pf

Currently untested






