# SadServers — Constanța (Jumping Frog)  
https://sadservers.com/newserver/constanta  

---

## Scenario
---
This puzzle is about **pivoting across users (“jumping like a frog”)** to finally retrieve a secret.  
- Each user (`user1`, `user2`, …) has `.ssh` access configured in a chained manner.  
- The task is to escalate from one user to the next by generating SSH keys and appending them to `authorized_keys`.  
- Once inside the final user (`user3`), the target `secret.txt` file can be accessed and copied to the admin’s home directory.  

---

## TL;DR (Fix Summary)
---
- Generated SSH keys for each user, appended the `.pub` into their `.ssh/authorized_keys`.  
- Used `ssh -i` to hop from one user to the next.  
- Reached `user3`, read the `secret.txt`.  
- Copied/moved the secret into `/home/admin/solution.txt`.  
- Verified with `/home/admin/agent/check.sh`.  

---

## Step-by-step Command History (trimmed)
---
1. Explored `/home` and confirmed available users.  
2. For **user1**:  
   ```bash
   cd /home/user1/.ssh/
   ssh-keygen -f user1key
   cat user1key.pub >> authorized_keys
   ssh -i user1key user1@localhost
    ```

3. For **user2**:

   ```bash
   cd /home/user2/.ssh/
   ssh-keygen -f u2key
   cat u2key.pub >> authorized_keys
   ssh -i u2key user2@localhost
   ```
4. For **user3**:

   ```bash
   cd /home/user3
   cat secret.txt
   cp secret.txt /home/admin/secret.txt
   mv /home/admin/secret.txt /home/admin/solution.txt
   ```
5. Verified solution:

   ```bash
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  cd /home
 2  ls
 3  id
 4  ls -ltr
 5  id user3
 6  cd user1/
 7  ls
 8  ls -a
 9  cd .ssh/
10  ssh-keygen -f user1key
11  cat user1key.pub >> authorized_keys 
12  ssh -i user1key user1@localhost
13  history
```

```
 1  cd /home
 2  id
 3  cd user2/.ssh/
 4  ssh-keygen -f u2key
 5  cat u2key >> authorized_keys 
 6  cat u2key.pub >>authorized_keys 
 7  ssh -i u2key user2@localhost
 8  history
```

```
 1  id
 2  cd /home/
 3  cd .ssh
 4  ls
 5  cd user
 6  ls
 7  ls3
 8  cd user3
 9  ls -ltr
10  cat secret.txt 
11  id
13  cp secret.txt /home/admin/secret.txt
14  cat /home/admin/solution.txt 
15  mv /home/admin/secret.txt /home/admin/solution.txt 
16  ls -ltr
17  /home/admin/agent/check.sh
18  history
```