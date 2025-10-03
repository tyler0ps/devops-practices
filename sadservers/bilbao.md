# SadServers — "Bilbao": Basic Kubernetes Problems
https://sadservers.com/newserver/bilbao  

---

## Scenario
---
The application (nginx deployment) was not coming up correctly due to incorrect **resource requests/limits** and unnecessary **tolerations** defined in the manifest.  
This caused scheduling issues and the pod could not run properly on the available nodes.  

The task was to fix the manifest and redeploy the workload so that the pod starts successfully.  

---

## TL;DR (Fix Summary)
---
- Inspected the failing pod (`nginx-deployment`) and cluster state.  
- Reviewed the `manifest.yml`.  
- Fixed the manifest by:  
  - Removing invalid/unnecessary tolerations.  
  - Updating resource requests and limits to match cluster capacity:  
    - **Requests:** `cpu: 50m`, `memory: 100Mi`  
    - **Limits:** `cpu: 100m`, `memory: 200Mi`  
- Reapplied the manifest.  
- Verified pod scheduling and successful service response using `curl`.  
- Confirmed correctness with `/home/admin/agent/check.sh`.  

---

## Step-by-step Command History (trimmed)
---
1. Checked current state with the provided script:  
   ```bash
   /home/admin/agent/check.sh
    ```

2. Looked at pod details and cluster info:

   ```bash
   k get pods
   k describe pod nginx-deployment-67699598cc-zrj6f
   k get nodes
   k get svc
   ```
3. Opened and inspected the workload manifest:

   ```bash
   cat manifest.yml
   vi manifest.yml
   ```
4. Modified the manifest → removed tolerations and set correct resource requests/limits.
5. Applied the fixed manifest:

   ```bash
   k apply -f manifest.yml
   ```
6. Watched pods come up and tested service accessibility:

   ```bash
   k get pods -w
   curl 10.43.216.196
   ```
7. Verified solution with check script:

   ```bash
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  /home/admin/agent/check.sh
 2  cat /home/admin/agent/check.sh
 3  curl 10.43.216.196
 4  k get pods
 5  kubectl get pods
 6  alias k=kubectl
 7  k describe pod nginx-deployment-67699598cc-zrj6f 
 8  k get nodes
 9  k get svc
10  ls
11  ls -ltr
12  cat manifest.yml 
13  vi manifest.yml 
14  k apply -f manifest.yml # remove tolerance, update resources request to 50m/100Mi and limit 100m/200Mi
15  k get pods -w
16  curl 10.43.216.196
17  /home/admin/agent/check.sh
18  history
```
