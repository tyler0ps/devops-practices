# SadServers — "Tokamachi": Troubleshooting a Named Pipe

[https://sadservers.com/scenario/tokamachi](https://sadservers.com/scenario/tokamachi)

Session 1
```bash
tail -f reader.log
```
Keep it running

Session 2
```bash
/bin/bash -c '
echo "this is a test message being sent to the pipe" > /home/admin/namedpipe &
exec 3> /home/admin/namedpipe
while true; do
printf "%s\n" "this is a test message being sent to the pipe" >&3
sleep 0.5
done
' &
```

## Full Command History (as executed)

---

```
 1  tail -f reader.log
 2  ps -ef | grep named
 3  [200~/home/admin/agent/check.sh~
 4  /home/admin/agent/check.sh
 5  tail -f reader.log
 6  /home/admin/agent/check.sh
 7  tail -f reader.log
 8  /home/admin/agent/check.sh
 9  cat /home/admin/agent/check.sh 
10  tail -f reader.log
11  ps -ef 
12  kill -9 1640
13  ps -ef 
14  tail -f reader.log
15  cat /home/admin/agent/check.sh 
16  /home/admin/agent/check.sh
17  ps
18  ps -ef
20  /home/admin/agent/check.sh
21  tail -f /home/admin/reader.log
22  echo "EXTRA one-off message" > /home/admin/namedpipe
23  tail -f /home/admin/reader.log
24  /home/admin/agent/check.sh
25  tail -f /home/admin/reader.log
27  ps auxf|grep -q 'pipe'
28  if ! ps auxf|grep -q 'pipe'
29  ps auxf|grep -q 'pipe" > /home/admin/named[pipe]'"
30  ps auxf|grep -q 'pipe > /home/admin/named[pipe]'
31  ps auxf|grep -q pipe
32  ps auxf|grep -pipe
33  ps auxf|grep pipe
34  grep -h
35  grep --help
36  ps auxf 
37  ps auxf  | grep pipe
38  cat /home/admin/agent/check.sh 
39  /bin/bash -c '
echo "this is a test message being sent to the pipe" > /home/admin/namedpipe &
exec 3> /home/admin/namedpipe
while true; do
  printf "%s\n" "this is a test message being sent to the pipe" >&3
  sleep 0.5
done
' &
40  cat /home/admin/agent/check.sh 
41  /home/admin/agent/check.sh
42  ps -ef 
43  kill -9 2199
44  /home/admin/agent/check.sh
45  history
```
