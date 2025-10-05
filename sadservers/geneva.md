# SadServers — "Geneva": Renew an SSL Certificate

[https://sadservers.com/scenario/geneva](https://sadservers.com/scenario/geneva)

---

## Scenario

---

Nginx’s HTTPS endpoint was using an **expired/invalid certificate**.
Goal: find the active cert path used by Nginx, **issue a fresh self-signed cert** with the existing private key, replace the old cert, and restart Nginx so TLS works again.

---

## TL;DR (Fix Summary)

---

* Searched Nginx configs to locate the active TLS cert/key paths.
* Confirmed cert status via `openssl s_client`.
* Generated a new self-signed cert using the existing key:

  ```bash
  sudo openssl req -x509 -new -nodes -key /etc/nginx/ssl/nginx.key -sha256 -days 365 -out /etc/nginx/ssl/nginx2.crt
  ```
* Replaced `nginx.crt` with the new cert and **restarted Nginx**.
* Verified with the agent script.

---

## Step-by-step Command History (trimmed)

---

1. Checked HTTPS and inspected cert details from the running service:

   ```bash
   curl -v https://localhost
   echo | openssl s_client -connect localhost:443 2>/dev/null | openssl x509 -noout -dates
   echo | openssl s_client -connect localhost:443 2>/dev/null | openssl x509 -noout -text
   ```
2. Located Nginx TLS configuration and cert/key paths:

   ```bash
   cat /etc/nginx/nginx.conf
   find /etc/nginx -type f -name "*.conf" -exec cat {} \; | egrep -i "ssl|crt|key"
   # Found /etc/nginx/ssl/nginx.crt and /etc/nginx/ssl/nginx.key
   ```
3. Generated a new self-signed certificate with the **existing key**:

   ```bash
   sudo openssl req -x509 -new -nodes -key /etc/nginx/ssl/nginx.key -sha256 -days 365 -out /etc/nginx/ssl/nginx2.crt
   ```
4. Replaced the live certificate and restarted Nginx:

   ```bash
   sudo mv /etc/nginx/ssl/nginx2.crt /etc/nginx/ssl/nginx.crt
   sudo systemctl restart nginx.service
   ```
5. Verified:

   ```bash
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  curl https//localhost
 2  curl https://localhost -v
 3  find /etc/ -type f -name "*nginx.conf"
 4  cat /etc/nginx/nginx.conf
 5  find /etc/nginx -type f -name "*.conf"
 7  find /etc/nginx -type f -name "*.conf" -exec realpath {} \; | cat | grep -i "crt"
 8  find /etc/nginx -type f -name "*.conf" -exec realpath {} \; | cat
 9  find /etc/nginx -type f -name "*.conf" -exec realpath {} \; | cat | xargs grep -i "crt" $0
10  find /etc/nginx -type f -name "*.conf" -exec cat {} \;
11  find /etc/nginx -type f -name "*.conf" -exec cat {} \; | egrep -i "ssl|crt|prm|key"
12  cat /etc/ssl/certs/ssl-cert-snakeoil.pem
13  cat /etc/ssl/certs/ssl-cert-snakeoil.pem
14  find /etc/nginx -type f -name "*.conf" -exec cat {} \; | egrep -i "ssl"
15  echo | openssl s_client -connect localhost:443 2>/dev/null | openssl x509 -noout -dates
16  echo | openssl s_client -connect localhost:443 2>/dev/null | openssl x509 -noout -text
17  find /etc/nginx -type f -name "*.conf"
18  find /etc/ -type f -name "*.conf"
19  find /etc/ -type f -name "*.conf" | grep nginx
20  cat /etc/nginx/nginx.conf
21  cd /etc/nginx/modules-enabled/
22  ls -ltr
23  cd ..
24  ls
25  cd ssl/
26  ls
27  cd ..
28  ls
29  grep . -iR "nginx.crt"
30  grep -iR "nginx.crt" .
31  cat nginx.crt
32  cat /etc/nginx/ssl/nginx.crt
33  openssl x509 -noout -subject -issuer
34  openssl x509 -noout -subject -issuer /etc/nginx/ssl/nginx.crt
35  openssl x509 -noout -subject -issuer -in /etc/nginx/ssl/nginx.crt
36  sudo openssl req -x509 -new -nodes -key /etc/nginx/ssl/nginx.key -sha256 -days 365 -out /etc/nginx/ssl/nginx2.crt
37  ls
38  cd ssl/
39  ls
40  mv nginx2.crt nginx.crt
41  ls -ltr
42  rm nginx.crt
43  sudo rm nginx.crt
44  sudo mv nginx2.crt nginx.crt
45  sudo systemctl restart nginx.service
46  /home/admin/agent/check.sh,
47  /home/admin/agent/check.sh
48  history
```
