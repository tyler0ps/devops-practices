https://sadservers.com/scenario/oaxaca

Solution: find the file descriptor and close it.

lsof /home/admin/somefile
-> PID 805
ls -ltr /proc/805/fd/ | grep /home/admin/somefile
-> 77
exec 77>&-
