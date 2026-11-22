# Fortran 77
## EBCDI-Code
Extended binary coded decimal interchange code
|H\L|0|1|2|3|4|5|6|7|8|9|A|B|C|D|E|F|
|---|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|0  | | | | |b|&|-| | | | | | | | |0|
|1  | | | | | | |/| |a|j| | |A|J| |1|
|2  | | | | | | | | |b|k|s| |B|K|S|2|
|3  | | | | | | | | |c|l|t| |C|L|T|3|
|4  | | | | | | | | |d|m|u| |D|M|U|4|
|5  | | | | | | | | |e|n|v| |E|N|V|5|
|6  | | | | | | | | |f|o|w| |F|O|W|6|
|7  | | | | | | | | |g|p|x| |G|P|X|7|
|8  | | | | | | | | |h|q|y| |H|Q|Y|8|
|9  | | | | | | | | |i|r|z| |I|R|Z|9|
|A  | | | | | |!| |:| | | | | | | | |
|B  | | | | |.|$|,|#| | | | | | | | |
|C  | | | | |<|*|%|@| | | | | | | | |
|D  | | | | |(|)|_|'| | | | | | | | |
|E  | | | | |+|;|>|=| | | | | | | | |
|F  | | | | | | |?|"| | | | | | | | |

## Punched card
- 12 rows
- 80 columns
### typical code
|row\value|0|1|2|3|4|5|6|7|8|9|A|B|C|D|E|F|G|H|I|J|K|L|M|N|O|P|Q|R|S|T|U|V|W|X|Y|Z|.|<|(|+|-|*|)|/|,|%|#|@|
|---------|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|12       |-|-|-|-|-|-|-|-|-|-|X|X|X|X|X|X|X|X|X|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|X|X|X|X|-|-|-|-|-|-|-|-|
|11       |-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|X|X|X|X|X|X|X|X|X|-|-|-|-|-|-|-|-|-|-|-|-|X|X|X|-|-|-|-|-|
|0        |X|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|X|X|X|X|X|X|X|X|-|-|-|-|-|-|-|X|X|X|-|-|
|1        |-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|X|-|-|-|-|
|2        |-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|3        |-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|X|-|
|4        |-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|-|-|-|-|-|X|-|-|-|X|-|-|-|X|-|X|
|5        |-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|-|-|-|-|-|X|-|-|-|X|-|-|-|-|-|
|6        |-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|
|7        |-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|8        |-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|X|X|X|X|-|X|X|-|X|X|X|X|
|9        |-|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|X|-|-|-|-|-|-|-|-|-|-|-|-|

## Column position rules
|columns|values|
|-|-|
|1|empty or 'C' for a comment|
|1-5|[optional] label
|6|[optional] continuation of previous line
|7-72| statement
|73-80|[optional] sequence number

## Variable types
- INTEGER
- REAL
- DOUBLE PRECISION
- COMPLEX
- LOGICAL
- CHARACTER

## Jump instruction
### Aritmetic condition
~~~
IF(x) n1, n2, n3
~~~
x  -> integer or real to test from an expresion or direct
n1 -> label to jump when x < 0
n2 -> label to jump when x = 0
n3 -> label to jump when x > 0
### logical condition
~~~
IF(x) s
~~~
x -> logical value to test
s -> statement to run if x is true (for example GOTO)

Also possible since 77 (but boring):
~~~
IF(x)
THEN
s1
ELSEIF(x2)
s2
ELSE
s3
ENDIF
~~~

### Unconditional
~~~
GOTO n
~~~
n -> label to jump

### calculated
~~~
GOTO(n1, n2, nm), I
~~~
I -> Variable containing the index of n (1, 2, ..., m)
nx -> label to jump when I = x

## Logical expresion
possible values:
- .TRUE.
- .FALSE.
### relational operator
- .LT. : Less
- .LE. : Less or equal
- .GT. : Greater
- .GE. : Greater or equal
- .EQ. : Equal
- .NE. : Not equal
### logical operator
- .NOT.
- .OR.
- .AND.

## Standard function
### mathematical
- EXP(f)
- ALOG(f)
- SIN(f)
- COS(f)
- ATAN(f)
- TANH(f)
- SQRT(f)
### type casting
- FLOAT(i)
- IFIX(f)
### absolute value
- IABS(i)
- ABS(f)
### sign transfer
- ISIGN(j,i)
- SIGN(g,f)
