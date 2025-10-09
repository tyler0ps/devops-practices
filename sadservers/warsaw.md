## TODO: Write doc
https://sadservers.com/newserver/warsaw

```bash
OKadmin@i-01da9d81ae6851a35:~/app$ history
    1  clear
    2  curl  http://localhost:9000/metrics
    3  vurl -v  http://localhost:9000/metrics
    4  curl -v  http://localhost:9000/metrics
    5  ls -ltr
    6  cd app/
    7  ls -ltr
    8  cat docker-compose.yaml 
    9  cat prometheus.yml 
   10  cat go.sum 
   11  cat main.go
   12  grep -io POST main.go
   13  sed -i 's/POST/GET/' main.go
   14  cat Dockerfile.app 
   15  cat docker-compose.yaml 
   16  cat prometheus.yml 
   17  grep -io '8000' prometheus.yml 
   18  grep -io 'golang' prometheus.yml 
   19  grep -io '8000' prometheus.yml 
   20  sed -i 's/8000/9000/' prometheus.yml 
   21  docker compose ls
   22  docker compose up -d --build 
   23  http://localhost:9000/metrics
   24  curl http://localhost:9000/metrics
   25  clear
   26  cat /home/admin/agent/check.sh
   27  /home/admin/agent/check.sh
   28  history
```