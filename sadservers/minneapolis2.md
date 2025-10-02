# SadServers — Minneapolis-2  
https://sadservers.com/newserver/minneapolis-2  

---

## Scenario
---
A large CSV file (`data.csv`) needed to be split into smaller files for processing.  
The challenge was that each split file had to **retain the original CSV header** row, otherwise validation with `check_csv.py` would fail.  

---

## TL;DR (Fix Summary)
---
- Used `split -n l/10 data.csv` to divide the file into 10 chunks.  
- Renamed the split outputs (`xaa`, `xab`, …) into meaningful filenames (`data-00.csv`, `data-01.csv`, …).  
- Extracted the CSV header line from the original file.  
- Inserted the header at the top of every split file (`sed -i "1i <header>" data-XX.csv`).  
- Verified correctness with `python3 check_csv.py` and `/home/admin/agent/check.sh`.  

---

## Step-by-step Command History (trimmed)
---
1. Checked `split` options and file size.  
2. Split the original CSV into 10 parts:  
   ```bash
   split -n l/10 data.csv
   ```

3. Verified line counts and renamed chunks:

   ```bash
   mv xaa data-00.csv
   mv xab data-01.csv
   ...
   mv xaj data-09.csv
   ```
4. Extracted the header line:

   ```bash
   sed -n '1p' data.csv
   ```
5. Inserted the header into each split file:

   ```bash
   sed -i.bak "1i $(sed -n '1p' data.csv)" data-00.csv
   sed -i.bak "1i $(sed -n '1p' data.csv)" data-01.csv
   ...
   sed -i.bak "1i $(sed -n '1p' data.csv)" data-09.csv
   ```
6. Ran the checker to validate results:

   ```bash
   python3 check_csv.py
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```bash
 1  which split
 2  split --help
 3  lks
 4  ls
 5  du -h data.csv 
 6  head -n50 data.csv 
 7  head -n10 data.csv 
 8  split -n --help
 9  split -n l/10 data.csv 
10  ls -ltr
11  cat xae 
12  ls
13  wc -l xaa 
14  ls -ltr
15  du -h *
16  head -n-2 data.csv 
17  head -n2 data.csv 
18  ls
19  head -n2 xaa 
20  head -n2 xad 
21  head -n2 xab
22  check_csv.py
23  python check_csv.py
24  python3 check_csv.py
25  mv xaa data-00.csv
26  clear
27  ls
28  mv xab data-01.csv
29  mv xac data-02.csv
30  mv xad data-03.csv
31  mv xae data-04.csv
32  mv xaf data-05.csv
33  mv xag data-06.csv
34  mv xah data-07.csv
35  mv xai data-08.csv
36  mv xaj data-09.csv
37  sed -n '1p' data.csv 
38  sed -n '1i hello' data-00.csv 
39  sed '1i hello' data-00.csv | head -2
40  sed --help
41  sed --help | grep -i before
42  sed '1i hello' data-01.csv | head -2
43  sed -n '1p' data-00.csv 
44  sed -n '1p' data-00.csv | xargs echo $0
45  sed -n '1p' data-00.csv | xargs sed -n "1i $0" data-01.csv 
46  sed -n "1i $(sed -n '1p' data-00.csv)" data-01.csv 
47  sed "1i $(sed -n '1p' data-00.csv)" data-01.csv | sed "1,3p"
48  sed "1i $(sed -n '1p' data-00.csv)" data-01.csv | head -n2
49  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-01.csv
50  ls
51  python3 check_csv.py
52  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-02.csv
53  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-03.csv
54  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-04.csv
55  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-05.csv
56  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-06.csv
58  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-08.csv
59  sed -i.bak "1i $(sed -n '1p' data-00.csv)" data-09.csv
60  python3 check_csv.py
61  /home/admin/agent/check.sh
62  history
```
