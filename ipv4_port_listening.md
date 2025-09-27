In the current directory there is a file called netstat.out.

Print all the IPv4 listening ports sorted from the higher to lower.

awk '/tcp\ .*LISTEN/{print $4}' netstat.out | awk -F: '{print $2}' | sort -nr