# SadServers — "Quito": Control One Container from Another
https://sadservers.com/newserver/quito  

---

## Scenario
---
This challenge demonstrates **how to control Docker from within another container** — i.e., managing Docker from inside a container by mounting the host’s Docker socket.  

By default, containers are isolated and cannot access Docker commands or control other containers.  
To achieve this, you need to **mount the host’s `/var/run/docker.sock` socket** into the target container so that Docker commands run inside it actually interact with the host’s Docker daemon.  

---

## TL;DR (Fix Summary)
---
- Inspected running containers (`docker ps`).  
- Launched a container named `docker-access` with the host’s Docker socket mounted:  
  ```bash
  docker run -it -v /var/run/docker.sock:/var/run/docker.sock --name docker-access docker-access
  ```

* Entered the `docker-access` container shell.
* Confirmed that Docker commands inside the container (`docker ps`, `docker restart <id>`) now controlled host containers.
* Verified functionality with `/home/admin/agent/check.sh`.

---

## Step-by-step Command History (trimmed)

---

1. Checked containers and verified the presence of the `docker-access` image:

   ```bash
   docker ps -a
   ```
2. Started a container with **Docker socket mounted** to the host:

   ```bash
   docker run -it -v /var/run/docker.sock:/var/run/docker.sock --name docker-access docker-access
   ```

   > This grants the container permission to run `docker` commands directly on the host.
3. Executed shell access inside the container:

   ```bash
   docker exec -it docker-access sh
   ```
4. Inside the container, confirmed host-level Docker control:

   ```bash
   docker ps
   docker restart <container_id>
   ```
5. Returned to the host and validated the setup:

   ```bash
   docker exec docker-access docker ps
   /home/admin/agent/check.sh
   ```

---

## Full Command History (Host)

---

```
 1  ls
 2  docker ps
 3  docker ps -a
 4  docker restart docker-access 
 5  docker exec -it 1566600ac41c 
 6  docker exec -it 1566600ac41c  sh
 7  ls
 8  docker ps
 9  docker run -it -v /var/run/docker.sock:/var/run/docker.sock docker-access
10  docker stop docker-access
11  docker run -it -v /var/run/docker.sock:/var/run/docker.sock docker-access --name docker-access
12  docker run -it -v /var/run/docker.sock:/var/run/docker.sock --name docker-access docker-access 
13  docker rm docker-access
14  docker run -it -v /var/run/docker.sock:/var/run/docker.sock --name docker-access docker-access 
15  history
16  docker exec docker-access docker ps
17  docker run -v /var/run/docker.sock:/var/run/docker.sock --name docker-access docker-access 
18  docker start docker-access
19  docker ps
20  /home/admin/agent/check.sh
21  history
```

## Full Command History (Inside docker-access container)

---

```
 0  docker ps
 1  docker ps -a
 2  docker restart 6d07db770d87
 3  docker ps
 4  history
```
