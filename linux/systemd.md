# Systemd
## Type of unit files
- service
- socket
- slice
- mount / automount
- target
- timer
- path
- swap

## Relevant file location
|Path|Comment|
|-|-|
|/lib/systemd/|Systemd executables|
|/lib/systemd/system/|System unit files|
|/etc/systemd/|Systemd configurations|
|/etc/systemd/systen/|Unit files overwrites|
|/var/log/syslog|Systemd log file|

## Systemd tools
### Analysing tool
- time to bootup
    ~~~bash
    systemd-analyze time
    ~~~
- time to initialize units
    ~~~bash
    systemd-analyze blame <[optional] unit name>
    ~~~
- security
    ~~~bash
    systemd-analyze security <[optional] unit name>
    ~~~
### Show all settings of a unit
~~~bash
systemctl cat <unit name>
~~~

## Logging
~~~bash
journalctl [options]
~~~
options:
- -e &rarr; Show a couple entries from the end
- -f &rarr; Follow
### write to logging from script
~~~bash
systemd-cat [options] <[optional] command>
~~~
options:
- -p \<priority> &rarr; info | debug | crit | ...

When no commands given then log input stream, otherwise redirect output and error stream of the command to the log.  


## Editing services
Edit an overwrite file for a service.
~~~
systemctl edit [options] <name of service>
~~~
options:
- --full &rarr; edit the full service
- --force &rarr; create a new service if not existing

## Unit directives
Show all directives and where it is documented:
~~~bash
man systemd.directives
~~~
### [Unit]
- Description: Short decription text
- Wants: Units to be started along(weak)
- After: Starts after the listed units are up
- Before: Starts before the listen units
- OnFailure: Units to start if entering "failed" state
~~~bash
man systemd.unit
~~~
### [Service]
- ExecStartPre: Command to execute before ExecStart
- ExecStart: Command to execute when started
- ExecStartPost: Command to execute after ExecStart
- ExecStop: Command to execute when stoped
- IPAddressAllow: IP addresses allowed to reach the unit
- IPAddressDeny: IP addresses denied to reach the unit
- RestrictNetworkInterfaces: Network interfaces allowed to reach the unit
~~~bash
man systemd.service
~~~
### [Install]
Relevant when enabling
- WantedBy: Let the listed units starts this unit (link in .wanted)
- Alias: Give an alternative name for this unit
~~~bash
man systemd.unit
~~~

## Target
A systemd target is a group of other units (service, path, mount points, socket, other targets)for a particular purpose.

### Important targets
|target|description|
|-|-|
|multi-user|OS fully operational in text mode|
|graphical|OS fully perational in graphical mode|
|rescue|Small system only for root(maintenance)|
|emergency|Minimal system for recovery|

### Change default target
get actual default target:
~~~bash
systemctl get-default
~~~
temporarly:
~~~bash
systemctl isolate <target name>
~~~
persistent:
~~~bash
systemctl set-default <target name>
