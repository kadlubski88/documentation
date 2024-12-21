# IO-Link
IO-Link is a standardised(IEC 61131-9) Input/Output technologie to communicate with sensors and with actors.
- plug and play capabillity
- integrated diagnostic
- remote parametrisation

## communication
### type
- **direction:** half-duplex
- **topologie:** point to point
- **hierarchie:** single master multiple slave
  
### medium
- 3 to 5 wires
- max 20m
- min 0.34 mm²

### pinout (typical)
|pin|port class A|port class B|
|-|-|-|
|1|L+|L+|
|2|DI/DQ (optional)|2L+|
|3|L-|L-|
|4|C/Q|C/Q|
|5|-|2M|

### signal
- **type:** single ended
- **amplitude:** 0-24V
- **definition:** 
  - logical 1 &rbarr; (C/Q) - (L-) = 0V
  - logical 0 &rbarr; (C/Q) - (L-) = 24V
- **rate:** 4.8 to 230.4 kBauld

## description
IO-Link devices, like sensors or actores, are connected to a IO-Link Master. The master is the gateway between the devices and a higher level controller.<br>
The devices are parameterized with a IODD(IO Device Description) file.<br>
The IODD is a XML file containing all the information of the device, like:
- communication property
- value range
- default value
- identification
- process diagnostic
- device data
- text description
- illustration

Most of the IODD can be found in the official IODD database <a href="https://ioddfinder.io-link.com/#/">IIOD finder</a>

there is 4 different data transmission type:
- process data(cyclic): to 32 byte of data
- value status(cyclic)
- device data(acyclic): serial number, diagnostic, ...
- event(acyclic)
  
The pull rate of a cyclic transmission can be parameterized. An acyclic transmission is triggerd on demand or through a given treshhold.

When the master is not able to reached the device after a certain number of tentative, he will signal an error to the higher level controller.

There is two types of IO-Link ports:
- port class A: 
  - power supply for the device: 24V 200mA
  - optional a digital input/output
  - M5 to M12 socket, max 4 pins
- port class B:
  - power supply for the device: 24V 200mA
  - second isolated power supply: 24V 1.6-3.5A
  - M12 socket, 5 pins
  
An IO-Link master port support 4 modes:
- IO-Link communication
- digital input
- digital output
- deactivated

## references
- <a href="https://io-link.com/en/">official main page</a>
- <a href="https://io-link.com/share/Downloads/At-a-glance/IO-Link_System_Description_eng_2018.pdf">system description pdf</a>
- <a href="https://io-link.com/share/Downloads/Package-2020/IOL-Interface-Spec_10002_V113_Jun19.pdf">system specification pdf</a>



