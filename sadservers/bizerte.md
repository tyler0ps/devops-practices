# SadServers — "Bizerte": The Slow Application

[https://sadservers.com/newserver/bizerte](https://sadservers.com/newserver/bizerte)

---

## Scenario

---

A web application (`slow_app.py`) was running slowly because it couldn’t properly connect to its Redis backend.
The systemd service `slow-app.service` defined the environment variable `REDIS_HOST` incorrectly as `127.0.0.2` instead of `127.0.0.1`.
The goal was to locate and fix this configuration so the application connects successfully to Redis and responds on port `5000`.

---

## TL;DR (Fix Summary)

---

* Found that `slow_app.py` used the `REDIS_HOST` environment variable.
* Checked environment and saw `REDIS_HOST=127.0.0.2`.
* Updated `/etc/systemd/system/slow-app.service` to use `127.0.0.1`.
* Reloaded systemd configuration and restarted the service.
* Verified that the app was reachable via `curl localhost:5000`.
* Confirmed with `/home/admin/agent/check.sh`.
 
---

## Step-by-step Command History (trimmed)

---

1. Checked network listening ports and running processes:

   ```bash
   sudo ss -tpln
   ps -ef | grep 823
   ```
2. Inspected application code and environment variable:

   ```bash
   cat /opt/slow_app.py
   env | grep REDIS_HOST
   ```

   → Found `REDIS_HOST=127.0.0.2`.
3. Verified systemd service configuration:

   ```bash
   systemctl status slow-app.service
   systemctl cat slow-app.service | grep -i env
   ```
4. Edited the service file to fix the Redis host IP:

   ```bash
   sudo sed -i 's/127.0.0.2/127.0.0.1/p' /etc/systemd/system/slow-app.service
   ```
5. Reloaded and restarted the service:

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl restart slow-app.service
   systemctl status slow-app.service
   ```
6. Verified that the web app responds:

   ```bash
   curl localhost:5000
   ```
7. Ran check script:

   ```bash
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  ss -tpln 
 2  sudo ss -tpln 
 3  ps -ef | grep pid=823
 4  ps -ef | grep 823
 5  cat /opt/slow_app.py
 6  env | grep REDIS_HOST
 7  export REDIS_HOST=127.0.0.1
 8  curl localhost:5000
 9  systemctl status slow-app.service 
10  systemctl cat slow-app.service
11  systemctl cat slow-app.service | grep -i envi
12  sed -n 's/127.0.0.2/127.0.0.1/p' /etc/systemd/system/slow-app.service
13  sed -i 's/127.0.0.2/127.0.0.1/p' /etc/systemd/system/slow-app.service
14  sudo sed -i 's/127.0.0.2/127.0.0.1/p' /etc/systemd/system/slow-app.service
15  sudo systemctl restart slow-app.service 
16  systemctl daemon-reload
17  sudo systemctl daemon-reload
18  sudo systemctl restart slow-app.service 
19  systemctl status slow-app.service
20  /home/admin/agent/check.sh
21  history
```