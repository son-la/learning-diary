### AWS Lambda 
* Code invokation as a service :) 
* Integration models
  * Synchronouse i.e.: Client queries Lambda directly and wait for response
    * Auth: AWS IAM or none
    * Cognito, CloudFront, WAF to protect direct Lambda function call
  * Asynchronous i.e.: 
    * Event source -> Function -> AWS Services
  * Poll-based (Event source mapping)
* Performance
  * Mem: 128MB -> 10GB
  * CPU and Network scale propotionally e.g.: 10GB -> 6vCPUs
  * Use AWS Lambda Power tuning -> mem=X -> Execution time & Cost. Execution on x86_64 vs ARM (Graviton2)
* Execution Environment lifecycle
  * Stages
    * Init 
      * Varies from < 100ms to 1s.
      * Cold start
        *  < 1% production invokes
        * Code update -> Cold start 
      * Steps: `Create new execution env`, `Download code/ image`, `Runtime`, `Run function prehandler inization code` 
    * Invoke
      * Steps: `Run function handler code`
    * Shutdown
  * Developer optmizes function `pre-handler` and `handler`

* Development tips:
  * Business logic code outside handler function
  * Don't include the whole aws-sdk, only include what's needed 
    * Avoid monolithic
    * Minify/uglify production code
  * Connection establishment
    * Handle reconnection in handler
    * Keep-alive in AWS SDKs
  * State
    * Keep data for subsequent invocations. Store only thing that required
  * AWS Xray for profiling function
  * Java has snapstart i.e.: when user function -> 10x faster startup. No extra cost
    





### API Gateway
  * Functions
    * Throttling logic
    * Routing
    * Caching
    * Auth
    * ...
  * Directly connecto to AWS services. No need to use Lambda as proxy

### Amazon EventBridge
  * `EventBridge pipe`  parse `DynamoDB` item and put to `EventBridge event bus`


* Modular function do single thing

### Model
* Orchestration (AWS Step Functions)
  * In-built login and state machine. E.g.: `DynamoDB.GetItem ?? CloudFormation.CreateStack : SQS.SendMessage("Item not found")`
  * Standard vs Express
    ![alt text](serverless-step-function-model.png "Models") Combination: Standard workflow triggers Express workflow.


* Choreogrpahy (AWS EventBridge)


### Reference architect
* Streaming service
![alt text](serverless-streaming-example.png "Streaming reference arch")
