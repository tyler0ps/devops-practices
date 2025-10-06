# SadServers — "Apia": Needle in a Haystack

[https://sadservers.com/newserver/apia](https://sadservers.com/newserver/apia)

## Scenario

In this challenge, you’re placed in a directory full of text files under `/home/admin/data/`.
Only one of them hides the keyword that solves the task. The goal is to find the file that’s *different* from the rest — the “needle in a haystack.”
Once identified, you must extract the special keyword and save it in `/home/admin/solution`.

## TL;DR (Fix Summary)

* Inspected file sizes to find anomalies (`wc -c * | grep -v 1046`).
* Compared two suspicious files (`file0.txt` and `file76.txt`).
* Normalized content using `tr`, `sort`, and `sed` to identify differing words.
* Found the keyword `eureka`.
* Saved solution via `echo eureka > /home/admin/solution`.

## Step-by-step Command History (trimmed)

```bash
# Explore files
ls -ltr
cd data/
ls -ltr

# Identify file sizes and possible outliers
wc -c * | grep -v 1046

# Compare content of outlier files
sdiff file76.txt file0.txt

# Normalize content for clean diffing
tr '[:punct:]' '\n' < file0.txt | tr ' ' '\n' | tr -d ' ' | sort | sed '/^$/d' > sorted0
tr '[:punct:]' '\n' < file76.txt | tr ' ' '\n' | tr -d ' ' | sort | sed '/^$/d' > sorted1

# Inspect differences
vimdiff sorted0 sorted1

# Found keyword and wrote solution
echo eureka > /home/admin/solution
/home/admin/agent/check.sh
```

## Full Command History (as executed)

```bash
1  ls -ltr
2  cd data/
3  ls -ltr
4  cat file24.txt 
5  cat file1.txt
6  cat file2.txt
7  du -h *
8  du *
9  ls -ltr
10 wc -c file0.txt 
11 wc -c * | grep -v 1046
12 cat file76.txt
13 cat file0.txt
14 sdiff
15 sdiff --help
16 sdiff file76.txt file0.txt 
17 cp file0.txt tmp0.txt
18 tr '[:punct:]' '\n' < tmp0.txt | tr ' ' '\n' | tr -d ' ' | sort | sed '/^$/d' > sorted0
19 tr '[:punct:]' '\n' < file76.txt | tr ' ' '\n' | tr -d ' ' | sort | sed '/^$/d' > sorted1
20 sdiff sorted0 sorted1 
21 vimdiff sorted0 sorted1 
22 echo eureka > /home/admin/solution
23 /home/admin/agent/check.sh
24 history
```
