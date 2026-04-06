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
## relevant file location
|Path|Comment|
|-|-|
|/lib/systemd/|Systemd executables|
|/lib/systemd/system/|System unit files|
|/etc/systemd/|Systemd configurations|
|/etc/systemd/systen/|Unit files overwrites|
|/var/log/syslog|Systemd log file|

## Editing services
Edit an overwrite file for a service.
~~~
systemctl edit [options] <name of service>
~~~
options:
- --full &rarr; edit the full service
- --force &rarr; create a new service if not existing

