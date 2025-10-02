# SadServers “Moyogalpa” – Security Snag (permissions, TLS & AppArmor)
[https://sadservers.com/newserver/moyogalpa](https://sadservers.com/newserver/moyogalpa)

---

## Scenario

A Golang web app must serve static files over **HTTPS** and pass client verification. The success test is that `curl https://webapp:7000/users.html` returns the file contents without bypassing TLS checks (after the CA is trusted on the client). ([sadservers.com][1])

---

## TL;DR (Fix Summary)

* **Fix file & directory permissions** so the `webapp` process can *traverse directories* and *read the file*:

  * `chown -R webapp:webapp /home/webapp/static-files`
  * `chmod 750 /home/webapp/static-files` (and ensure **x** on each parent dir)
  * `chmod +r /home/webapp/static-files/users.html`
* **Lock down certs** to be readable by the service:

  * `chown root:webapp /home/webapp/pki/server.{crt,pem}`
  * `chmod 640 /home/webapp/pki/server.{crt,pem}`
* **Trust the CA** on the host doing `curl`:

  * `cp /home/webapp/pki/CA.crt /usr/local/share/ca-certificates/ && update-ca-certificates --fresh`
* **Ensure name resolution** for the host `webapp` (add to `/etc/hosts` if needed).
* **AppArmor**: profile was blocking reads; switch to *complain* (quick fix) or update the profile to allow `/home/webapp/static-files/**` and `/home/webapp/pki/*`:

  * `aa-status`, `journalctl -k | grep -i DENIED` to confirm
  * `sudo aa-complain /usr/local/bin/webapp`
* **Restart & verify**: `systemctl restart webapp` → `curl https://webapp:7000/users.html` (should succeed). ([sadservers.com][1])

---

## Step-by-step Command History (trimmed)

> The essentials only, grouped by task.

### 1) Inspect service & errors

```bash
systemctl status webapp
journalctl -u webapp -n200
aa-status
journalctl -k | grep -i DENIED
systemctl show webapp -p ProtectHome,ProtectSystem,DynamicUser,RootDirectory,ReadOnlyPaths,ReadWritePaths,PrivateTmp
```

### 2) Check path traversal & permissions

```bash
ls -ld /home /home/webapp /home/webapp/static-files /home/webapp/static-files/users.html
namei -l /home/webapp/static-files/users.html
getfacl /home /home/webapp /home/webapp/static-files /home/webapp/static-files/users.html
```

### 3) Fix static-file perms

```bash
chown -R webapp:webapp /home/webapp/static-files
chmod 750 /home/webapp/static-files
chmod +r /home/webapp/static-files/users.html   # file must be readable
# (If any parent dir lacked 'x', add it)
chmod +x /home/webapp/static-files
```

### 4) Fix certificate perms for the service

```bash
chown root:webapp /home/webapp/pki/server.crt
chown root:webapp /home/webapp/pki/server.pem
chmod 640 /home/webapp/pki/server.crt
chmod 640 /home/webapp/pki/server.pem
```

### 5) Trust CA & hostname for curl

```bash
cp /home/webapp/pki/CA.crt /usr/local/share/ca-certificates/
update-ca-certificates --fresh
# ensure /etc/hosts contains a line mapping 'webapp' -> local IP
vi /etc/hosts
```

### 6) AppArmor (quick unblock or proper allow-list)

```bash
aa-status
sudo aa-complain /usr/local/bin/webapp    # quick unblock during troubleshooting
# (Long-term: adjust /etc/apparmor.d/local/usr.local.bin.webapp to allow needed paths)
```

### 7) Restart & verify

```bash
systemctl restart webapp
curl https://webapp:7000/users.html
```

---

## Full Command History (as executed)

**Session 1**

```bash
1  ls -ltr
2  cd ../
3  ls -ltr
4  cd webapp/
5  ls -ltr
6  cd pki/
7  sudo chmod +r pki/
8  cd pki/
9  ls
10 ls -ld pki/
11 sudo cd pki/
12 ls
13 cd pki/
14 sudo cd pki
15 ls -ltr pki/
16 cd pki/
17 sudo cd pki/
18 sudo ls pki/
19 ls
20 sudo chmod +xr pki/server.crt pki/server.pem
21 ls -ltr pki/ 
22 env APP_STATIC_DIR='/home/webapp/static-files' APP_CERT='/home/webapp/pki/server.crt' APP_KEY='/home/webapp/pki/server.pem' /usr/local/bin/webapp
23 sudo chown webapp:webapp pki pki/*
24 ls
25 ls -ltr
26 APP_STATIC_DIR='/home/webapp/static-files' APP_CERT='/home/webapp/pki/server.crt' APP_KEY='/home/webapp/pki/server.pem' /usr/local/bin/webapp
27 cd pki/
28 ls
29 su -
30 sudo -s
31 history
```

**Session 2**

```bash
1  ls
2  ls -ltr
3  cd pki/
4  ls
5  cd ..
6  env APP_STATIC_DIR='/home/webapp/static-files' APP_CERT='/home/webapp/pki/server.crt' APP_KEY='/home/webapp/pki/server.pem' /usr/local/bin/webapp
7  systemctl status web
8  systemctl status webapp
9  systemctl edit webapp
10 systemctl cat webapp
11 chown -R webapp:webapp /home/webapp/static-files
12 chmod -R 750 /home/webapp/static-files
13 chown root:webapp /home/webapp/pki/server.crt
14 chown root:webapp /home/webapp/pki/server.key
15 chmod 640 /home/webapp/pki/server.crt
16 chown root:webapp /home/webapp/pki/server.pem
17 chmod 640 /home/webapp/pki/server.pem
18 id webapp
19 systemctl restart webapp
20 systemctl status webapp
21 curl https://webapp:7000/users.html
22 cat /etc/hosts
23 vi /etc/hosts
24 curl https://webapp:7000/users.html
25 ls
26 cd pki/
27 ls
28 cp CA.crt /usr/local/share/ca-certificates/
29 update-ca-certificates --fresh
30 curl https://webapp:7000/users.html
31 journalctl -u webapp
32 journalctl -u webapp -n200
33 journalctl -u webapp | tail -n50
34 ls -ld /home/webapp/static-files/users.html:
35 ls -ld /home/webapp/static-files/users.html
36 ls -ld /home/webapp/static-files
37 ls -ld /home/webapp/
38 ls -ld /home/webapp
39 ls -ld /home/
40 namei -l /home/webapp/static-files/users.html
41 # hoặc
42 ls -ld /home /home/webapp /home/webapp/static-files /home/webapp/static-files/users.html
43 namei -l /home/webapp/static-files/users.html
44 namei --help
45 namei -l /home/webapp/static-files/users.html
46 getfacl /home /home/webapp /home/webapp/static-files /home/webapp/static-files/users.html
47 systemctl cat webapp | sed -n '/\[Service\]/,/^\[/p'
48 systemd-analyze cat-config webapp.service | sed -n '/\[Service\]/,/^\[/p'
49 systemctl show webapp -p ProtectHome,ProtectSystem,DynamicUser,RootDirectory,ReadOnlyPaths,ReadWritePaths,PrivateTmp
50 ls -ld /home /home/webapp /home/webapp/static-files /home/webapp/static-files/users.html
51 chmod +x /home/webapp/static-files
52 ls -ld /home/webapp/static-files
53 chmod +x /home/webapp/static-files/users.html
54 ls -ld /home/webapp/static-files/users.html
55 systemctl restart webapp
56 curl https://webapp:7000/users.html
57 journalctl -u webapp | tail -n50
58 cat /home/webapp/static-files/users.html:
59 cat /home/webapp/static-files/users.html
60 systemctl cat webapp
61 clear
62 aa-status
63 journalctl -k | grep -i DENIED
64 ls -ld /home/webapp/static-files/users.html
65 chmod +r /home/webapp/static-files/users.html
66 ls -ld /home/webapp/static-files/users.html
67 curl https://webapp:7000/users.html
68 aa-status
69 journalctl -k | grep -i DENIED
70 ls -ld /home/webapp/static-files/users.html
71 systemctl show webapp -p ProtectHome,ProtectSystem,DynamicUser,RootDirectory,ReadOnlyPaths,ReadWritePaths,PrivateTmp
72 sudo aa-complain /usr/local/bin/webapp
73 sudo systemctl restart webapp
74 curl https://webapp:7000/users.html
75 history
```

---
