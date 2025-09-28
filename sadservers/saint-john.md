https://sadservers.com/scenario/saint-john

lsof /var/log/bad.log | sort -nk2 | awk '/PID/{next}{print $2}' | xargs kill -9

admin@ip-10-1-12-49:~$ lsof /var/log/bad.log | awk 'NR>1{print $2}' | xargs -r kill -9 
