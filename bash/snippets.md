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

## Stop all docker container
~~~bash
docker stop $(docker ps -a -q)
~~~

## is IP address valide
~~~bash
is_ip_valide() {
    [[ $1 =~ ^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$ ]] || return 1
    local old_IFS=$IFS
    IFS='.'
    local ip_array=($1)
    [[ $((ip_array[0])) -le 255 && $((ip_array[1])) -le 255 && $((ip_array[2])) -le 255 && $((ip_array[3])) -le 255 ]] || return 1
    IFS=$old_IFS
    return 0
}
~~~