## Scenario
https://sadservers.com/newserver/rosario

You’re dropped on a host with MariaDB running. There’s a SQL dump (`backup.sql`) that fails to import due to syntax errors. You need to restore it so a checker script passes.

The host is limited (no internet, minimal tools). You have `sudo`.

---

## TL;DR (Fix Summary)

1. Stop the system service and start `mysqld` in a permissive mode to get access.
2. Import fails because the dump has **`/*! ... */?`** (a `?` instead of `;`) in versioned comment directives.
3. Normalize those **`?` → `;`** endings (carefully).
4. Ensure we’re writing into the **correct database** by adding `USE main;`.
5. Re-import and run the checker.

---

## Full Command History (as executed)

```bash
1  sudo systemctl stop mariadb.service
2  sudo mysqld --skip-grant-tables &
3  sudo mysqldump -u root main > sample_backup.sql
4  cat sample_backup.sql
5  sudo mysql -u root < backup.sql 
6  sed -i 's/*\/?/*\/;/g' backup.sql 
7  sudo mysql -u root < backup.sql 
8  grep -i '?' backup.sql 
9  sed -i 's/?/;/g' backup.sql 
10 sudo mysql -u root < backup.sql 
11 sed -n '22p' backup.sql 
12 sed '22i hello' backup.sql 
13 sed -i '22i USE main;' backup.sql 
14 sudo mysql -u root < backup.sql 
15 /home/admin/agent/check.sh
16 history
```
