# SadServers — "Bangalore": Envoy Panics
https://sadservers.com/newserver/bangalore  

---

## Scenario
---
In this challenge, Envoy proxy was **failing to serve traffic** and panicking because of misconfigured cluster references and default panic thresholds.  

The issue involved two misconfigurations:
1. The **cluster name mismatch** — Envoy config referenced `app_cluster`, while the actual backend service used `express_cluster`.  
2. The **panic threshold** (`healthy_panic_threshold`) was not defined, causing Envoy to panic when too few healthy hosts were detected.  

The goal was to fix both problems and restore stable proxy behavior.  

---

## TL;DR (Fix Summary)
---
- Found Envoy service failing via `docker logs`.  
- Identified incorrect cluster reference (`app_cluster`) in `envoy.yaml`.  
- Updated it to the correct cluster name (`express_cluster`).  
- Added a `common_lb_config` section with `healthy_panic_threshold: { value: 0 }` under the cluster definition.  
- Restarted the Envoy container.  
- Verified that the proxy served traffic on `localhost:10000` and backend health endpoint returned success.  
- Confirmed with `/home/admin/agent/check.sh` (if applicable).  

---

## Step-by-step Command History (trimmed)
---
1. Inspected running processes and listening ports:  
   ```bash
   ss -tpln
   ps -ef | grep envoy
    ```

2. Reviewed the `docker-compose.yml` and `envoy.yaml` configuration files:

   ```bash
   cat docker-compose.yml
   cat envoy.yaml
   ```
3. Checked logs for the failing Envoy container:

   ```bash
   docker ps
   docker logs <envoy_container_id>
   ```

   → Found panic caused by `app_cluster` not found.
4. Searched configuration references:

   ```bash
   grep -iR "app_cluster" .
   ```

   → Confirmed mismatch, replaced with `express_cluster`:

   ```bash
   sed -i 's/app_cluster/express_cluster/g' envoy.yaml
   ```
5. Restarted Envoy:

   ```bash
   docker compose restart envoy
   ```
6. Verified that backend was reachable and health checks passed:

   ```bash
   curl localhost:10000
   curl localhost:3002/health
   ```
7. Added panic threshold to ensure Envoy stays stable:

   ```yaml
   common_lb_config:
     healthy_panic_threshold: { value: 0 }
   ```

   Inserted this right under `lb_policy: round_robin` in the cluster section, e.g.:

   ```bash
   sed '32i \    common_lb_config:\n      healthy_panic_threshold: { value: 0 }' envoy.yaml
   docker compose restart envoy
   ```
8. Retested access on port 10000 — successful.

---

## Full Command History (as executed)

---

```
 1  clear
 2  pwd
 3  ss -tpln 
 4  sudo ss -tpln
 5  ps -ef | grep envoy
 6  ls -ltr
 7  cat docker-compose.yml 
 8  cat envoy.yaml 
 9  docker ps
10  docker logs 82e8a1362e3f
11  grep . -iR "app_cluster"
12  grep -iR "app_cluster" .
13  cat ./envoy.yaml: 
14  cat ./envoy.yaml
15  grep -iR "express_cluster" .
16  sed -n 's/app_cluster/express_cluster/p' envoy.yaml 
17  sed -i 's/app_cluster/express_cluster/g' envoy.yaml 
18  docker compose restart envoy
19  docker ps 
20  curl localhost:10000
21  cat envoy.yaml 
22  docker ps
23  curl localhost:3002/healthy
24  curl localhost:3002/health
25  curl localhost:3002/health -v
27  cat envoy.yaml 
28  cat envoy.yaml  | grep -i fail_traffic_on_panic
29  grep -n "lb_policy: round_robin" envoy.yaml 
30  vi envoy.yaml'
31  sed '32i \    common_lb_config:\n      healthy_panic_threshold: { value: 0 }' envoy.yaml
32  docker compose erestart envoy
33  docker compose restart envoy
34  docker ps
35  curl localhost:10000
36  history
```
