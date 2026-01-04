## test if digit
### predicate
~~~forth
: ISDIGIT ( c -- flag)  DUP [char] 0 >= SWAP [char] 9 <= AND ;
~~~ 
### printer
~~~forth
: .ISDIGIT ( n --) CR IF ." Is a digit" ELSE ." Is not a digit" THEN CR ;
~~~ 
