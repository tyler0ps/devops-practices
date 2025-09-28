https://sadservers.com/scenario/saskatoon

Description: There's a web server access log file at /home/admin/access.log. The file consists of one line per HTTP request, with the requester's IP address at the beginning of each line.

Find what's the IP address that has the most requests in this file (there's no tie; the IP is unique). Write the solution into a file /home/admin/highestip.txt. For example, if your solution is "1.2.3.4", you can do echo "1.2.3.4" > /home/admin/highestip.txt

Root (sudo) Access: False

Test: The SHA1 checksum of the IP address sha1sum /home/admin/highestip.txt is 6ef426c40652babc0d081d438b9f353709008e93 (just a way to verify the solution without giving it away.)

egrep -o '^([0-9]{1,3}.){3}([0-9]{1,3})' /home/admin/access.log | sort | uniq -c | sort -nrk1 | head -1 | awk '{print $2}' > /home/admin/highestip.txt