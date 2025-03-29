# Make basics

## simple makefile
Structure for a rule:
~~~
target: source_1, ..., source_n
\t command_1
\t ...
\t command_n
~~~
Example with multiple rules:
~~~make
bla: bli.o blu.o
    gcc bli.o blu.o -o bla

bli.o: bli.c
    gcc bli.c -c

blu.o: blu.c
    gcc blu.c -c
~~~
A rule can be directly called from the make command.
~~~bash
makefile bli.o
~~~
If no rule is given to the make command, the first one will be called.
## comments
~~~make
#this is a comments
~~~
## call multiple rules
~~~make
all: bli.o blu.o

bli.o: bli.c
    gcc bli.c -c

blu.o: blu.c
    gcc blu.c -c
~~~
If rule "all" is called, bli.o and blu.o will be also called
~~~bash
make all
~~~
## fake target
if no source is given, the target name can be used to run commands
~~~make
clean:
    rm -f *.o
~~~
## shell error
If a command doesnt returns 0, make will exit with an error.

To ignore returns != 0, character "-" is used in front of the command
~~~make
bla:
    -command
~~~
## variable
Variables are typicaly written in upper case. Characters "$", "-" and 
and "=" can not be used.

To define a recursive variable:
~~~make
VARIABLE = bla
~~~
To define a simple variable:
~~~make
VARIABLE := bla
~~~
To use the variable:
~~~make
$(VARIABLE)
~~~
Example:
~~~make
PROGRAMM = bla
OBJECTS = bli.o blu.o
$(PROGRAMM): $(OBJECTS)
    gcc bli.c blu.c -o $(PROGRAMM)
~~~
Example recursive:
~~~make
TEXT = $(WHAT) $(WHO)
# TEXT = $(TEXT) $(WHO) is not possible
WHO = world
WHAT = Hello
WHO = you
all:
    @echo $(TEXT)
    # @ can be use for suppressing the output in stdout of the command itself
~~~
~~~bash
$ make
Hello you
~~~

Example simple:
~~~make
WHO := world
WHAT := Hello
TEXT := $(WHAT) $(WHO)
# TEXT = $(TEXT) $(WHO) is possible
WHO := you
all:
    @echo $(TEXT)
    @echo &(WHO)
~~~
~~~bash
$ make
Hello world
you
~~~
## define
For multiple line variable or multiple commands
~~~make
define bla
Value_1
...
Value_n
endef
~~~
## automatic variable
|variable|explaination|
|-|-|
|$@|target name|
|$<|first source name|
|$?|all sources name|
|$*|target name without extention|
Example:
~~~make
target.o: source.1 source.2 source.3
    @echo "@: " $@
    @echo "<: " $<
    @echo "?: " $?
    @echo "*: " $*
~~~
Results:
~~~
@: target.o
<: source.1
?: source.1 source.2 source.3
*: target
~~~



