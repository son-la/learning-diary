# SRE 


## Concepts

SLI - Service Level Indicator
* Quant mesurement. E.g.: Request latency, Throughput, Failure per request
SLO - Service Level Objective
* Target for a collection of SLIs

SLA - Service Level Agreement
* Business agreement based on SLOs. E.g.: Consequences when not meeting SLOs

Error budget
* Quantify risks
* Calculated from SLO. E.g.:

| SLO (%) | Downtime/ month (minutes) |
| -------- | ------- |
| 99.9 | 43.5| 
| 99.99| 4.5 |
| 99.999| 0.5 |
| 99.9998 | 0.05 ~ 3s |

* Error budget accumulates over time
* Error budget for different components (e.g.: dependency)

Overhead
* Work don't connecto to production services. E.g.: cost report

Toil
* *Manual* and *Repetitive* work connected to production services
* Toil time could be reduced with script, instead of manually do something



## Example


## Practical tips
* Communicate expectation to customer -> CRE roles
* Works with Product management to agree on SLO
* To gain confidence for more frequent new feature release -> More testing
* Sign-off for crtical features (from VP)
* Measure toil yourself
* Toil must be capped at 30%-50%
* Calculate payoff. E.g.: No of time happens x Duration v.s. Time to spend on automating the work



# Becoming SRE - Blank Edelman


### Chapter 1: What is SRE?
* SRE to Reliability as DevOps to Delivery. 
    * Both cover SDLC: Development, QA, Delivery, Operation. 
    * DevOps attention starts from Dev -> Opeartion
    * SRE attention starts from Operation -> Dev

### Chapter 2: SRE mindset

* Start with curiosity to explore different aspects

* Zoom out to see system perspective
* Creating/ nurturing feedback loop
* Focus on customer