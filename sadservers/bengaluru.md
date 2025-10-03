# SadServers — Bengaluru  
https://sadservers.com/scenario/bengaluru  

---

## Scenario
---
The task highlights one of the **least known characteristics of Kubernetes StatefulSets**:  
- Unlike Deployments, StatefulSets **do not automatically reschedule pods** to other nodes when the current node becomes unreachable.  
- This behavior can cause pods to remain stuck in `Terminating` or `Unknown` state if their original node goes down, unless explicitly deleted or restarted.  

The goal was to fix the StatefulSet pods so the application becomes healthy again.  

---

## TL;DR (Fix Summary)
---
- Observed that the node hosting the pod was stopped/unreachable.  
- Verified pod and StatefulSet behavior.  
- Edited the StatefulSet to remove unnecessary tolerations.  
- Restarted the StatefulSet rollout.  
- Deleted the stuck pod (`demo-statefulset-0`) so Kubernetes could recreate it on a healthy node.  

---

## Step-by-step Command History (trimmed)
---
1. Checked running containers with Docker (`docker ps`).  
2. Listed nodes and inspected the problematic node:  
   ```bash
   k get nodes
   k get nodes k3d-mycluster-agent-0 -oyaml
   ```

3. Simulated node failure by stopping it:

   ```bash
   docker stop k3d-mycluster-agent-0
   ```
4. Looked into taints and tolerations (`k taints`, `k taint --help`).
5. Inspected StatefulSet spec:

   ```bash
   k get sts demo-statefulset -oyaml
   k edit sts demo-statefulset
   ```

   → Removed tolerations for `unreachable`, `notready`, etc.
6. Restarted StatefulSet pods:

   ```bash
   k rollout restart sts demo-statefulset
   ```
7. Manually deleted the stuck pod to trigger rescheduling:

   ```bash
   k delete pod demo-statefulset-0
   kubectl delete pod demo-statefulset-0 --grace-period=0 --force
   ```

---

## Full Command History (as executed)

---

```
 1  docker ps
 2  k get nodes
 3  k get nodes k3d-mycluster-agent-0 -oyaml
 4  docker stop k3d-mycluster-agent-0
 5  k taints 
 6  k taint --help
 7  k taint node --help
 8  k get nodes
 9  k get pods
10  k get sts demo-statefulset -oyaml # remove tolerances unreachable, notready, ...
11  k edit sts demo-statefulset
12  k get pods 
13  k get pods
14  k rollout restart sts demo-statefulset
15  k delete pod demo-statefulset-0 
16  kubectl delete pod demo-statefulset-0 --grace-period=0 --force
17  /home/admin/agent/check.sh
18  history
```