# Forth
## Math (simple) operators
|Word|Stack notation|
|-|-|
|+| n1 n2 -- (n1 + n2)|
|-| n1 n2 -- (n1 - n2)|
|*| n1 n2 -- (n1 * n2)|
|/| n1 n2 -- (n1 / n2)|
|MOD| n1 n2 -- (n1 % n2)|
|/MOD| n1 n2 -- (n1 % n2) (n1 / n2)|
## Stack manipulation operators
|Word|Stack notation|
|-|-|
|SWAP| n1 n2 -- n2 n1|
|2SWAP| n1 n2 n3 n4 -- n3 n4 n1 n2 
|DUP| n -- n n|
|2DUP| n1 n2 -- n1 n2 n1 n2|
|OVER| n1 n2 -- n1 n2 n1|
|2OVER| n1 n2 n3 n4 -- n1 n2 n3 n4 n1 n2|
|ROT| n1 n2 n3 -- n2 n3 n1|
|-ROT| n1 n2 n3 -- n3 n2 n1|
|2ROT| n1 n2 n3 n4 n5 n6 -- n3 n4 n5 n6 n1 n2| 
|DROP| n --|
|2DROP| n1 n2 --|
## Comparison operators
|operator|Stack notation|
|-|-|
|=| n1 n2 -- (n1 == n2)|
|<>| n1 n2 -- (n1 != n2)|
|<| n1 n2 -- (n1 < n2)|
|>| n1 n2 -- (n1 > n2)|
|U<| u1 u2 -- (u1 < u2)|
|U>| u1 u2 -- (u1 > u2)|
|0=| n -- (n == 0)|
|0<| n -- (n < 0)|
|0>| n -- (n > 0)|
## Condition
~~~forth
IF ... ELSE ... THEN
~~~
IF reads the stack and compare to 0 (false). If it is not false, the words after IF until ELSE or THEN will be called. If it is false, then it's jump to ELSE or THEN (if ELSE not exists). The words after THEN will be always called.

IF can be nested in other IFs
~~~forth
DUP IF ... ELSE
DUP IF ... ELSE
IF ... ELSE
THE THEN THEN
~~~

~~~forth
ABORT" ..."
~~~
will abort the codition and write a string to the std output.

~~~forth
EXIT
~~~
 to exit the condition prematurely.

## Time operators
|Word|Stack notation|Comment|
|-|-|-|
|ms| n --| wait for at least n ms|
|uptime| -- d| get time in us since epoch| 
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
    

