# Bash snippets

## Get network interface names
~~~bash
sudo lshw -short -quiet -class network | grep network | awk '{print$2}'
~~~

## Get usage of mass memory in procent
~~~bash
df | grep -w "/" | grep --color=never -o "..%"
~~~