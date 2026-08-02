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
|`f` `character`|Move cursor to the next occurence of the given character|
|`F` `character`|Move cursor to the previous occurence of the given character|
|`gg`|Move cursor to the first line|
|`G`|Move cursor to the last line|
|`line number` `G`|Move cursor to the given line number|
|`%`|If cursor on a bracket, move cursor to the next matching bracket|
|`*`|Move cursor to the next same word|
> NOTE: prepend a number to repeat the motion 

## Text editing
|Key|Action|
|---|--------|
|`i`|Enter insert mode at the cursor|
|`I`|Enter insert mode at the begining of the line|
|`a`|Enter insert mode after the cursor|
|`A`|Enter insert mode at the end of the line|
|`o`|Open a line under the cursor and enter insert mode|
|`O`|Open a line over the cursor and enter insert mode|
|`x`|Remove the character under the cursor|
|`d` `motion`|Delete from the cursor before the motion, to the cursor after the motion|
|`dd`|Remove the all line|
|`r` `character`|Replace the character under the cursor with the given character| 
|`R` `characters`|Replace the next characters with the given characters|
|`p`|Put the last removed or yank character(s) after the cursor|
|`P`|Put the last removed or yank character(s) before the cursor|
|`c` `motion`|Remove the character(s) like `d`, but enter insert mode right after(change)|
|`cc`|Remove the all line and enter insert mode|

## Text object selection
|Key|Action|
|---|--------|
|`a`or`i`|Prefix for the next keys. `a` means with arounding withspaces or wrapper. `i` means only the object| 
|`w`|Word|
|`W`|WORD|
|`s`|Sentence|
|`p`|Paragraph|
|`(`or`)`|In () brackets written text|
|`[`or`]`|In [] brackets written text|
|`{`or`}`|In {} brackets written text|
|`<`or`>`|In <> brackets written text|
|`'`or`"`or`` ` ``|In quotes written text|

## Copying text
|Key|Action|
|---|--------|
|`"``x`|Use register x for the next yank, delete or put|
|`yy`|Copy the line|
|`y` `motion`or`selectio`|Yank|
|`v`|Enter visual mode|
|`V`|Enter visual line mode|
|`ctrl`+`v`|Enter visual block mode|

|Command|Action|
|-------|------|
|registers|List all registers|

## Windows commands
|Command|Action|
|-------|------|
|split|Split horizontaly. The same file.|
|vsplit|Split verticaly. The same file.|
|new|Split horizontaly. A new empty file|
|vnew|Split verticaly. A new empty file|
|only|Close all the other windows|
|resize -N|Decrease current window by N lines|
|resize +N|Increase current window by N lines|

## Other commands
|Command|Action|
|-------|------|
|set number|Enable line numbering|
|set relativenumber|Enable relative line numbering|
|set hlsearch|Enable search highlight|
|noh|Reset current hightlighting|
