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


