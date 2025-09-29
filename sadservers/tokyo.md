https://sadservers.com/scenario/tokyo
    1  exit
    2  iptables -L
    3  iptables --help
    4  iptables --list
    5  iptables -C INPUT
    6  sudo iptables -S INPUT
    7  curl -v 127.0.0.1
    8  sudo iptables -S INPUT
    9  iptables --help
   10  iptables --help | grep "-S"
   11  iptables --help | grep "\-S"
   12* iptables -S 
   13  iptables -S INPUT
   14  iptables -D INPUT -p tcp --dport 80 -j DROP
   15  iptables -S INPUT
   16  curl 127.0.0.1:80
   17  cat /etc/passwd | grep www
   18  chown www-data /var/www/html/index.html 
   19  ls -ltr /var/www/html/index.html 
   20  curl 127.0.0.1:80
   21  history