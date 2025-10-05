# SadServers — "Saint Paul": Merge Many CSVs files

[https://sadservers.com/newserver/st-paul](https://sadservers.com/newserver/st-paul)

---

## Scenario

---

You’re given **many CSV files** that each include a header row. The goal is to **merge them into a single `/home/admin/all.csv`** that has **one** header at the top and then all data rows from every file.

---

## TL;DR (Fix Summary)

---

* Captured a **canonical header** from one CSV into a file `header`.
* **Removed headers** from all CSVs.
* **Concatenated** all CSVs into `/home/admin/all.csv`.
* **Inserted** the canonical header at the top of the merged file.
* Verified with the check script.

---

## Step-by-step Command History (trimmed)

---

1. Inspect one CSV and save its header for reuse:

   ```bash
   head -1 polldayregistrations_enregistjourduscrutin24077.csv > header
   cat header
   ```
2. (Optional) Count/verify matched files:

   ```bash
   find . -type f -name "polldayregistrations_enregistjourduscrutin*.csv" | wc -l
   ```
3. Remove the first line (header) from **all** source CSVs:

   ```bash
   sed -i '1d' ./polldayregistrations_enregistjourduscrutin*.csv
   ```
4. Concatenate all data rows into the destination file:

   ```bash
   cat ./polldayregistrations_enregistjourduscrutin*.csv > /home/admin/all.csv
   ```
5. Add the saved header back to the top of the merged file:

   ```bash
   sed -i "1i $(cat header)" /home/admin/all.csv
   ```
6. Validate:

   ```bash
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  ls -ltr
 2  cat polldayregistrations_enregistjourduscrutin24076.csv | head -n2
 3  head -1 polldayregistrations_enregistjourduscrutin24077.csv > header
 4  cat header 
 5  find . --maxdepth=1 -type f -name "polldayregistrations_enregistjourduscrutin*.csv" | wc -l
 6  find . --max-depth=1 -type f -name "polldayregistrations_enregistjourduscrutin*.csv" | wc -l
 7  find --help
 8  find . -depth=1 -type f -name "polldayregistrations_enregistjourduscrutin*.csv" | wc -l
 9  find . -depth 1 -type f -name "polldayregistrations_enregistjourduscrutin*.csv" | wc -l
10  find . -type f -name "polldayregistrations_enregistjourduscrutin*.csv" -depth 1 | wc -l
11  find . -type f -name "polldayregistrations_enregistjourduscrutin*.csv" 
12  find . -type f -name "polldayregistrations_enregistjourduscrutin*.csv"  | wc -l
13  sed '1d' ./polldayregistrations_enregistjourduscrutin35078.csv | head -n2
14  sed '1d' ./polldayregistrations_enregistjourduscrutin*.csv
15  sed -i '1d' ./polldayregistrations_enregistjourduscrutin*.csv
16  clear
17  cat ./polldayregistrations_enregistjourduscrutin*.csv > /home/admin/all.csv
18  sed '1i `cat header`' /home/admin/all.csv | head -n2 
19  sed "1i `cat header`" /home/admin/all.csv | head -n2 
20  sed -i "1i `cat header`" /home/admin/all.csv 
21  /home/admin/agent/check.sh
22  history
```
