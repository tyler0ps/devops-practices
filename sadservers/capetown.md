https://sadservers.com/newserver/capetown

admin@ip-10-1-12-106:/$ history
    1  exit
    2  ls
    3  systemctl status nginx.service
    4  ls -ltr /etc/nginx/sites-enabled/default
    5  sudo -u vi /etc/nginx/sites-available/default
    6  sudo vi /etc/nginx/sites-available/default
    7  systemctl restart nginx
    8  sudo systemctl restart nginx
    9  ls
   10  su -
   11  clear
   12  history
   13  curl -I 127.0.0.1:80
   14  find . -type f -name "*nginx.conf" 2>/dev/null
   15  cat ./etc/nginx/nginx.conf
   16  cat ./etc/nginx/nginx.conf | grep -i error
   17  tail --help
   18  tail /var/log/nginx/error.log; -n20
   19  cat ./etc/nginx/nginx.conf | grep -i worker_rlimit_nofile
   20  sudo vi ./etc/nginx/nginx.conf `
   21  sed '4i worker_rlimit_nofile 25000;' ./etc/nginx/nginx.conf
   22  sed '5i worker_rlimit_nofile 25000;' ./etc/nginx/nginx.conf
   23  sed '5i worker_rlimit_nofile 25000;' ./etc/nginx/nginx.conf | head -10
   24  sed '5i worker_rlimit_nofile 25000;' ./etc/nginx/nginx.conf | head -6
   25  sudo sed -i '5i worker_rlimit_nofile 25000;' ./etc/nginx/nginx.conf | head -6
   26  systemctl restart nginx
   27  sudo systemctl restart nginx
   28  curl -I 127.0.0.1:80
   29  history
   30  at /etc/nginx/sites-available/default
   31  cat /etc/nginx/sites-available/default
   32  sed '1i ;' /etc/nginx/sites-available/default | head -5
   33  sed '1i ;' /etc/nginx/sites-available/default | sed '1d' | head -5
   34  history
   35  echo test
   36  curl -Is 127.0.0.1:80|head -1
   37  history