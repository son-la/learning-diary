
### Check firewall
```
nc -l -u 8472 
echo 'Hello' | netcat -u 192.168.21.61 8472 
```

### ulimit
* ulimit for users are 1024
* containerd limit is infinite
```
grep ^Limit /lib/systemd/system/containerd.service
```
* Container takes ulimit from containerd, which is inherited from systemd


### cgroup
* Handle resource allocation and limitation for a process/ group of processes
* cgroup v2 is officially supported since 1.20, but stable in 1.25 onward.  
