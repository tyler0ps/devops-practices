# SadServers — "Budapest": User Creation

[https://sadservers.com/newserver/budapest](https://sadservers.com/newserver/budapest)

---

## Scenario

---

You are given a `user_list.txt` file containing semicolon-separated `username;password` entries and must create those system users on the host.
The task is to parse the input, create each user with a home directory, and set their password so the check script passes.

---

## TL;DR (Fix Summary)

---

* Converted the semicolon-separated list into one-per-line.
* Wrote a small shell script (`script.sh`) that reads each line, parses `username` and `password`, creates the user with `useradd -m`, and sets the password using a hashed value:

  ```sh
  sudo useradd -m $username
  sudo usermod --password $(echo $password | openssl passwd -1 -stdin) $username
  ```
* Iterated (edited and re-ran the script) until all users were created.
* Verified success with `/home/admin/agent/check.sh`.

**Security note:** the provided flow reads plaintext passwords from a file and uses them directly — this is fine for SadServers exercises but is **not recommended** for production. See *Notes & Improvements* below for safer alternatives.

---

## Step-by-step Command History (trimmed)

---

1. Inspect the user list and help for `adduser`/`useradd`.

   ```bash
   cat user_list.txt
   sudo adduser --help
   ```
2. Convert semicolon-separated entries to newline-separated (so `split` lines are usable):

   ```bash
   cat user_list.txt | tr ';' '\n' > broken_user_list.txt
   ```

   *(Used this to inspect fields, then reverted to parsing each original line inside the script.)*
3. Create `script.sh`, make it executable and iterate editing until it worked:

   ```bash
   vi script.sh
   chmod +x script.sh
   ./script.sh
   ```
4. Manually tried creating a user to verify the password hashing approach:

   ```bash
   sudo useradd -m tyler
   sudo usermod --password $(echo hello | openssl passwd -1 -stdin) tyler
   su tyler
   sudo passwd tyler           # interactive; tried options until settled on openssl approach
   ```
5. Final script run and verification:

   ```bash
   ./script.sh
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  ls
 2  cat user_list.txt 
 3  sudo adduser --help
 4  /home/admin/agent/check.sh
 5  cat /home/admin/agent/check.sh
 6  ls
 7  cat user_list.txt 
 8  sudo adduser --help
 9  ll
10  ls
11  vi 
12  ls
13  touch script.sh
14  vi script.sh 
15  for ln in `cat user_list.txt`; do cat $ln ;done;
16  for ln in `cat user_list.txt`; do echo $ln ;done;
17  cat user_list.txt | tr ';' '\n'
18  cat user_list.txt | tr ';' '\n' > broken_user_list.txt;
19  cat broken_user_list.txt 
20  vi script.sh 
21  ls -ltr
22  chmod +X script.sh 
23  ./scr
24  script.sh
25  script.sh 
26  ls
27  ls -ltr
28  chmod +x script.sh 
29  script.sh 
30  ./script.sh
31  vi script.sh 
32  ./script.sh
33  vi script.sh 
34  ./script.sh
35  vi script.sh 
36  sudo useradd -m tyler
37  sudo usermod --password tylerpass tyler
38  su tyler
39  sudo passwd tyler
40  su tyler 
41  sudo usermod --pasword 1 tyler
42  sudo usermod --password 1 tyler
43  su tyler
44  usermod --password $(echo hello | openssl passwd -1 -stdin) tyler
45  sudo usermod --password $(echo hello | openssl passwd -1 -stdin) tyler
46  su tyler
47  vi script.sh 
48  cat script.sh 
49  ./script.sh 
50  /home/admin/agent/check.sh
51  history
```

`script.sh` contents used in the exercise:

```sh
#!/bin/sh

for line in `cat user_list.txt`;
do
        username=$(echo $line | awk -F';' '{print $1}')
        password=$(echo $line | awk -F';' '{print $2}')
        echo "creating user $username"
        sudo useradd -m $username
        sudo usermod --password $(echo $password | openssl passwd -1 -stdin) $username
        echo "user created"
done;
```
