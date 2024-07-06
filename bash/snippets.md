# Bash snippets

## Get network interface names
~~~bash
sudo lshw -short -quiet -class network | awk '/network/{print$2}'
~~~

## Get usage of mass memory in procent
~~~bash
df | grep -w "/" | grep --color=never -o "..%"
~~~

## Get ip address of a specific device
~~~bash
ip add show <device name> | awk '/inet /{print $2}'
~~~