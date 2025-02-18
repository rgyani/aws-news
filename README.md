# AWS News for me


AWS has  over 200+ services, and is continuously releasing/updating existing service, it sometimes becomes difficult to track the updates. Here I am keeping some notes on some services I use and track

###  Microsoft annonces FerretDB 2.0, an open-source document database platform built on PostgreSQL
28 Jan 2025  
Microsoft has launched a new open-source document database platform built on PostgreSQL. This platform offers no commercial licensing fees and enhances performance with BSON support. Developers can use FerretDB 2.0 for a MongoDB-like experience with improved performance.

#### Key Features of Microsoft’s Open Source Document Database
The platform includes two custom PostgreSQL extensions designed to optimize performance and efficiency:

1. **Pg_documentdb_core:** This extension optimises PostgreSQL for BSON (Binary JavaScript Object Notation) handling. BSON is a binary-encoded format of JSON documents, making it much faster to store and retrieve data.
2. **Pg_documentdb_api:** This extension adds the ability to perform CRUD operations (Create, Read, Update, Delete), manage queries, and index your data.


Together, these extensions provide the foundation for building document-based applications on top of a relational system.

### AWS announces Aurora DSQL (Distributed SQL)
03 Dec 2024:  
Amazon just announced a new service called Aurora DSQL (distributed SQL) a serverless, globally distributed database, promising a SLA of 99.999%, multi-regional, **postgres compatible** to compete with [Google Spanner](https://cloud.google.com/spanner).  
AWS claims that their offer is 4x faster than spanner (in read and write), and globally distributed across multiple regions.  
* To ensure that the database stays consistent across regions, under minime delays, AWS decoupled compute and storage. This technique is not new and used by other database companies like Neon. The only difference is that Neon is not real-time and global, while Aurora DSQL is.
* To ensure each region sees commits in the correct order, Aurora DSQL uses Amazon TimeSync Service, an EC2 add-on that synchronizes EC2 clocks using atomic clock satellites.   

As of this writing, Aurora DSQL is missing a lot of feature from Postgres :
* Database (only one database per cluster)
* Views
* Triggers
* **Foreign keys (a big one…)**
* a lot of extensions, like pgvector or postgis
( 10k row update per commit

### AWS announces Amazon S3 Tables - Fully managed Apache Iceberg tables optimized for analytics workloads
03 Dec 2024:  
 S3 Tables introduce table buckets, a new bucket type that is purpose-built to store tabular data. With table buckets, you can quickly create tables and set up table-level permissions to manage access to your data lake. You can then load and query data in your tables with standard SQL, and take advantage of Apache Iceberg’s advanced analytics capabilities such as row-level transactions, queryable snapshots, schema evolution, and more. Table buckets also provide policy-driven table maintenance, helping you to automate operational tasks such as compaction, snapshot management, and unreferenced file removal.


### Amazon S3 will no longer charge for several HTTP error codes
13 May 2024:
After a recent outcry over S3 charging for Unauthorized requests (4xx), AWS Chief Evangelist Jeff Barr got [involved](https://x.com/jeffbarr/status/1787844682216792163) and AWS announced [change](https://aws.amazon.com/about-aws/whats-new/2024/05/amazon-s3-no-charge-http-error-codes)  
Only took them 14 years, nice!

### Hashicorp sale to IBM
IBM announced on April 24 2024 that it will pay $6.4 billion ($35 per share) for HashiCorp, has stated that the company will remain independent after the takeover, but based on what actually happened after its previous acquisitions in the IT world, not everybody is sold on that promise.

Earlier in August 2023 Hashicorp, changed their licencing model to Business Source License (BSL) in place of the standard Mozilla Public License v2.0.
In response to this OpenTofu was forked to be developed as a community-driven alternative to Terraform. However Hashcorp was quick to send them a [Cease-And-Desist letter accusing of stealing code](https://www.reddit.com/r/Terraform/comments/1c1iquc/our_response_to_hashicorps_cease_and_desist/) 

### Redis Licence Change 
 In 2018, Redis Labs introduced a license change for certain Modules (RedisGraph, RedisSearch, ReJSON, Redis-ML, and RedisBloom but not Redis itself), moving them from the permissive Apache 2.0 license to a more restrictive Common Clause license. This change aimed to prevent cloud service providers from offering Redis Labs' commercial add-ons as a service without sharing revenue.  
In 2024, Redis underwent another licensing change, adopting the Redis Source Available License v2 (RSALv2) and the Server Side Public License v1 (SSPLv1) for its core repository. This decision prompted the Linux Foundation to create a fork named [Valkey](https://valkey.io/), enabling the community to maintain an open-source version of Redis.  
Valkey has since been backed by AWS, Google Cloud, Oracle, Ericsson, and Snap Inc, while notably Microsoft has created their own fork named [Garnet](https://github.com/microsoft/garnet).  

Earlier in 2021, Elastic announced a bombshell in the open source world: [the ELK Stack would no longer be open source, as of version 7.11]((https://logz.io/blog/open-source-elasticsearch-doubling-down/).  
The lead to forks like OpenSearch

### Amazon CloudFront announces availability of Embedded Points of Presence
23 Feb 2024:  
Points of Presence (POPs) are a new type of CloudFront infrastructure deployed closest to end viewers, within internet service provider (ISP) and mobile network operator (MNO) networks to deliver large scale live-stream video, video-on-demand (VOD), and game downloads. 

### CloudFront KeyValueStore: A low-latency datastore for CloudFront Functions
21 Nov 2023:
With CloudFront Functions in Amazon CloudFront, you can write lightweight functions in JavaScript for high-scale, latency-sensitive CDN customizations. Previously, you had to embed configuration data inside the function code, eg. data to determine if a URL should be redirected and which URL to redirect to.  
With CloudFront KeyValueStore, you can now update the data associated with a function and the function code independently from each other. This simplifies function code and makes it easy to update data without the need to deploy code changes.


### AWS Bedrock, a fully managed service to build generative AI applications with foundation models 
28 Sep, 2023:  
Read More here
https://aws.amazon.com/blogs/aws/build-ai-apps-with-partyrock-and-amazon-bedrock/


### AWS VPC Lattice for connecting clients to services within a VPC
31 Mar, 2023:   
VPC Lattice is similar to AWS PrivateLink with a key difference.  
While AWS PrivateLink works by placing Elastic Network Interfaces within your subnet, which your clients can use to tunnel network traffic to the destination service, VPC Lattice works by exposing endpoints as link-local addresses(only accessible by software that runs on the client instance itself)

AWS has carved out the range 169.254.171.0/24 for VPC Lattice’s use, typically routing directly to 169.254.171.0

 Remember, we earlier had other link-local addresses like
 * EC2’s Instance Metadata Service, which is located at 169.254.169.254
 * Amazon Time Sync Service (NTP), which is located at 169.254.169.123
 * Route 53’s DNS Resolver, which is located at 169.254.169.253
 * ECS’s Task Metadata Endpoint, which is located at 169.254.170.2
 
 These didnot require any special routing or security rules.

 But VPC does require Security Groups and NACLs to allow traffic to and from the VPC Lattice data plane at 169.254.171.0/24 on whichever port the destination service exposes.

### Amazon DynamoDB now supports up to 100 actions per transaction
6 Sep, 2022:  
Amazon DynamoDB transactions enable coordinated, all-or-nothing changes to multiple items both within and across tables. The maximum number of actions in a single transaction has now increased from 25 to 100.



### Accelerate Your JAVA Lambda Functions with Lambda SnapStart
28 Nov 2022:   
When using Lambda, your functions are run inside of a secure and isolated execution environment. The lifecycle of each environment consists of three main phases: Init, Invoke, and Shutdown.  
Among other things, the Init phase bootstraps the runtime for the function and runs the function’s static code. In many cases, these operations are completed within milliseconds and do not lengthen the phase in any appreciable way. In the remaining cases, they can take a considerable amount of time, for several reasons.  
First, initializing the runtime for some languages can be expensive. For example, the Init phase for a Lambda function that uses one of the Java runtimes in conjunction with a framework such as Spring Boot, Quarkus, or Micronaut can sometimes take as long as ten seconds (this includes dependency injection, compilation of the code for the function, and classpath component scanning).   
Second, the static code might download some machine learning models, pre-compute some reference data, or establish network connections to other AWS services.

After you enable Lambda SnapStart for a particular Lambda function, publishing a new version of the function will trigger an optimization process.   
The process launches your function and runs it through the entire Init phase. Then it takes an immutable, encrypted snapshot of the memory and disk state, and caches it for reuse.  
When the function is subsequently invoked, the state is retrieved from the cache in chunks on an as-needed basis and used to populate the execution environment. 

This optimization makes invocation time faster and more predictable, since creating a fresh execution environment no longer requires a dedicated Init phase.  

**Some Caveats:**
1. Only available for Java 11 runtime.
2. SnapStart does not support provisioned concurrency, the arm64 architecture, the Lambda Extensions API, Amazon Elastic File System (Amazon EFS), AWS X-Ray, or ephemeral storage greater than 512 MB.
3. Adds 90secs to deployment

[link](https://aws.amazon.com/blogs/aws/new-accelerate-your-lambda-functions-with-lambda-snapstart/)


### Amazon OpenSearch (formerly ElasticSearch) Serverless 
28 Nov 2022:  
Before the launch of OpenSearch Serverless, you created a managed cluster, specifying instance types, counts, and storage options, and then managed the lifecycle and shard strategy for indices within that cluster. With OpenSearch Serverless, you create a Collection, which manages a group of indices that work together to support a specific workload. You no longer need to specify the hardware or manage the indices directly.   
[link](https://aws.amazon.com/blogs/aws/preview-amazon-opensearch-serverless-run-search-and-analytics-workloads-without-managing-clusters/)

### Amazon Inspector Now Scans AWS Lambda Functions for Vulnerabilities
28 Nov 2022:   
Amazon Inspector is available starting today for functions and layers written in Java, NodeJS, and Python. By default, it continually scans all the functions inside your account, but if you want to exclude a particular Lambda function, you can attach the tag with the key InspectorExclusion and the value LambdaStandardScanning.   
[link](https://aws.amazon.com/blogs/aws/amazon-inspector-now-scans-aws-lambda-functions-for-vulnerabilities/)


### Step Functions Distributed Map 
28 Nov 2022:   
With Step functions, the new distributed map state can launch up to ten thousand parallel workflows to process data, instead of 40 earlier  
[link](https://aws.amazon.com/blogs/aws/step-functions-distributed-map-a-serverless-solution-for-large-scale-parallel-data-processing/)

### Amazon CloudWatch launches cross-account observability across multiple AWS accounts
27 Nov 2022:  
With cross-account observability in CloudWatch, you can seamlessly search, visualize, and analyze your metrics, logs, and traces without any account boundaries.   
[link](https://aws.amazon.com/about-aws/whats-new/2022/11/amazon-cloudwatch-cross-account-observability-multiple-aws-accounts/)


### AWS opens the 30th AWS Region – Asia Pacific (Hyderabad) Region in India.
21 Nov 2022:  
AWS announced the general availability of the 30th AWS Region, Asia Pacific (Hyderabad) Region, with three Availability Zones and the ap-south-2 API name.
[link](https://aws.amazon.com/blogs/aws/now-open-the-30th-aws-region-asia-pacific-hyderabad-region-in-india/)


### Cross-Account Access capabilities for AWS Step Functions
18 Nov 2022:  
We have to use resource-based policies to make cross-account access for Step Functions possible. With resource-based policies, you can specify who has access to the resource and what actions they can perform on it.  
However, Not all AWS services support resource-based policies. eg, it is possible to enable cross-account access via resource-based policies with services like AWS Lambda, Amazon SQS, or Amazon SNS, but, services such as Amazon DynamoDB do not support resource-based policies, so your workflows can only use Step Functions’ direct integration if it belongs to the same account.

Now, customers can take advantage of identity-based policies in Step Functions so your workflow can directly invoke resources in other AWS accounts, thus allowing cross-account service API integrations.  
[link](https://aws.amazon.com/blogs/compute/introducing-cross-account-access-capabilities-for-aws-step-functions/)


### AppSync GraphQL APIs support Javascript Resolvers  
17 Nov 2022:  
AWS AppSync supports JavaScript resolvers and provides a resolver evaluation engine to test them before publishing them to the cloud.  
[link](https://aws.amazon.com/blogs/aws/aws-appsync-graphql-apis-supports-javascript-resolvers/)


### New region in Switzerland, eu-central-2
08 Nov 2022:
AWS announced the opening of its 28th AWS Region: Europe (Zurich), also known by its API name: eu-central-2.  
[link](https://aws.amazon.com/blogs/aws/a-new-aws-region-opens-in-switzerland/)


### AWS Managed Services (AMS) now supports SQL Server on EC2 Operations
03 Nov 2022:  
With this launch, customers can now bring their existing SQL Server licenses (BYOL) to EC2 and take advantage of AMS to operate more efficiently.  
SQL Server on EC2 Operations is available to AMS customers for an additional fee and is available in all regions where AMS is available.  
[link](https://aws.amazon.com/about-aws/whats-new/2022/11/aws-managed-services-supports-sql-server-ec2-operations/)

### AWS Introduces server-side filters GraphQL subscriptions with AWS Amplify
28 Oct 2022:  
Subscriptions are long-lasting GraphQL read operations that can update their result whenever a particular server-side event occurs. Most commonly, updated results are pushed from the server to subscribing clients. For example, a chat application's server might use a subscription to push newly received messages to all clients in a particular chat room.       
With Amplify v10.3.1, we can now filter real-time GraphQL subscription events service-side, which gives developers the ability to optimize network traffic by only getting the real-time events for the data they care about. So now, in the above scenario, our subsciption will filter and push only messages which contains a particular text

```
//establishing real-time subscription with
const sub = API.graphql(
  onCreateTweet, {
  input: {
     filter: { // <- Brand NEW filter support!
        content: {
           contains: "AWS Amplify"
        }
     }
  }
}).subscribe()
```
[link](https://aws.amazon.com/blogs/mobile/announcing-server-side-filters-for-real-time-graphql-subscriptions-with-aws-amplify/)


### AWS Introduces AWS Parameters and Secrets Lambda Extension to Improve Performances and Security
18 Oct 2022:  
We dont need to include boilerplate in every function or worry about your caching implementation. Just use the AWS Parameters and Secrets Lambda Extension - easily added as **a layer to your function**.  
[link](https://aws.amazon.com/about-aws/whats-new/2022/10/aws-parameters-secrets-lambda-extension/)



### Amazon accidentally exposed an internal elastic search server packed with Prime Video viewing habits
27 Oct 2022:  
Security researcher Anurag Sen found an internal Amazon's Elastic Search DB (named Sairon) packed with Amazon Prime viewing habits stored, without password protection  
[link](https://techcrunch.com/2022/10/27/amazon-prime-video-server-exposed/)


### AWS has opened an AWS Local Zone in Germany in Hamburg.
27 Oct 2022:  
AWS Local Zones are small data centers adjacent to major population centers that places compute, storage, database, and other select AWS services close to large population and industry centers.  
[link](https://aws.amazon.com/about-aws/whats-new/2022/10/announcing-general-availability-aws-local-zones-hamburg-warsaw/)



### AWS Neptune Serverless
26 Oct 2022:   
Amazon Neptune Serverless is a new deployment option that automatically scales capacity based on the needs of the application, for developers to run graph databases without managing database capacity.    
[link](https://aws.amazon.com/about-aws/whats-new/2022/10/amazon-neptune-serverless-generally-available/)  
However, there are still some limitations (as I understand)
* No CloudFormation support
* Only a few regions 
* Still requires a VPC (just like RDS) 
* Doesn't scale to zero  


### Python 3.11.0 released (upto 60% faster)
24 Oct 2022:  
[link](https://www.python.org/downloads/release/python-3110/)

### AWS Lambda Functions powered by AWS Graviton2 now available in 12 additional regions
6 Oct 2022:   
AWS Lambda functions on AWS Graviton2, using an Arm-based processor architecture, are designed to deliver up to 19% better performance at 20% lower cost for a variety of Serverless workloads  
[link](https://aws.amazon.com/about-aws/whats-new/2022/10/aws-lambda-functions-graviton2-12-regions/)


### IAM Access Analyzer now reviews your AWS CloudTrail history to identify actions used across 140 AWS services and generates fine-grained policies
5 Oct, 2022:  
IAM Access Analyzer policy generation has expanded support to identify actions used from over 140 services to help developers create fine-grained policies based on their AWS CloudTrail access activity. New additions include actions from services such as AWS CloudFormation, Amazon DynamoDB, and Amazon Simple Queue Service. When developers request a policy, IAM Access Analyzer gets to work and generates a policy by analyzing their AWS CloudTrail logs to identify actions used  
[link](https://aws.amazon.com/about-aws/whats-new/2022/10/iam-access-analyzer-cloudtrail-history-identify-actions-140-aws-services-fine-grained-policies/)


###  Kafka 3.3: KRaft to replace Zookeepers for leader election
3 Oct, 2022:  
Currently, Kafka uses ZooKeeper to store its metadata about partitions and brokers, and to elect a broker to be the Kafka Controller.  We would like to remove this dependency on ZooKeeper.  This will enable us to manage metadata in a more scalable and robust way, enabling support for more partitions.  It will also simplify the deployment and configuration of Kafka.


### WSL now supports systemd
21 Sept, 2022:  
Systemd is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as PID 1 and starts the rest of the system.  
[link](https://devblogs.microsoft.com/commandline/systemd-support-is-now-available-in-wsl/)


### Azure Policy as Code
12 Sept, 2022:  
Azure Enterprise Policy as Code – A New Approach  
[link](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/azure-enterprise-policy-as-code-a-new-approach/ba-p/3607843)

### AWS open sources EventRuler (java library which powers EventBridge)
06 Sept, 2022:  
Amazon opensource-s a key technology that powers EventBridge. Event Ruler is a Java library that allows you to build apps that can match any number of rules against events at several hundred thousand events per second.
[link](https://aws.amazon.com/blogs/opensource/open-sourcing-event-ruler/)


### AWS Step Functions adds 14 new intrinsic functions
31 Aug, 2022:  
Now, Step Functions makes it easier to perform data processing tasks such as array manipulation, JSON object manipulation, and math functions within your workflows without having to invoke downstream services or add Task states. 
When building workflows, you may need to check the result of map and parallel states, merge JSON objects, or create a UUID. Previously, to accomplish these tasks you needed to write functions in downstream services such as AWS Lambda which resulted in more code and integration points to manage. With Step Functions new intrinsic functions, you can perform basic data processing and data manipulations such as merging two JSON objects using states.JsonMerge directly in your workflow so you can combine the results of a task and its original input, allowing you to use downstream services for more business-critical tasks.  
[link](https://aws.amazon.com/about-aws/whats-new/2022/08/aws-step-functions-14-new-intrinsic-features-process-data-workflows/)


### Hreoku no longer free
25 Aug, 2022:  
After offering them for over a decade, Heroku today announced that it will eliminate all of its free services — pushing users to paid plans.  
Heroku allows programmers to build, run and scale apps across programming languages including Java, PHP, Scala and Go. Salesforce acquired the company for $212 million in 2010 and subsequently introduced support for Node.js and Clojure and Heroku for Facebook, a package to simplify the process of deploying Facebook apps on Heroku infrastructure.  
[link](https://help.heroku.com/RSBRUH58/removal-of-heroku-free-product-plans-faq)


### AWS Region in UAE (me-central-1)
29 Aug, 2022:   
The AWS Middle East (UAE) Region is the second Region in the Middle East, joining the AWS Middle East (Bahrain) Region.   
[link](https://aws.amazon.com/blogs/aws/now-open-aws-region-in-the-united-arab-emirates-uae/)


### Eu-west-1 ireland datacenter upgrade paused due to energy constraints
24 Aug, 2022:  
Amazon and Microsoft have reportedly scrapped plans to build new data centres in Ireland due to the risk of overwhelming the country’s power grid.  
[link](https://metro.co.uk/2022/08/24/microsoft-amazon-scrap-irish-data-centres-over-power-grid-constraints-17235104/)


### Amazon DynamoDB can now import Amazon S3 data into a new table
18 Aug 2022:  
[link](https://aws.amazon.com/blogs/database/amazon-dynamodb-can-now-import-amazon-s3-data-into-a-new-table/)




###  HTTP/3 Support for Amazon CloudFront 
15 Aug 2022:  
Amazon CloudFront is a content delivery network (CDN) service, a network of interconnected servers that is geographically closer to the users and reaches their computers much faster. Amazon CloudFront reduces latency by delivering data through 410+ globally dispersed Points of Presence (PoPs) with automated network mapping and intelligent routing.   
HTTP/3 uses QUIC, a user datagram protocol-based, stream-multiplexed, and secure transport protocol that combines and improves upon the capabilities of existing transmission control protocol (TCP), TLS, and HTTP/2. Now, you can enable HTTP/3 for end user connections in all new and existing CloudFront distributions on all edge locations worldwide, and there is no additional charge for using this feature.
[link](https://aws.amazon.com/blogs/aws/new-http-3-support-for-amazon-cloudfront/)



### AWS Lambda has tiered pricing
4 Aug 2022:  
AWS introduces tiered pricing for Lambda. With tiered pricing, customers who run large workloads on Lambda can automatically save on their monthly costs. Tiered pricing is based on compute duration measured in GB-seconds. The tiered pricing breaks down as follows:
![img](imgs/f9e801e5-9150-40f7-aff2-5964219b5baa.jfif)
[link](https://aws.amazon.com/blogs/compute/introducing-tiered-pricing-for-aws-lambda/)

### AWS Managed Kafka Serverless
28 April 2022:  
Amazon MSK reduces the work needed to set up, scale, and manage Apache Kafka in production. With Amazon MSK, you can create a cluster in minutes and start sending data.   
Amazon MSK Serverless automatically provisions and manages the required resources to provide on-demand streaming capacity and storage for your applications   
[link](https://aws.amazon.com/blogs/aws/amazon-msk-serverless-now-generally-available-no-more-capacity-planning-for-your-managed-kafka-clusters/)

However, here again, in addition to storage, data-in charges, and data-out charges, you pay for cluster hours and partition hours.  

Nicely summarized [here](https://www.lastweekinaws.com/blog/no-aws-aurora-serverless-v2-is-not-serverless/) the misuse of 'serverless' descriptor by AWS


### Aurora Serverless v2
21 April 2022:
Aurora Serverless v2 scales instantly to support even the most demanding applications, delivering up to 90% cost savings compared to provisioning for peak capacity.
[link](https://aws.amazon.com/about-aws/whats-new/2022/04/amazon-aurora-serverless-v2/)   
However, this doesnot scale to zero, hence the name serverless is a misnomer


### AWS Lambda Function URLS: Built-in HTTPS Endpoints for Single-Function Microservices
06 April 2022:  
Function URLs are dual stack-enabled, supporting IPv4 and IPv6. After you configure a function URL for your function, you can invoke your function through its HTTP(S) endpoint via a web browser, curl, Postman, or any HTTP client. You can access your function URL through the public Internet only.   
[link](https://aws.amazon.com/blogs/aws/announcing-aws-lambda-function-urls-built-in-https-endpoints-for-single-function-microservices/)


### AWS Lambda Now Supports Up to 10 GB Ephemeral Storage
24 March, 2022:  
AWS Lambda now allows you to configure ephemeral storage (/tmp) between 512 MB and 10,240 MB. You can continue to use up to 512 MB for free and are charged for the amount of storage you configure over the free limit for the duration of invokes.  
[link](https://aws.amazon.com/blogs/aws/aws-lambda-now-supports-up-to-10-gb-ephemeral-storage/)


### Amazon EC2 enables easier patching of guest operating system and applications with Replace Root Volume
22 April 2021:  
Amazon EC2 announces the Replace Root Volume feature that enables customers to replace the root volume for a running instance. The feature restores the root volume of an instance to its launch state, or to a specific snapshot, without stopping the instance.  
[link](https://aws.amazon.com/about-aws/whats-new/2021/04/ec2-enables-replacing-root-volumes-for-quick-restoration-and-troubleshooting/)


### Redis Stack
7 April 2022:  
Redis has aggressively sought to build on its main stack largely used for data caching during the past few years. After introducing RediSearch, RedisRaft, RedisAI and its most recent release eponymously called Redis 7.0, it is now further distancing itself from its previous reputation as a data caching provider. This is manifested in its release of Redis Stack: a single module intended to help NoSQL developers by regrouping a number of components in one interface.  
[link](https://thenewstack.io/redis-puts-almost-everything-under-a-single-module/)


### Lambda based crypto malware DENONIA
11 April 2022:     
Denonia cryptominer is first malware to target AWS Lambda  
[link](https://www.malwarebytes.com/blog/business/2022/04/denonia-cryptominer-is-first-malware-to-target-aws-lambda)


### AWS CDK v2
02 Dec, 2021:  
AWS CDK v2 consolidates the stable parts of the AWS Construct Library, including the core library, into a single package, aws-cdk-lib . Developers no longer need to install additional packages for the individual AWS services they use.

CDK v1 enters maintenance on June 1,2022
[link](https://aws.amazon.com/about-aws/whats-new/2021/12/aws-cloud-development-kit-cdk-generally-available/) 
