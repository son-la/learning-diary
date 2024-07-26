1. Find more occurance in access.log 
``` 
awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -n 1
```

2. Find last process writing to file
```
lsof -r1 /var/log/bad.log
```