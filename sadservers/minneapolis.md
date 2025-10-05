# SadServers — Minneapolis

[https://sadservers.com/newserver/minneapolis](https://sadservers.com/newserver/minneapolis)

---

## Scenario

---

Split a large CSV (`data.csv`) into **10 equally sized parts** and ensure **each split file contains the original header** line at the top.

---

## TL;DR (Fix Summary)

---

* Split the file into 10 parts with numeric suffixes and `.csv` extension:

  ```bash
  split -n l/10 -a 2 -d --additional-suffix=.csv data.csv data-
  ```
* Captured the header from the original file:

  ```bash
  head -n1 data.csv > header
  ```
* Inserted the header into parts `data-01.csv` … `data-09.csv` (the first part already contains it):

  ```bash
  for i in {1..9}; do sed -i "1i $(cat header)" data-0$i.csv; done
  ```

---

## Step-by-step Command History (trimmed)

---

1. Reviewed options, then split into 10 files:

   ```bash
   split -n l/10 -a 2 -d --additional-suffix=.csv data.csv data-
   ```
2. Verified outputs and inspected a part.
3. Extracted the header:

   ```bash
   head -n1 data.csv > header
   ```
4. Prefixed header to parts `01..09`:

   ```bash
   for i in {1..9}; do sed -i "1i $(cat header)" data-0$i.csv; done
   ```
5. Done.

---

## Full Command History (as executed)

---

```
 1  ls -ltr
 2  split --help
 3  split -n l/3 -a 2 -d --additional-suffix=.csv data.csv data
 4  ls -ltr
 5  rm data0*
 6  ls
 7  split -n l/10 -a 2 -d --additional-suffix=.csv data.csv data-
 8  ls -ltr
 9  cat v 
10  cat vdata-01.csv
11  cat data-01.csv
12  cat data-01.csv | head  -n1
13  cat data.csv | head  -n1
14  cat data.csv | head -n1 
15  ls cat data.csv | head -n1
16  ls
17  for i in {1..9}; do echo $i; done;
18  cat data.csv | head -n1 > header
19  for i in {1..9}; do sed -n "1i `cat header` data-0$i.csv"; done;
20  for i in {1..9}; do sed -n "1i `cat header`" data-0$i.csv; done;
21  for i in {1..9}; do sed -i "1i `cat header`" data-0$i.csv; done;
22  history
```
