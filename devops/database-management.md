## Flyway community ver
* No snapshot 
* No undo  
* Comparison schema change 

## Liquibase 
* Init project, specify changelog file.  
* Change log file: Tell what liquidbase to do. E.g.: Include the change file. In change file, refers to the change set.  
* Snapshot 
* Changelog include actual change and rollback section defining what to do in the case of rollback 

## Bytebase 
* Bytebase is centralized  
* Gitops approach 
* Nice UI 
* No CLI -> huge minus point

 
# Design criteria:
* Schema migration can be integrated into application helm chart/ code
* Startup perform current state check and perform necessary steps  
* Alarm/ fail start when there has bene manual modification  
* Rollback if application downgrade happen  
* License


