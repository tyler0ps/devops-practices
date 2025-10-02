# SadServers — "Helsingør": The first walls of postgres physical replication
https://sadservers.com/newserver/helsingor  

---

## Scenario
---
The PostgreSQL replica container was failing due to insufficient configuration parameters in `postgres.conf`.  
Several resource limits, preventing the database from operating correctly under load.  

The goal was to identify and update these PostgreSQL settings, then restart the container to restore proper functionality.  

---

## TL;DR (Fix Summary)
---
- Inspected `docker-compose.yml` and Postgres replica configuration.  
- Located `postgres.conf` inside `./postgres/replica/`.  
- Updated key parameters with `sed`:
  - `max_connections = 100`  
  - `max_worker_processes = 8`  
  - `max_wal_senders = 10`  
  - `max_locks_per_transaction = 64`  
- Restarted the Postgres container (`docker restart <container_id>`).  
- Verified logs until the service came up cleanly.  
- Confirmed success with `/home/admin/agent/check.sh`.  

---

## Step-by-step Command History (trimmed)
---
1. Checked running containers with `docker ps`.  
2. Reviewed `docker-compose.yml` to locate Postgres setup.  
3. Inspected logs of the failing container (`docker logs <id>`).  
4. Opened and searched inside `./postgres/replica/postgres.conf`.  
5. Applied `sed -i` edits to increase limits:
   - `max_connections` → 100  
   - `max_worker_processes` → 8  
   - `max_wal_senders` → 10  
   - `max_locks_per_transaction` → 64  
6. Restarted the container after each change (`docker restart <id>`).  
7. Monitored logs (`docker logs <id> | tail -50`).  
8. Final verification with `/home/admin/agent/check.sh`.  

---

## Full Command History (as executed)

```bash

1  /home/admin/agent/check.sh
2  docker ps
3  docker compose ls
4  cat /home/admin/docker-compose.yml
5  docker ps
6  docker logs 98e1b8d4a341
7  docker compose ls
8  cat /home/admin/docker-compose.yml | awk '.conf'
9  cat /home/admin/docker-compose.yml | awk '.conf'
10  cat /home/admin/docker-compose.yml | awk '/.conf/'
11  cat ./postgres/replica/postgres.conf
12  cat ./postgres/replica/postgres.conf | grep max
13  cat ./postgres/replica/postgres.conf | grep 80
14  sed -n 's/max_connections = 80/max_connections = 100/' ./postgres/replica/postgres.conf
15  sed 's/max_connections = 80/max_connections = 100/' ./postgres/replica/postgres.conf
16  sed 's/max_connections = 80/max_connections = 100/' ./postgres/replica/postgres.conf | sed -n '100'
17  sed 's/max_connections = 80/max_connections = 100/' ./postgres/replica/postgres.conf | sed -n '/100/'
18* sed 's/max_connections = 80/max_connections = 100/' ./postgres/replica/postgres.co
19  sed -n 's/max_connections = 80/max_connections = 100/' ./postgres/replica/postgres.conf
20  sed -n 's/max_connections = 80/max_connections = 100/p' ./postgres/replica/postgres.conf
21  sed -i 's/max_connections = 80/max_connections = 100/p' ./postgres/replica/postgres.conf
22  sed -n 's/max_connections = 80/max_connections = 100/p' ./postgres/replica/postgres.conf
23  clear
24  docker ps
25  docker restart 98e1b8d4a341
26  docker ps
27  docker ps -w
28  watch docker ps
29  docker logs 98e1b8d4a341
30  sed -n 's/max_worker_processes = 4/max_worker_processes = 8/p' ./postgres/replica/postgres.conf
33  docker restart 98e1b8d4a341
34  docker logs 98e1b8d4a341
35  docker logs 98e1b8d4a341 | tail -f -n20
36  docker logs 98e1b8d4a341 | tail  -n20
37  sed -n 's/max_wal_senders = 5/max_wal_senders = 10/p' ./postgres/replica/postgres.conf
38  sed -i 's/max_wal_senders = 5/max_wal_senders = 10/p' ./postgres/replica/postgres.conf
39  docker restart 98e1b8d4a341
40  docker logs 98e1b8d4a341 | tail -50
41  docker p[s
42  docker ps
43  sed -i 's/max_locks_per_transaction = 32/max_locks_per_transaction = 64/p' ./postgres/replica/postgres.conf
44  docker restart 98e1b8d4a341
45  docker ps
46  watch docker ps
47  docker logs 98e1b8d4a341 | tail -50
48  /home/admin/agent/check.sh
49  history
```
---