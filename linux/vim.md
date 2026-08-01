# Vim
## Motion
|Key|Motion|
|---|--------|
|`h`|Move cursor to the right|
|`j`|Move cursor to the next line|
|`k`|Move cursor to the previous line|
|`l`|Move cursor to the left|
|`w`|Move cursor to the first character of the next word|
|`b`|Move cursor to the first character of the previous word|
|`e`|Move cursor to the last character of the word or next word|
|`0`|Move cursor to the begining of the line|
|`$`|Move cursor to the end of the line|
|`gg`|Move cursor to the first line|
|`G`|Move cursor to the last line|
|`line number` `G`|Move cursor to the given line number|
|`%`|If cursor on a bracket, move cursor to the next matching bracket|
> NOTE: prepend a number to repeat the motion 

## Text editing
|Key|Action|
|---|--------|
|`i`|Enter insert mode at the cursor|
|`a`|Enter insert mode after the cursor|
|`A`|Enter insert mode at the end of the line|
|`x`|Remove the character under the cursor|
|`d` `motion`|Delete from the cursor before the motion, to the cursor after the motion|
|`dd`|Remove the all line|
|`r` `character`|Replace the character under the cursor with the given character| 
|`R` `characters`|Replace the next characters with the given characters|
|`p`|Put the last removed character(s) after the cursor|
|`P`|Put the last removed character(s) before the cursor|
|`c` `motion`|Remove the character(s) like `d`, but enter insert mode right after| 
|`cc`|Remove the all line and enter insert mode|
