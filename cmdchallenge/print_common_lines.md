access.log.1 and access.log.2 are http server logs.
Print the IP addresses common to both files, one per line.

grep -oE -h "([0-9]{1,3}\.){3}[0-9]{1,3}" access.log.* | sort | uniq -d