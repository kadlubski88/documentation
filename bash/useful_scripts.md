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

## NTP synchronisation manager
~~~bash
timesync() {
    #set default variable
    is_sync="false"
    is_active="false"
    ntp_server_ip="not defined"

    #set awk scripts
    read -rd '' awk_get_state <<'EOF'
    /NTP service/ {print "service:" $2}
    /synchronized/ {print "sync:" $2}
    EOF

    read -rd '' awk_get_server <<'EOF'
    /Server/ {print $2}
    EOF

    read -rd '' awk_overwrite_conf <<'EOF'
    /NTP=/ && !/Fallback/ {$0="NTP=" ip} 1
    EOF

    get_status() {
        state=$(sudo timedatectl | awk -F ': ' "$awk_get_state")
        local old_IFS=$IFS
        IFS=$'\n' 
        read -d "" -ra state_array <<< "$state"
        IFS=":"
        for ((i=0;i<${#state_array[@]};i++))
        do
            state_property=(${state_array[$i]})
            case ${state_property[0]} in
                sync) [[ "${state_property[1]}" == "yes" ]] && is_sync="true" ;;
                service) [[ "${state_property[1]}" == "active" ]] && is_active="true" ;;
            esac
        done
        ntp_server_ip=$(sudo timedatectl timesync-status | awk -F ': ' "$awk_get_server")
        IFS=$old_IFS
    }

    print_status() {
        printf '%s:\t%s\n' "NTP active" "$is_active"
        printf '%s:\t%s\n' "Synchronized" "$is_sync"
        printf '%s:\t%s\n' "Server address" "$ntp_server_ip"
    }

    do_reload() {
        sudo systemctl restart systemd-timesyncd &>/dev/null || printf '%s\n' "reloading failed"
    }

    enable_sync() {
        sudo timedatectl set-ntp true
    }

    disable_sync() {
        sudo timedatectl set-ntp false
    }

    set_server() {
        cp /etc/systemd/timesyncd.conf /tmp/timesyncd.conf.tmp
        awk -v ip="$1" "$awk_overwrite_conf" /tmp/timesyncd.conf.tmp > /etc/systemd/timesyncd.conf
    }

    for ((i=1;i<=$#;i++))
    do
        case ${!i} in
            enable) enable_sync ;;
            disable) disable_sync ;;
            set)
                next_index=$((i + 1))
                set_server ${!next_index}
                ;;
            reload) do_reload ;;
            status) 
                get_status
                print_status
                ;;
        esac
    done
}
~~~