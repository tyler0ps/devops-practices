# SadServers — "Tokelau": Delete from history

[https://sadservers.com/newserver/tokelau](https://sadservers.com/newserver/tokelau)

---

## Scenario

---

You need to **remove specific entries** (those matching a pattern) from the shell history so they no longer appear in the session history file. The challenge shows how to identify history line numbers for matching entries, delete them in the correct order, and persist the cleaned history.

---

## TL;DR (Fix Summary)

---

* Extracted history line numbers for commands matching a pattern (`foo`) into a file.
* Deleted those history entries by index **in reverse order** (to avoid shifting indices).
* Wrote the cleaned history back to the history file.
* Verified with the provided check script.

---

## Step-by-step Command History (trimmed)

---

1. List history entries that match `foo` and capture their line numbers:

   ```bash
   history | grep -i foo | awk '{print $1}' > list
   ```
2. Delete each matching history entry by index — iterate in reverse (using `tac`) so deletions don't shift subsequent indices:

   ```bash
   for i in `tac list`; do history -d $i; done;
   ```
3. Persist the in-memory history to the history file:

   ```bash
   history -w
   ```
4. Run the verification script:

   ```bash
   /home/admin/agent/check.sh
   ```
5. Inspect history if needed:

   ```bash
   history
   ```

---

## Full Command History (as executed)

---

```
history | grep -i foo | awk '{print $1}' > list
for i in `tac list`; do history -d $i; done;
history -w
/home/admin/agent/check.sh
history
```
