# Pinball RS485 architecture

## Hardware

There is a half-duplex RS485 bus. Bus frequency is 2MHz. 

Connector is a standard RJ45 connector with the following pinout:

|Pin|Usage|
|---|---|
|1|RS485 A|
|2|RS485 B|
|3|reserved|
|4|+5V|
|5|+5V|
|6|reserved|
|7|GND|
|8|GND|

+5V/GND is not required, it can be used to power devices from a central node.

## Adressing

Master uses address 0x00.
Slave addresses range from 0x01 to 0xAF. adresses higher than this are reserved for future applications.

|Address|Component|Remarks|
|---|---|---|
|0x00|Master processor||
|0x11|Lamp decoder|e.g. Afterglow or similar|
|0x21|Switch decoder||
|0x31|Solenoid decoder||
|0x41|DMD decoder||
|0x51|Sound decoder||
|0x81-0x8F|Light effects device||


## Line protocol

Bus access is controlled by the master. 
Slaves are only allowed to send data to the bus when the bus master assigned a time slot. 

Each time slot is 1ms long, the client can send for at most 0.9,s which means the maximum transfer size is 1800 bit = 225 octets.
This is the maximum message length supported. If longer data transfers are required, they need to be split into multiple packets.


