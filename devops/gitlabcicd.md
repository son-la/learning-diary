* Objects
  * Pipeline
  * Job

* For system pkg installation
  * Job log /var/opt/gitlab/gitlab-ci/builds
  * Job artifact /var/opt/gitlab/gitlab-rails/shared/artifacts

* Job log is moved artifact directory after being archived.  
* By default, after a month, artifacts are deleted if job collect artifacts. There's a case of expired artifacts but not getting deleted  

* Delete pipeline will delete all build jobs and its logs/ artifacts 