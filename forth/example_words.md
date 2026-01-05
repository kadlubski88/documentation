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
