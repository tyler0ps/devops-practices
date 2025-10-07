https://sadservers.com/scenario/melbourne

## Will re-do this challenge

   1  curl localhost
    2  curl localhost -v
    3  systemctl status nginx
    4  journalctl -u nginx
    5  journalctl -u nginx --help
    6  journalctl -u nginx --help -r -n50
    7  journalctl -u nginx -r -n50
    8  journalctl -u nginx -r -n20
    9  journalctl -u nginx -r -n20 --no-pager
   10  journalctl -u nginx --no-pager | tail -n20
   11  journalctl -u nginx --no-pager | tail -n20 -f
   12  journalctl -u nginx --no-pager | tail -f
   13  systemctl restart nginx.service 
   14  sudo systemctl restart nginx.service 
   15* 
   16  su root
   17* 
   18  curl localhost -v
   19  ps -ef | grep wdgi
   20  ps -ef | grep wsgi
   21  systemctl list-units --type=service | grep wsgi
   22* 
   23  systemctl list-units --type=service | grep gunicorn
   24  systemctl status gunicorn.service
   25  cat /var/log/nginx/error.log
   26  cat /home/admin/wsgi.py
   27  ps -ef | grep wsgi
   28  sudo ss -tpln
   29  python3 /home/admin/wsgi.py
   30  python3 /home/admin/wsgi.py -v
   31  which python3
   32  systemctl cat gunicorn.s
   33  systemctl cat gunicorn.service 
   34  systemctl cat gunicorn.socket 
   35  cat unix:/run/gunicorn.socket
   36  cat /etc/nginx/nginx.conf 
   37  ls -ltr /etc/nginx/conf.d/
   38  ls -ltr /etc/nginx/modules-enabled/
   39  ls -ltr /etc/nginx/sites-enabled/
   40  cat /etc/nginx/sites-available/default 
   41  sudo ls -l /run/gunicorn.socket
   42  sudo systemctl status gunicorn
   43  sudo journalctl -u gunicorn
   44  sudo journalctl -u gunicorn | tail -n20
   45  sudo journalctl -u gunicorn | tail -n100 | grep -iE "error|fatal"
   46  sudo journalctl -u gunicorn | tail -n100 | grep -iE "error"
   47  sudo journalctl -u gunicorn | tail -n100 | grep -i "error"
   48  sudo journalctl -u gunicorn | tail -n100 | grep -i "fatal"
   49  sudo journalctl -u gunicorn | tail -n100 
   50  sudo journalctl -u gunicorn
   51  sudo ls -l /run/gunicorn.socket
   52  cat /etc/systemd/system/gunicorn.service
   53  sudo ls -l /run/gunicorn.sock
   54  cat /etc/nginx/sites-available/default 
   55  sed -n 's/socket/sock/p' /etc/nginx/sites-available/default 
   56  sed -i 's/socket/sock/g' /etc/nginx/sites-available/default 
   57  sudo sed -i 's/socket/sock/g' /etc/nginx/sites-available/default 
   58  sudo ls -l /run/gunicorn.sock 
   59  sudo systemctl restart nginx.service 
   60  curl localhost
   61  curl localhost:80 -v
   62  tail /var/log/nginx/access.log
   63  curl localhost:80 -v
   64  tail /var/log/nginx/access.log
   65  tail /var/log/nginx/error.log
   66  cat /etc/nginx/sites-available/default
   67  sudo ls -l /run/gunicorn.sock
   68  sudo journalctl -u gunicorn.sock
   69  sudo systemctl status gunicorn
   70  journalctl -u gunicorn
   71* 
   72  journalctl -u gunicorn | tail -n30
   73  curl localhost:80 -v
   74  cat /etc/systemd/system/gunicorn.service
   75  cat /etc/systemd/system/gunicorn.socket 
   76  ps -ef | grep guni
   77  ps -ef | grep nginx
   78  sudo vi /etc/systemd/system/gunicorn.socket
   79  sudo systemctl restart /etc/systemd/system/gunicorn.socket
   80  sudo systemctl restart gunicorn.socket
   81  systemctl daemon-reload
   82  sudo systemctl daemon-reload
   83  sudo systemctl restart gunicorn.socket
   84  journalctl -xe gunicorn.socket 
   85  cat /etc/systemd/system/gunicorn.socket
   86  cat /etc/systemd/system/gunicorn.socket | grep -i nginx
   87  sudo sed -i 's/nginx/www-data/g' /etc/systemd/system/gunicorn.socket
   88  sudo systemctl restart gunicorn.socket
   89  sudo systemctl daemon-reload
   90  sudo systemctl restart gunicorn.socket
   91  curl localhost:80 -v
   92  sudo journalctl -u gunicorn.socket
   93  curl localhost:80 -v
   94  sudo journalctl -u gunicorn.socket
   95  sudo journalctl -u gunicorn.socket 
   96  sudo journalctl -u gunicorn.socket | tail -n20
   97  sudo journalctl -u gunicorn.socket | tail f
   98  sudo journalctl -u gunicorn.socket | tail 
   99  sudo journalctl -u gunicorn.socket | tail -f
  100  sudo journalctl -u gunicorn.socket
  101  sudo ss -xlpn
  102  sudo ss -xlpn | grep gun
  103  sudo systemctl status gunicorn.socket
  104  curl --unix-socket /run/gunicorn.sock http://localhost/
  105  sudo systemctl status gunicorn.service
  106  which wsgi
  107  wsgi
  108  cat /home/admin/wsgi.py
  109  cat /etc/systemd/system/gunicorn.service;
  110  vi /home/admin/wsgi.py
  111  sudo systemctl restart gunicorn.s
  112  sudo systemctl restart gunicorn.service 
  113  sudo systemctl restart gunicorn.socket 
  114  curl localhost
  115  cat /var/log/nginx/error.log
  116  sudo systemctl status gunicorn.service
  117  journalctl -u gunicorn.service
  118  journalctl -u gunicorn.service | tail -n20
  119  vi /home/admin/wsgi.py
  120  sudo systemctl restart gunicorn.socket 
  121  sudo systemctl restart gunicorn.service 
  122  journalctl -u gunicorn.service | tail -n20
  123  curl localhost
  124  history