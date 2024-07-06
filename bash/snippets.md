# Bash snippets

## Get network interface names
~~~bash
sudo lshw -short | grep network | awk '{print$2}'
~~~

## Get usage of mass memory in procent
~~~bash
df -h | grep -w "/" | grep -o "..%"
~~~