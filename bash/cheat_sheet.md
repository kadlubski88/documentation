# Bash cheat sheet

## variable
### write a complex string in a variable
~~~bash
read variable <<'EOF'
some
complex
string
EOF
~~~
### copy file in a variable
~~~bash
variable="$(< /path/to/file.txt)"
~~~
### get number of characters in a variable
~~~bash
${#variable}
~~~
## variable substitution
if variable is undefined or an empty string <br>
then return substitution <br>
else return variable
~~~bash
echo ${variable:-"substitution"}
# only if undefined:
echo ${variable-"substitution"}
~~~
if variable is undefined or an empty string <br>
then return an empty string
else return substitution
~~~bash
echo ${variable:+"substitution"}
# only if undefined:
echo ${variable+"substitution"}
~~~
if variable is undefined or an empty string <br>
then initialise variable with value
~~~bash
${variable:="value"}
# only if undefined:
${variable="value"}
~~~
if variable is undefined or an empty string <br>
then <br>
&emsp; if message is undefined <br>
&emsp; then return a standard stderr and stop script <br>
&emsp; else return message on stderr and stop script <br>
else return variable
~~~bash
echo ${variable:?["message"]}
# only if undefined:
echo ${variable?["message"]}
~~~



## predifined variables
|variable|definition|
|-|-|
|$#|number of arguments|
|$*|all arguments in a string separated with $IFS|
|$@|all arguments in separate strings|
|$0|program path relative to $PWD|
|$x|x'st argument (1 to 9)|
|$?|exit code from the last called programm|
|$$|pid of the actual process|
|$!|pid of the last called process|
### shift
shift n time the arguments
($x &rarr; $x-n)
~~~bash
shift n
~~~

## escape sequence
~~~bash
$'escape_sequence'
~~~
|escape sequence|definition|
|-|-|
|\b|backspace|
|\n|new line|
|\r|cariage return|
|\t|horizontal tabulator|
|\v|vertical tabulator|

## environement variable
### set environment variable
~~~bash
export $ENVIRONEMENT_VARIABLE
~~~

## array
### define array
~~~bash
array=(value1 value2 value3)
~~~
### define dictionary
~~~bash
dictionary[key]=value
~~~
### get cell value
~~~bash
echo ${array[index/key]}
~~~
### get length of an array
~~~bash
${#array[@]}
~~~
### fill array with space separated values from a command
~~~bash
IFS=" " read -ra array <<< "$(command -abc)"
~~~
### fill array with multiline values from a command
~~~bash
IFS=$'\n' read -d "" -ra array <<< "$(command -abc)"
~~~

## test
### true
~~~bash
[[ expression ]]
~~~
### false
~~~bash
[[ ! expression ]]
~~~
### and
~~~bash
[[ expression1 -a expression2 ]]
~~~
### or
~~~bash
[[ expression1 -o expression2 ]]
~~~
### string
~~~bash
[[ [option] string ]]
~~~
|option|definition|
|-|-|
|-n|length is not zero|
|-z|length is zero|
### string comparaison
~~~bash
[[ string1 [option] string2 ]]
~~~
|option|definition|
|-|-|
|=|equal|
|!=|not equal|
### integer comparaison
~~~bash
[[ integer1 [option] integer2 ]]
~~~
|option|definition|
|-|-|
|-eq|is equal|
|-ge|is greater or equal than|
|-gt|is greater than|
|-le|is less or equal than|
|-lt|is less than|
|-ne||is not equal|
### file
~~~bash
[[ [option] file ]]
~~~
|option|definition|
|-|-|
|-e|exists|
|-f|exists and is a regular file|
|-d|exists and is a directory|
|-s|exists and has a size greater than 0|
|-w|exists and the user has write access|
|-w|exists and the user has execute access|
### file comparaison
~~~bash
[[ file1 [option] file2 ]]
~~~
|option|definition|
|-|-|
|-ef|is have the same device and inode numbers|
|-nt|is newer(modification) than|
|-ot|is older than|


## integer calculation
~~~bash
expr integer1 [signe/comparator] integer2
~~~
signe:
- \+
- \-
- \*
- \/
- \%

comparator:
- =
- !=
- \>
- \>=
- \<
- \<=

## subshell
~~~bash
# do something in current dir
(cd /some/other/dir && other-command)
# continue in original dir
~~~
## brace expansion
~~~bash
rm /some/dir/file.{sh,md}
#rm /some/dir/file.sh
#rm /some/dir/file.md
~~~
~~~bash
rm /some/dir/file{,.md}
#rm /some/dir/file
#rm /some/dir/file.md
~~~
~~~bash
rm /some/dir/file_{1..3}
#rm /some/dir/file_1
#rm /some/dir/file_2
#rm /some/dir/file_3
~~~

## tilde
- ~ &rarr; same as $HOME
- ~+ &rarr; same as $PWD
- ~- &rarr; same as $OLDPWD

## command line keyboard shortcuts
|keys|action|
|----|------|
|tab |auto completion|
|ctrl + r|command history|
|ctrl + a|move cursor to start of the line|
|ctrl + e|move cursor to end of the line|
|alt + f|jump to next word|
|alt + b|jump one word back|
|ctrl + u|cut from cursor to start of the line|
|ctrl + k|cut from cursor to end of the line|
|ctrl + y|paste cutted text|
|shift + ctrl + c|copy selection|
|shift + ctrl + v|paste selection|
|ctrl + l|clean the screen|
|ctrl + x ctrl + e|edit command in text editor|
