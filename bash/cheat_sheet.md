# Bash cheat sheet
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

## get number of characters in a variable
~~~bash
${#variable}
~~~

## get length of an array
~~~bash
${#array[@]}
~~~

## copy file in a variable
~~~bash
file="$(< /path/to/file.txt)"
~~~

## fill array with space separated values from a command
~~~bash
IFS=" " read -ra array <<< "$(command -abc)"
~~~

## fill array with multiline values from a command
~~~bash
IFS=$'\n' read -d "" -ra array <<< "$(command -abc)"
~~~

## test if variable equal to a static string
~~~bash
[[ "$variable" == "static string" ]]
~~~


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