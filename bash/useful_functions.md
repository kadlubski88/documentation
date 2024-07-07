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