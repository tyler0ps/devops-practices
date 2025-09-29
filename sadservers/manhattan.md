https://sadservers.com/scenario/manhattan

systemctl list-units --type=service
journalctl -u postgresql@14-main.service --no-pager -n200 | grep -iE 'fatal|error'
df -h /opt/pgdata/main


sudo -u postgres createdb dt
sudo -u postgres psql -d dt -c "CREATE TABLE IF NOT EXISTS persons (
  id BIGSERIAL PRIMARY KEY,
  name TEXT NOT NULL
);"
  
sudo -u postgres psql -c "insert into persons(name) values ('jane smith');" -d dt