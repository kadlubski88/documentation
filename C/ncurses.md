# ncurses

## description
ncurses is a TUI library. It is heavely used in UNIX based systems.

[Tutorial 1](https://tldp.org/HOWTO/NCURSES-Programming-HOWTO/intro.html#WHERETOGETIT)

[Tutorial 2](https://invisible-island.net/ncurses/ncurses-intro.html)

## installation
~~~
sudo apt install libncurses-dev
~~~

## compiling
~~~
gcc <file to compile> -lncurses
~~~
## hello world
~~~c
#include <ncurses.h>

int main() {	
	initscr();
	printw("Hallo Welt!");	
	refresh();			
	getch();			
	endwin();			

	return 0;
}
~~~

## functions
### initscr()
Initialize the curses library and create a window(write buffer).
~~~c
WINDOW * initscr(void);  
~~~
### printw()
Write a string in the standard window at the cursor position.
~~~c
int printw(const char *str,...);
~~~
### refresh()
Routine to update the screen.
~~~c
int refresh(void); 
~~~
### getch()
~~~c
int getch(void);
~~~
### endwin()
Terminate ncurses and clean
~~~c
int endwin(void);
~~~
### move()
Move the cursor in the standard window.
~~~c
int move(int y, int x);
~~~
### addch()
Write a character in the standard window at the cursor position.
~~~c
int addch(const chtype ch); 
~~~
### cbreak()
Deactivate the terminal buffer. Ctrl-C will still functioning(terminate programm).
~~~c
int cbreak(void);
~~~
### noecho()
Deactivate echoing. 
~~~c
int noecho(void);
~~~
### getmaxyx()
Get the number of raws and columns of the selected window.
~~~c
? getmaxyx(WINDOW *win,int y,int x);
~~~