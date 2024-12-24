## exit(3)
~~~c
#include <stdlib.h>

void exit(int status);
~~~
The exit function will terminate the process and run registred functions. (atexit(3), on_exit(3))
_exit(2) or _Exit(2) can be used to bypass the registred functions.
All open stdio(3) streams are flushed and closed.

## atexit(3)
~~~c
#include <stdlib.h>

int atexit(void (*function)(void));
~~~
Register a function to be run at exit(3)

Example:
~~~c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

    void
    bye(void) {
        printf("Bye world\n");
    }

    int
    main(void) {
        long a;
        int i;

        a = sysconf(_SC_ATEXIT_MAX);
        printf("ATEXIT_MAX = %ld\n", a);

        i = atexit(bye);
        if (i != 0) {
            fprintf(stderr, "cannot set exit function\n");
            exit(EXIT_FAILURE);
        }

        exit(EXIT_SUCCESS);
    }

~~~