# Pinball RS484 architecture

## Hardware

There is a half-duplex RS485 bus. Bus frequency is 2MHz. 

## Adressing

Master uses address 0x00.
Slave addresses range from 0x01 to 0x7f. adresses higher than this are reserved for future applications.

|address|component|remarks|
|---|---|---|
|0x11|lamp decoder|e.g. Afterglow or similar|
|0x21|switch decoder||
|0x31|solenoid decoder||
|0x41|DMD decoder||

## Line protocol

Bus access is controlled by the master. 
Slaves are only allowed to send data to the bus when the bus master assigned a time slot. 

Each time slot is 1ms long, the client can send for at most 0.9,s which means the maximum transfer size is 1800 bit = 225 octets.
This is the maximum message length supported. If longer data transfers are required, they need to be split into multiple packets.


