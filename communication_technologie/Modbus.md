# Modbus RTU
Modbus RTU is a fieldbus standard for communication between industrial electronic devices in a RS485 Bus.

## communication
### type
- **direction:** half-duplex
- **topologie:** bus
- **hierarchie:** single master multiple slave
  
### medium
- 2 to 3 wires
- up to 1200m depending on Baud rate

### pinout (typical)
|pin|label|
|-|-|
|1|A(-)|
|2|B(+)|
|3|GND|

### signal
- **type:** differential
- **amplitude:** 2-3V
- **definition:**
  - logical 1 &rbarr; A - B > 0.2V
  - logical 0 &rbarr; A - B < -0.2V
- **rate:** up to 921600 Baud

## description
### Modbus serial line PDU
| Address field | Function code | Data | CRC |
|-|-|-|-|
|1 Byte|1 Byte| 0 to 252 Bytes | 2 Bytes |
> Max 256 Bytes

### Register area
| Name | FC | Access | Register range |
|-|-|-|-|
| Coil | 1,5,15 | read/write | 00001-09999 |
| Discrete input | 2 | read | 10001-19999 |
| Holding register | 3,6,16 | read/write | 40001-49999 |
| Input register | 4 | read | 30001-39999 |

### Function code
|FC|Name|
|-|-|
|1|read coils|
|2|Read discrete inputs|
|3|Read holding register|
|4|Read input register|
|5|Write single coil|
|6|Write single Register|
|15|Write multiple coils|
|16|Write multiple registers|

### PDU
#### FC1 Read coils
Read from 1 to 2000 contiguous status of coils.

Request:
- Function code: 1 Byte
- Starting Address: 2 Bytes
- Quantity of coils: 2 Bytes

Response:
- Function code: 1 Byte
- Byte count: 1 Byte
- Coil status: n Byte
> Up to 8 coil status in one Byte

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### FC2 Read discrete inputs
Read from 1 to 2000 contiguous status of discrete inputs.

Request:
- Function code: 1 Byte
- Starting Address: 2 Bytes
- Quantity of inputs: 2 Bytes

Response:
- Function code: 1 Byte
- Byte count: 1 Byte
- Input status: n Byte
> Up to 8 coil status in one Byte

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### FC3 Read holding registers
Read from 1 to 125 contiguous block of holding registers.

Request:
- Function code: 1 Byte
- Starting Address: 2 Bytes
- Quantity of registers: 2 Bytes

Response:
- Function code: 1 Byte
- Byte count: 1 Byte
- Register values: n Byte
> Two bytes for one register

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### FC4 Read input registers
Read from 1 to 125 contiguous block of input registers.

Request:
- Function code: 1 Byte
- Starting Address: 2 Bytes
- Quantity of registers: 2 Bytes

Response:
- Function code: 1 Byte
- Byte count: 1 Byte
- Register values: n Byte
> Two bytes for one register

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### FC5 Write single coil
Request:
- Function code: 1 Byte
- Output address: 2 Bytes
- Output value: 2 Bytes
> True(0x0000) or False(0xFF00)

Response:
- Function code: 1 Byte
- Output address: 2 Bytes
- Output values: 2 Bytes
> True(0x0000) or False(0xFF00)

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### FC6 Write single register
Request:
- Function code: 1 Byte
- Register address: 2 Bytes
- Register value: 2 Bytes

Response:
- Function code: 1 Byte
- Register address: 2 Bytes
- Register values: 2 Bytes

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### FC15 Write multiple coils
Write from 1 to 1968 contiguous status of coils.
Request:
- Function code: 1 Byte
- Starting address: 2 Bytes
- Quantity of outputs: 2 Bytes
- Byte count: 1 Byte
- Output values: n Bytes
> Up to 8 coil status in one Byte

Response:
- Function code: 1 Byte
- Starting address: 2 Bytes
- Quantity of outputs: 2 Bytes

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### FC16 Write multiple registers
Write from 1 to 123 contiguous registers.
Request:
- Function code: 1 Byte
- Starting address: 2 Bytes
- Quantity of registers: 2 Bytes
- Byte count: 1 Byte
- Register values: n Bytes
> Two bytes for one register

Response:
- Function code: 1 Byte
- Starting address: 2 Bytes
- Quantity of registers: 2 Bytes

Error:
- Function code: 1 Byte (Function code + 0x80)
- Exeption code: 1 Byte

#### Exeption code
|Code|Definition|
|-|-|
|1|Function code not supported|
|2|Address is invalid|
|3|Address is out of range|
|4|Request failed|

## references
- <a href="https://www.modbus.org/file/secure/modbusoverserial.pdf">Modbus Serial Line Protocol</a>
- <a href="https://www.modbus.org/file/secure/modbusprotocolspecification.pdf">Modbus Application Protocol</a>



