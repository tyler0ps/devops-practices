# SadServers — Bucharest

[https://sadservers.com/scenario/bucharest](https://sadservers.com/scenario/bucharest)

---

## Scenario

---

Local PostgreSQL connections for database `app1` (user `app1user`) were being **rejected** due to `pg_hba.conf` rules.
The fix is to change the relevant rule from `reject` to `md5` authentication and restart PostgreSQL so the user can connect with a password.

---

## TL;DR (Fix Summary)

---

* Located the active `pg_hba.conf`.
* Replaced the offending `reject` rule with `md5`.
* Restarted PostgreSQL (`postgresql@13-main.service`).
* Verified connection using:

  ```bash
  PGPASSWORD=app1user psql -h 127.0.0.1 -d app1 -U app1user -c '\q'
  ```

---

## Step-by-step Command History (trimmed)

---

1. Tested connection (failed due to auth):

   ```bash
   PGPASSWORD=app1user psql -h 127.0.0.1 -d app1 -U app1user -c '\q'
   ```
2. Reviewed Postgres configs and located `pg_hba.conf`:

   ```bash
   systemctl status postgresql@13-main.service
   sudo find / -type f -name 'pg_hba.conf'
   sudo cat /etc/postgresql/13/main/pg_hba.conf
   ```
3. Switched the rule from `reject` → `md5`:

   ```bash
   sudo sed -i 's/    reject/    md5/g' /etc/postgresql/13/main/pg_hba.conf
   ```
4. Restarted PostgreSQL and re-tested:

   ```bash
   sudo systemctl restart postgresql@13-main.service
   PGPASSWORD=app1user psql -h 127.0.0.1 -d app1 -U app1user -c '\q'
   ```

---

## Full Command History (as executed)

---

```
 1  PGPASSWORD=app1user psql -h 127.0.0.1 -d app1 -U app1user -c '\q'
 2  cat pg_hba.conf
 3  systemctl status postgresql
 4  systemctl status postgresql@13-main.service 
 5  cat /etc/postgresql/13/main/postgresql.conf
 6  cat /etc/postgresql/13/main/postgresql.conf | grep -i app1
 7  PGPASSWORD=app1user psql -h 127.0.0.1 -d app1 -U app1user -c '\q' 
 8  cat /etc/postgresql/13/main/postgresql.conf | grep -i app
 9  cat /etc/postgresql/13/main/postgresql.conf | grep -i ssl
10  find . -type f -name 'pg_hba.conf'
11  cd /
12  find . -type f -name 'pg_hba.conf'
13  sudo find . -type f -name 'pg_hba.conf'
14  cat ./etc/postgresql/13/main/pg_hba.conf
15  sudo cat ./etc/postgresql/13/main/pg_hba.conf
16  sudo cat ./etc/postgresql/13/main/pg_hba.conf | grep app
17  sudo cat ./etc/postgresql/13/main/pg_hba.conf | grep rect
18  sudo cat ./etc/postgresql/13/main/pg_hba.conf | grep reject
19  sudo sed -n 's/    reject/    md5/p' ./etc/postgresql/13/main/pg_hba.conf
20  sudo sed -i 's/    reject/    md5/g' ./etc/postgresql/13/main/pg_hba.conf
21  systemctl restart postgresql
22  sudo systemctl restart postgresql
23  sudo systemctl restart postgresql@13-main.service 
24  PGPASSWORD=app1user psql -h 127.0.0.1 -d app1 -U app1user -c '\q'
25  history
```
