# Linux administration

## UID/GID
Get user ID, user group ID and all groups ID where the user belong.
~~~
id [option] <username (optional)>
~~~
options:
- -u &rarr; show only the user ID
- -g &rarr; show only the user group ID
- -G &rarr; show all the IDs
- -Xn &rarr; show only the names, where X is one of the option above

All groups IDs and who belongs to this groups are stored in the file: `/etc/group`

## login history
Show the login history of the machine
~~~
last
~~~
The history is stored in the file: `/var/log/wtmp` (not readable).

## password management
Manage password of the users
~~~
passwd [option] <username>
~~~
options:
- empty &rarr; prompt to change password interactively (without username for own password)
- -S &rarr; show status of a user password
  - NP &rarr; no password
  - LK or L &rarr; locked
  - P &rarr; password setted
- -l &rarr; block user
- -u &rarr; unblock user
- -e &rarr; let the password expire
- -x \<days> &rarr; max age of a password
- -n \<days> &rarr; min age of a password before changing

Change password over script
~~~
echo <username>:<new password> | chpasswd
~~~

Let a password expire at an certain date
~~~
chage -E <date: 2024-07-19> <username>
#annulation of the expire date
chage -E -1 <username>
~~~

## delete a user
Delete user from the database
~~~
deluser [option] <username>
~~~
options:
- -r &rarr; delete home directory

Delete all the file from the user
~~~
find -uid <user ID> -delete
~~~

## group management
  


