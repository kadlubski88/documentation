## test if digit
### predicate
~~~forth
: ISDIGIT ( c -- flag)  DUP [char] 0 >= SWAP [char] 9 <= AND ;
~~~ 
### printer
~~~forth
: .ISDIGIT ( n --) CR IF ." Is a digit" ELSE ." Is not a digit" THEN CR ;
~~~ 
## pseudo random number
~~~forth
: prand ( n1 n2 -- n) over - utime + swap mod + ;
~~~
- n1: offset
- n2: max value
- n: value between n1 and (n2 - n1)
## is in range (lo <= n < hi)
~~~forth
: INRANGE (n lo hi -- flag) OVER - ROT ROT - U> ;
~~~
> Test:
> |Word|Stack status|
> |-|-|
> | |n lo hi|
> |OVER|n lo hi lo|
> |-|n lo (hi - lo)|
> |ROT|lo (hi - lo) n|
> |ROT|(hi - lo) n lo|
> |-|(hi - lo) (n - lo)|
> |U>|(hi - lo) U> (n - lo)| 

From https://www.forth.com/starting-forth/4-conditional-if-then-statements/

OR

~~~forth
: INRANGE (n lo hi -- flag) ROT DUP ROT < ROT ROT <= AND ;
~~~
> Test:
> |Word|Stack status|
> |-|-|
> | |n lo hi|
> |ROT|lo hi n|
> |DUP|lo hi n n|
> |ROT|lo n hi n|
> |<|lo n (hi < n)|
> |ROT|n (hi < n) lo|
> |ROT|(hi < n) lo n|
> |<=|(hi < n) (lo <= n)|
> |AND|(hi < n) AND (lo <= n)|

## Reverse star parallelogram
~~~forth
: /STARS (n1 n2 --) --->/10 3 
    CR DUP 0            /10 3 3 0
    +DO                 /10 3               + 10 2
        1 - DUP 0       /10 2 2 0           | 10 1 1 0
        +DO             /10 2               | 10 1
            32 emit     /Print 2 spaces     | 10 1
        LOOP            /10 2               | 10 1
        OVER 0          /10 2 10 0          | 10 1 10 0
        +DO             /10 2               | 10 1
            ." *"       /Print 10 stars     | 10 1
        LOOP            /10 2               | 10 1
        CR              /10 2               |
    LOOP                /------------------>+
    DROP DROP           /Clean up the stack
;
~~~

## Print ASCII table
~~~forth
: .ASCII ( -- )
    CR 127 32 
    +DO 
        DECIMAL I . ." : " HEX I . ." : " I EMIT CR
    LOOP
    DECIMAL
;
.ASCII
BYE
~~~

## Print endless diamants
~~~forth
: DIAMANT ( n -- )
    >R
    1 1
    BEGIN
        DUP R@ SWAP - SPACES 
        DUP 2 * 0 
        +DO   
            ." *"
        LOOP
        DUP R@ >=
        IF
            SWAP DROP -1 SWAP
        THEN
        DUP 1 <=
        IF 
            SWAP DROP 1 SWAP
        THEN
        OVER +
        CR
        20 MS
    AGAIN
;
20 DIAMANT
BYE
~~~

