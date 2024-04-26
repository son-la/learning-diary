* Request = soft limit
  * Only used for scheduling
  * $$ CpuTime = { shares \over \sum_{} share} * NumCPUs   $$
* Limit = hard limit
  * Cgroup CFS Bandwidth Control
  * Containers are limited to using quota amount of CPU time in a period
  * By default, `cpu.cfs_period_us=100000` or `100ms`. Check `cpu.cfs_quota_us`
  * When checking `cpu.stat`,
    * `nr_periods` = number of periods the app is running
    * `nr_throttled` = number of periods the app is throttled

* If CPU usage is low, but latency is high -> check throtlling
  * If throtlling is high (approaching 100%), some options:
    * Increase CPU Limit 
    * Decreate number of threads 
      * Go: set GOMAXPROCES
    * Use whole CPU instead of fractional




* Ref: https://www.youtube.com/watch?v=UE7QX98-kO0