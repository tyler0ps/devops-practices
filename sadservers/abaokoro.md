## TODO: Write doc

https://sadservers.com/newserver/abaokoro

history
    1  ls
    2  tar -xzf dbs_to_restore.tar.gz first.sql
    3  ls
    4  df -h
    5  ls
    6  cd /
    7  du -h 
    8  du -h  | sort -hk1
    9  du -h  | sort -rhk1
   10  du -h 2>/dev/null | sort -rhk1 2 | head 20
   11  du -h 2>/dev/null | sort -rhk1 2 | head -n20
   12  du -h 2>/dev/null | sort -rhk1 | head -n20
   13  cd ./var/log/custom
   14  ks -ktr
   15  ls -ltr
   16  du -h U
   17  du -h *
   18  rm 2025-06-05.log 
   19  rm 2023-10-07.log 
   20  ls
   21  ls -ltr
   22  df -h
   23  ls -ltr
   24  du -h
   25  df -h
   26* 
   27  tar -xzf  dbs_to_restore.tar.gz 
   28  ls
   29  df -h
   30  du -h *
   31  ls -ltr /var/log/custom
   32  ls
   33  ls -ltr /var/log/custom
   34  du -h /var/log/custom
   35* 
   36  sudo rm -rf /var/log/custom
   37  ls -ltr
   38  tar -xzf  dbs_to_restore.tar.gz 
   39  ls
   40  mysql -u root
   41  sudo systemctl stop mariadb.service 
   42  mysqld_safe 
   43  ls
   44  systemctl status mariadb.service 
   45  mysql -u root
   46  mysqld_safe --skip-grant-tables
   47  sudo mysqld_safe --skip-grant-tables 
   48  mysql -u root
   49  systemctl status mariadb.service 
   50  history

history
    1  mysql -u root
    2  mysql -u root -e "SET PASSWORD FOR root@localhost='';"
    3  mysqladmin -u root ''
    4  mysqladmin -u root -ppass ''
    5  sudo mysql -u root -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'yourpasswd';
'
    6  sudo mysql -u root -e "ALTER USER \'root\'@\'localhost\' IDENTIFIED BY \'\'"
    7  sudo mysql -u root
    8  ps -ef | grep mysql
    9  kill -9 1512
   10  clear
   11  sudo systemctl restart mariadb.service 
   12  mysql -u root
   13  ls
   14  df -h
   15  mysql -u root -e 'CREATE DATABASE first;'
   16  sudo mysql -u first < first.sql ;
   17  sudo mysql -u root first < first.sql ;
   18  mysql -u root -e 'CREATE DATABASE second;'
   19  sudo mysql -u root second < second.sql;
   20  mysql -u root -e 'CREATE DATABASE third;'
   21  sudo mysql -u root third < third.sql 
   22  /home/admin/agent/check.sh
   23  history