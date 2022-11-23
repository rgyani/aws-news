# AWS News for me


AWS has  over 200+ services, and is continuously releasing/updating existing service, it sometimes becomes difficult to track the updates. Here I am keeping some notes on some services I use and track

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

### AWS Managed Kadka Serverless
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
