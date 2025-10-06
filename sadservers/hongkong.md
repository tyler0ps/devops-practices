# "Hong-Kong": can't write data into database.
https://sadservers.com/newserver/hongkong

```bash
sed -i '/^data_directory/d' /etc/postgresql/14/main/postgresql.conf 
sed -i 's/#data_directory/data_directory/' /etc/postgresql/14/main/postgresql.conf 
systemctl restart postgresql.service
sudo sudo -u postgres createdb dt
sudo -u postgres psql -d dt -c "CREATE TABLE IF NOT EXISTS persons (
  id BIGSERIAL PRIMARY KEY,
  name TEXT NOT NULL
);"
sudo -u postgres psql -c "insert into persons(name) values ('jane smith');" -d dt
```

## Full CMD history
```bash
    1  exit
    2  sudo -u postgres psql -c "insert into persons(name) values ('jane smith');" -d dt
    3  docker ps
    4  ls
    5  whoami
    6  ps
    7  ps -r
    8  ps -ef
    9  echo $0
   10  systemctl status postgres
   11  systemctl status postgresql
   12  journalctl -u postgresql.service 
   13  systemctl list-units --type=service
   14* 
   15  journalctl -u postgresql@14-main.service
   16  journalctl -u postgresql@14-main.service --no-pager
   17  ls -ld /opt/pgdata/main
   18  ls -ltr /opt/pgdata/main
   19  systemctl status /etc/postgresql/14/main/postgresql.conf
   20  cat /etc/postgresql/14/main/postgresql.conf
   21  cat /etc/postgresql/14/main/postgresql.conf | grep -i data
   22  /opt/pgdata/main
   23  mkdir -p /opt/pgdata/main
   24  cat /etc/postgresql/14/main/postgresql.conf | grep -i data
   25  cat /etc/postgresql/14/main/postgresql.conf | grep -i data
   26  ls -ltr /var/lib/postgresql/14/main
   27  vi /var/lib/postgresql/14/main 
   28  cat /etc/postgresql/14/main/postgresql.conf | grep -iE '^#data_directory'
   29  df -h /opt/
   30  df -h /var/
   31  sed -n 's/#data_directory/data_directory/p' /etc/postgresql/14/main/postgresql.conf 
   32  sed -i 's/#data_directory/data_directory/' /etc/postgresql/14/main/postgresql.conf 
   33  cat /etc/postgresql/14/main/postgresql.conf 
   34  cat /etc/postgresql/14/main/postgresql.conf | grep -n 'data'
   35* 
   36* 
   37  history
   38  systemctl status /etc/postgresql/14/main/postgresql.conf
   39  clear
   40  systemctl list-units --type=service
   41  systemctl restart postgresql.service
   42  systemctl status postgresql.service
   43  systemctl status postgresql@14-main.service
   44  sudo -u postgres psql -c "insert into persons(name) values ('jane smith');" -d dt
   45  sudo -u postgres createdb dt
   46  sudo -u postgres psql -d dt -c "CREATE TABLE IF NOT EXISTS persons (
  id BIGSERIAL PRIMARY KEY,
  name TEXT NOT NULL
);"
   47  sudo -u postgres psql -c "insert into persons(name) values ('jane smith');" -d dt
   48  history
```