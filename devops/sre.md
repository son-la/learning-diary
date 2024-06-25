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
* SLO will not be right, but with measurement -> Come back and discuss about SLO.

## Risk management

* Template
    * TTD: Time to discover
    * TTR: Time to recovery

| Risk                 | TTD | TTR | Freq/ Yr | Users | Bad / Yr |
|----------------------|-----|-----|----------|-------|----------|
| Production DB backup | 0   | 2h  | 12       | 100%  | 1440m    |
| DC Failure           | 15m | 8h  | 1        | 100%  | 780m     |



# SRE Book Google

## Monitoring distributed system

* Four golden signals
    > * Latency
        >> * Separate succesful and failed requests. Fail fast is better. 
    > * Traffic
        >> * Demand for the system
        >> * Example
            >>> * Web service: HTTP requests per second 
            >>> * Streaming: I/O rate, concurrent session
            >>> * KV storage: transaction per second, retrieval per second
    > * Errors 
        >> * Explicitly (HTTP status code), Implicitly (Response content) or Policy (Latency > 1s)
    > * Saturation/ Utilization
        >> * Usually look for indirect signals. Depends on system .e.: memroy-constraint system -> focus on memory utilization
        >> * Latency is good indicator of saturation. Measure p99 latency 

* Avoid staring at the screen to watch for problems
* Prevent alert flooding with trigger dependency
    > * Example: If parent trigger is NOT ok, dependent trigger won't fire
* Keep monitoring/ alerting rules simple
    > * Exception: Abnomaly traffics
    > * Use better tools for post hoc analysis
* Blackbox monitoring is symptom-oriented, modest but critical.
* Whitebox monitoring is important for debugging and imminent problems
* Better to look at distribution rather than means to see also variation. E.g.: 1% request can be 50 x average value. Woyrring about the `Tail`
* Find appropriate resolution for measurement
    > * Correlate measurement resolution with SLO. E.g.: Status check 1-2 times/ minute is sufficient for SLO 99.9% uptime. Fullness check 1 time / minute is sufficient for hardrive with SLO 99.9% availability.
    > * Higly granular measurement can be done locally, and aggregation and anlysis is done by external system -> Avoid high retention cost.
* Simplicity is the best
    > * Neither used in dashboard nor alert -> signals to be removed
    > * Simple, predictable and reliable monitoring rules
    > * Google's monitoring system are broken up into binaries.

* Question to ask when creating new monitoring and alerting rule
    > * When can I ignore this alert? How can I avoid that situation?
    > * Does this alert definitley mean users are being negatively impacted? 
    > * Can I do something to repsonse? Could the action wait until morning? Could action be safely automated? Is action long-term fix or workaround? 
    > * Any other people getting paged for this issue? 

* Design philosophy for monitoring/ alerting:
    > * Page = urgent. Avoid *Alert fatigue*
    > * Page is actionable
    > * Page requires intelligence
    > * Page should be about novel problem

* Spend much more efforts to catch symptoms. For a cause, it must be very definitie and imminent. 

* If root cause for alert cannot be addressed -> automate response



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


### Chapter 4: Advocacy
* Build the story
    > * Know the audience and speak their language
* Story ideas: reputation, possiblity, efficiency, surprise, transformation 
* Collect ideas to share (Remember to ask permission to retell it)
(!): Resilience engineering

### Chapter 5: Preparing to become SRE
* Coding
* Fundamentals: single system, distributed system, statistics, data visualization, story telling, 


### Chapter 11: Organizational factors for success
* NOTE: This chapter has quite many useful questions to get to know the organization
* Organization values are key for any success. 

* F1: Identifying the real problem
* F2: Identify willingess to solve problem
* F3: Identify timeline/ patience to wait for improvement
* F4: Collobration in organization (How easy to collab to get things change)
* F5: Data-driven decision making
* F6: Lesson learn/ post-motern culture
* F7: How easy to make change
* F8: Identify frictions in the system

### Chapter 12: How SRE fails
* Well many ways :) 

### Chapter 13: Selling SRE
* Developers taking production work v.s. dedicated production engineers with developer background
* SRE investment is like insurance about outage risks
* Audience:
    > * Product manager: user aquisition, feature velocity
    > * Finance: revenue growth for associated user acquisition
    > * Sernior exec: How many minutes are willing to talk to unhappy customers about reliability issue? 
