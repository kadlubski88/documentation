# Unix
## Philosophy
Unix programs:
- are simple
- follow the element of least surprise
- accept input from stdin
- generate output to stdout
- have meaningfull exit code
- have a manual page

## Architecture
An operating system (OS) can be defined as the software that controls the hardware resources of the computer and provides an environement under which programs can run.

An operating system consists of six differents parts:
- **Kernel:** Core of the OS, controlling the hardware and managing the processes.
- **System calls:** Interface between the kernel and the rest of the OS.
- **Library functions:** Common functions, using the system calls.
- **Shell:** Special application, providing an interface for running other applications.
- **Applications:** Everthing else.

## Logging in
When the user log in, the system looks up in the password file.
~~~
/etc/passwd
~~~
This is a colon separated field table with some information about the user. Every user is represented on one line.
~~~
kadlubski:x:1000:1000:George Kadlubski,,,:/home/kadlubski:/bin/bash
~~~
|field|entry|
|-|-|
|0|login name|
|1|encrypted password|
|2|user id|
|3|group id|
|4|user name + comments|
|5|user home directory|
|6|user command interpreter|

If in the field 1 is an 'x' written, the encrypted password is in the shadow file.
~~~
/etc/shadow
~~~ 

> see:<br>
> passwd(5), shadow(5)

## Program and process
A progam is an executable file saved on the disk. The exec() command is used to run a programm.

An instance of a program is a process.
Every process has a unique PID. A PID is always non-negatve.

For process control, 3 primary functions are used:
- fork()
- exec() -> 7 variants
- waitpid()


