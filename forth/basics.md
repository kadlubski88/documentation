# Forth
## Forth on Arduino nano v3 (ard nano v4)
### Installation
- Arduino UNO as an ISP programmer
- Get 328-16MHz-38400.hex file from https://github.com/oh2aun/flashforth/tree/master/avr/hex
- Connect ISP programmer to Arduino nano (Dont connect USB on nano) see https://docs.arduino.cc/built-in-examples/arduino-isp/ArduinoISP/ 
- Install avrdude if necessary see https://github.com/avrdudes/avrdude
- Flash nano
    ~~~bash
    avrdude -c arduino -p m328pb -P /dev/ttyACM0 -b 19200 -U flash:w:328-16MHz-38400.hex:i
    # /dev/ttyACM0 is the port of the programmer
    ~~~
- Disconnect nano from programmer
- Connect nano to USB (/dev/ttyUSB0)
- Access forth prompt with
    ~~~bash
    screen -L /dev/ttyUSB0 38400
    ~~~
    

