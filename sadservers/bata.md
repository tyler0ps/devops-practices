# SadServers — "Bata": Find in /proc

[https://sadservers.com/newserver/bata](https://sadservers.com/newserver/bata)

---

## Scenario

---

Search under `/proc` for a line that starts with `secret:` and save the **secret value** (after the colon) into `/home/admin/secret.txt`, ignoring permission noise from kernel-proc files.

---

## TL;DR (Fix Summary)

---

* Recursively grep `/proc` for lines beginning with `secret:` while silencing errors.
* Strip the `secret:` label and write just the value to `/home/admin/secret.txt`.
* Verify with the agent script.

Key one-liner:

```bash
grep -iR -e '^secret:' /proc 2>/dev/null -h | awk -F: '{print $2}' > /home/admin/secret.txt
```

---

## Step-by-step Command History (trimmed)

---

1. Navigate into `/proc` and explore:

   ```bash
   cd /proc && ls -ltr
   ```
2. Search recursively for the target line, suppressing errors from unreadable proc entries:

   ```bash
   grep -iR -e '^secret:' /proc 2>/dev/null
   ```
3. Extract only the secret **value** (text after `secret:`) and write to file:

   ```bash
   grep -iR -e '^secret:' /proc 2>/dev/null -h | awk -F: '{print $2}' > /home/admin/secret.txt
   ```
4. Validate:

   ```bash
   cat /home/admin/secret.txt
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  sudo echo $0
 2  clear
 3  id
 4  group
 5  ps -ef 
 6  cd /proc/
 7  ls
 8  ls -ltr 
 9  ls -ltr  | grep sys
10  cd sys
11  ls
12  ls -ltr
13  ls -ltra
14  grep . -iRE "^secret:"
15  grep . -iR -e "^secret:"
16  grep . -iR -e "^secret:" 2>/dev/null
17  cat ./kernel/core_pattern
18  grep . -iR -e "^secret:" -n 2>/dev/null 
19  grep --help
20  grep . -iR -e "^secret:" -h 2>/dev/null | awk -F: '{print $2}' > /home/admin/secret.txt
21  cat /home/admin/secret.txt 
22  /home/admin/agent/check.sh
23  history
```
