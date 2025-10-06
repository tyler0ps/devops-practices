# "Karakorum": WTFIT – What The Fun Is This?
https://sadservers.com/newserver/karakorum

## Solution
```bash
sudo apt-get install --reinstall coreutils
sudo chmod +x /home/admin/wtfit
touch /home/admin/wtfitconfig.conf
sudo sed -i 's/listen 80 default_server;/listen 7777 default_server;/' /etc/nginx/sites-available/default 
sudo systemctl restart nginx.service
/home/admin/wtfit
```

## Full CMD history
```bash
    1  ls
    2  sudo apt-get install --reinstall coreutils
    3  ls
    4  cd /home/admin/
    5  ls
    6  sudo chmod +x wtfit 
    7  ./wtfit 
    8  strace v 
    9  strace ./wtfit
   10  touch /home/admin/wtfitconfig.conf
   11  strace ./wtfit
   12  sudo tcpdump -i lo -A
   13  nginx
   14  systemctl status nginx
   15  systemctl start nginx
   16  sudo systemctl restart nginx
   17  systemctl status nginx
   18  cat /etc/nginx/
   19  cat /etc/nginx/nginx.conf 
   20  cat /etc/nginx/conf.d/*.conf
   21  ls /etc/nginx/conf.d/
   22  cat etc/nginx/conf.d/default.conf
   23  cat /etc/nginx/nginx.conf | grep 80
   24  cat /etc/nginx/nginx.conf | grep listen
   25  vi /etc/nginx/nginx.conf 
   26  cd /etc/nginx/
   27  ls
   28  ls -ltr conf.d/
   29  ls -ltr sites-enabled/
   30  cat /etc/nginx/sites-available/default 
   31  vi /etc/nginx/sites-available/default
   32  cat /etc/nginx/sites-available/default 
   33  sed -n '/listen 80 default_server;/p'
   34  sed -n '/listen 80 default_server;/p' /etc/nginx/sites-available/default 
   35  sed -n 's/listen 80 default_server;/listen 7777 default_server;/p' /etc/nginx/sites-available/default 
   36  sed -i 's/listen 80 default_server;/listen 7777 default_server;/p' /etc/nginx/sites-available/default 
   37  sudo sed -i 's/listen 80 default_server;/listen 7777 default_server;/p' /etc/nginx/sites-available/default 
   38  sudo systemctl restart nginx.service 
   39  systemctl status nginx.service 
   40  cat /etc/nginx/nginx.conf
   41  cat /etc/nginx/nginx.conf | grep 7777
   42  systemctl status nginx.service 
   43  cat /etc/nginx/sites-enabled/default:23
   44* 
   45  grep -n '7777' /etc/nginx/sites-enabled/default
   46  sudo sed -i '22d' /etc/nginx/sites-enabled/default 
   47  grep -n '7777' /etc/nginx/sites-enabled/default 
   48  sudo systemctl restart nginx.service 
   49  sudo systemctl status nginx.service 
   50  /home/admin/wtfit
   51  history
```