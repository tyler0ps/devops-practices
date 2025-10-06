# SadServers — "Gitega": Git Time Machine

[https://sadservers.com/scenario/gitega](https://sadservers.com/scenario/gitega)

## Scenario

You’re dropped into a Git repository containing Go code and a set of tests.
The tests are currently failing, and your mission is to **find the commit where the tests last passed**.
Once identified, you must record the full commit hash of that working state into `/home/admin/solution`.

## TL;DR (Fix Summary)

* Inspected Git commit history using `git log` and `git log --oneline`.
* Checked out successive commits and ran `go test` each time.
* Discovered that commit `2e44089778e44dcd9b97aa3baacdcff10311841b` passed all tests.
* Saved that hash to `/home/admin/solution`.

## Step-by-step Command History (trimmed)

```bash
# Review repo and test setup
ls -ltr
cd git/
go test   # failing

# Review commits
git log --oneline

# Check out earlier commits and test
git checkout 96086c8; go test
git checkout 5179399; go test
git checkout 2e44089; go test  # ✅ tests pass here

# Write the good commit hash as solution
echo 2e44089778e44dcd9b97aa3baacdcff10311841b > /home/admin/solution
/home/admin/agent/check.sh
```

## Full Command History (as executed)

```bash
1  git status
2  ls -ltr
3  cd git/
4  ls -ltr
5  go test
6  git log
7  git log --oneline
8  gco 96086c8
9  git checkout 96086c8
10 go test
11 git log
12 git log --oneline
13 git checkout 5179399; go test;
14 git checkout 2e44089; go test;
15 git log | grep 2e44089
16 echo 2e44089778e44dcd9b97aa3baacdcff10311841b > /home/admin/solution
17 /home/admin/agent/check.sh
18 history
```