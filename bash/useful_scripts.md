# Useful bash functions
## get all ethernet interfaces and their IP address
~~~bash
get_ips() {
    command="$(lshw -short -quiet -class network 2>/dev/null | awk '/network/{print$2}')"
    IFS=$'\n' read -d "" -ra networks <<< $command
    for network in "${networks[@]}"
    do
        network_ip="$(ip add show $network | awk '/inet /{print $2}')"
        [[ -n $network_ip ]] || network_ip="not connected"
        printf '%s: %s\n' "$network" "$network_ip"
    done
}
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

## change host name
~~~bash
change_hostname() {
    # TBD: cp hostname and hosts file in /tmp
    hostname=$(< "$hostname_path")
    echo "$1" > "$hostname_path"
    # TBD: if sed failed -> restore file
    sed -i "s/$hostname/$1/g" "$hosts_path" 
}
~~~