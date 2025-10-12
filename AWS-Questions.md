# AWS DevOps Interview Questions

A comprehensive collection of AWS service-specific interview questions for DevOps professionals. This repository covers all major AWS services with questions ranging from basic to advanced levels.

## 📋 Table of Contents

- [EC2 (Elastic Compute Cloud)](#ec2-elastic-compute-cloud)
- [IAM (Identity and Access Management)](#iam-identity-and-access-management)
- [S3 (Simple Storage Service)](#s3-simple-storage-service)
- [VPC (Virtual Private Cloud)](#vpc-virtual-private-cloud)
- [Load Balancing (ELB/ALB/NLB)](#load-balancing-elbalbnlb)
- [Auto Scaling](#auto-scaling)
- [ECS (Elastic Container Service)](#ecs-elastic-container-service)
- [CloudFront](#cloudfront)
- [CloudWatch](#cloudwatch)
- [Route 53](#route-53)
- [Lambda](#lambda)
- [CloudFormation](#cloudformation)
- [RDS (Relational Database Service)](#rds-relational-database-service)
- [EBS (Elastic Block Store)](#ebs-elastic-block-store)

---

## EC2 (Elastic Compute Cloud)

### ⭐ Essential Questions for Junior DevOps Engineers
*These are the bare minimum questions you MUST know as a junior DevOps engineer*

**Q.1** What is Amazon EC2 and what is its primary purpose in AWS?

**Q.2** What is an EC2 instance type, and how do you choose the right one for your application?

**Q.3** Describe the typical steps involved in launching an EC2 instance.

**Q.4** What are security groups, and how do they control inbound and outbound traffic to EC2 instances?

**Q.5** What is an Amazon Machine Image (AMI)?

**Q.6** What is the difference between stopping and terminating an EC2 instance?

**Q.7** What are the different EC2 instance states?

**Q.8** How do you connect to an EC2 instance?

**Q.9** What is an EC2 key pair and why is it important?

**Q.10** What are the different purchasing options for EC2 instances?

### Additional EC2 Questions

**Q.11** What is an EC2 instance family, and when would you use one family over another?

**Q.12** What is an EC2 user data script, and how can it be used during instance launch?

**Q.13** Explain the purpose of EC2 instance metadata and how you can access it from within an instance.

**Q.14** How can you create custom AMIs, and why might you want to do so?

**Q.15** Explain the use of Network Access Control Lists (NACLs) and how they differ from security groups.

**Q.16** How do you enable and configure AWS Web Application Firewall (WAF) in front of an EC2-based web application?

**Q.17** What is Auto Scaling, and how can it be used to ensure high availability and scalability of EC2 instances?

**Q.18** Explain the purpose of Amazon Elastic Load Balancing (ELB) and its integration with EC2 instances.

**Q.19** What is Amazon EC2 Container Service (ECS), and how does it help with containerized applications on EC2 instances?

**Q.20** How can you configure Amazon Route 53 for DNS-based load balancing of EC2 instances?

**Q.21** What is status check in EC2 instance?

**Q.22** How to change instance types for running application without downtime of application?

**Q.23** What is difference between AMI and Snapshot?

**Q.24** How to troubleshoot boot related issues like kernel panic in EC2 Instances?

**Q.25** How many maximum number of IPs can be attached to an instance?

**Q.26** Describe different types of purchasing options available in AWS?

**Q.27** What are the different types of AWS Placement Groups, and how do they differ?

**Q.28** Can you change the placement group of a running EC2 instance?

**Q.29** What is the difference between an Availability Zone and a Placement Group?

**Q.30** What are some best practices for using Placement Groups in AWS?

**Q.31** Explain the limitations or constraints of AWS Placement Groups?

**Q.32** What is the difference between EBS-backed and instance-store-backed EC2 instances and their respective advantages and limitations?

**Q.33** How do you monitor EC2 instance performance?

**Q.34** What is EC2 instance hibernation and when would you use it?

**Q.35** Explain the concept of EC2 instance tenancy (shared, dedicated, dedicated host).

---

## IAM (Identity and Access Management)

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.36** What is AWS IAM and why is it important?

**Q.37** Explain the difference between an AWS user, group, role, and policy.

**Q.38** What is an IAM policy and how does it work?

**Q.39** What is the difference between inline policies and managed policies?

**Q.40** What is the principle of least privilege in IAM?

**Q.41** What is an IAM role and when would you use it?

**Q.42** How do IAM users authenticate to AWS?

**Q.43** What is the AWS root account and why should you avoid using it?

**Q.44** What are IAM access keys and when are they used?

**Q.45** What is MFA (Multi-Factor Authentication) and why is it important?

### Additional IAM Questions

**Q.46** How do you control access to AWS services and resources using IAM?

**Q.47** What are the best practices for creating and managing IAM users in AWS?

**Q.48** How do you enable multi-factor authentication (MFA) for AWS IAM users?

**Q.49** Describe the process of setting up cross-account access in AWS IAM.

**Q.50** What is AWS Identity Federation, and how does it work with IAM?

**Q.51** Explain the differences between IAM policies and resource-based policies in AWS.

**Q.52** How do you rotate access keys for IAM users, and why is key rotation important?

**Q.53** What is AWS Cognito, and how does it relate to IAM in the context of user identity and authentication?

**Q.54** Explain the concept of AWS Security Token Service (STS) and how it relates to temporary credentials in IAM.

**Q.55** What is the limit to attach max number of policies to IAM roles?

**Q.56** What is trusted entity in AWS?

**Q.57** Can you provide an example of a complex IAM scenario you've encountered in AWS and how you resolved it?

**Q.58** Your organization is concerned about security breaches due to compromised AWS access keys. How would you implement a secure access key rotation strategy for IAM users?

**Q.59** Your organization is migrating on-premises applications to AWS. How would you ensure a seamless transition for user authentication and authorization using AWS IAM?

**Q.60** Your organization has adopted AWS Organizations to manage multiple AWS accounts. How would you enforce IAM best practices and policies across these accounts efficiently?

**Q.61** What are service control policies (SCPs) in AWS Organizations?

**Q.62** How do you audit IAM permissions and access?

**Q.63** What is IAM Access Analyzer?

**Q.64** Explain IAM policy conditions and when you would use them.

**Q.65** What is the difference between identity-based and resource-based policies?

---

## S3 (Simple Storage Service)

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.66** What is Amazon S3, and what is its primary purpose within the AWS ecosystem?

**Q.67** Describe the difference between an S3 bucket and an S3 object.

**Q.68** What are the different storage classes available in Amazon S3, and when would you use each one?

**Q.69** How do you make an S3 bucket public or private?

**Q.70** What is an S3 bucket policy?

**Q.71** How do you upload and download files to/from S3?

**Q.72** What is S3 versioning?

**Q.73** What is the maximum file size you can upload to S3?

**Q.74** How do you organize objects in an S3 bucket?

**Q.75** What is the difference between S3 and EBS?

### Additional S3 Questions

**Q.76** Explain the structure of an S3 object's URL (Uniform Resource Locator).

**Q.77** What is S3 data consistency, and how does it work in different scenarios (e.g., read-after-write consistency, eventual consistency)?

**Q.78** How do you secure data stored in an S3 bucket, and what are the key access control mechanisms in S3?

**Q.79** Explain the use of S3 bucket policies and IAM policies in controlling access to S3 resources.

**Q.80** How can you encrypt data in S3, and what are the encryption options available?

**Q.81** What is S3 Object Lock, and how can it be used to enhance data security and compliance?

**Q.82** How do you transfer large data into and out of an S3 bucket?

**Q.83** What is versioning in S3, and what are its benefits and use cases?

**Q.84** Explain the concept of S3 Lifecycle policies and provide examples of when they might be useful.

**Q.85** How can you replicate data between S3 buckets in different AWS regions or accounts?

**Q.86** What is S3 Select, and how does it improve data retrieval efficiency?

**Q.87** What is the Amazon S3 Transfer Acceleration feature, and when might you use it?

**Q.88** What AWS services can be used for monitoring and logging S3 activities, and how would you set up such monitoring?

**Q.89** Explain the purpose of Amazon S3 event notifications, and provide examples of use cases.

**Q.90** What factors influence the cost of using Amazon S3, and how can you optimize costs while using S3 for your data storage needs?

**Q.91** Give examples of industries or scenarios where Amazon S3 is a valuable storage solution.

**Q.92** How can S3 be integrated with other AWS services, such as EC2, Lambda, or Glacier, to build scalable and efficient applications?

**Q.93** Explain how you would architect a backup and disaster recovery solution using S3.

**Q.94** Discuss the advantages and considerations of using Amazon S3 as a content delivery solution (S3 as a static website host or through Amazon CloudFront).

**Q.95** What is S3 Cross-Region Replication (CRR) and Same-Region Replication (SRR)?

**Q.96** How do you enable static website hosting on S3?

**Q.97** What are S3 pre-signed URLs and when would you use them?

**Q.98** Explain S3 Intelligent-Tiering storage class.

**Q.99** What is S3 Glacier and when would you use it?

**Q.100** How do you secure data in transit to and from S3?

---

## VPC (Virtual Private Cloud)

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.101** What is Amazon Virtual Private Cloud (Amazon VPC), and why is it important in AWS networking?

**Q.102** What is the primary difference between a public subnet and a private subnet in a VPC?

**Q.103** What is an Internet Gateway (IGW)?

**Q.104** What is a NAT Gateway and when would you use it?

**Q.105** What is a route table in VPC?

**Q.106** What are security groups in the context of VPC?

**Q.107** What is the default VPC?

**Q.108** What is a CIDR block?

**Q.109** How many VPCs can you create per AWS account per region?

**Q.110** What is the difference between security groups and NACLs?

### Additional VPC Questions

**Q.111** How do you connect a VPC to an on-premises data center, and what are the options available for this connection?

**Q.112** Explain the purpose of Amazon VPC peering and its use cases.

**Q.113** What is the significance of route tables in a VPC, and how do you control traffic routing between subnets?

**Q.114** What are VPC Endpoints, and how do they enhance security and reduce data transfer costs for certain AWS services?

**Q.115** Explain the use of a Bastion Host (Jump Host) in a VPC for secure remote access to instances.

**Q.116** What is Direct Connect, and how does it provide dedicated network connectivity between an on-premises data center and an AWS VPC?

**Q.117** Describe the concept of VPC Flow Logs and their benefits for network monitoring and troubleshooting.

**Q.118** What is AWS Transit Gateway, and how does it simplify network connectivity and management in complex VPC architectures?

**Q.119** Explain the use of AWS PrivateLink for securely accessing AWS services over private connections within a VPC.

**Q.120** What are some best practices for designing VPC architectures that are highly available, fault-tolerant, and scalable?

**Q.121** Give examples of scenarios where you would use VPC peering, VPC endpoints, or Direct Connect to enhance network connectivity.

**Q.122** Discuss strategies for managing and optimizing VPC resources, including IP address allocation, subnet sizing, and route table design.

**Q.123** What are the considerations when setting up VPCs in a multi-region or global configuration for disaster recovery or load balancing?

**Q.124** What is a VPN connection and how does it differ from Direct Connect?

**Q.125** Explain the concept of elastic network interfaces (ENI).

**Q.126** What is a Network ACL (NACL) and how is it different from security groups?

**Q.127** Can you attach multiple Internet Gateways to a single VPC?

**Q.128** What is VPC sharing and when would you use it?

**Q.129** How do you troubleshoot VPC connectivity issues?

**Q.130** What is the maximum CIDR block size you can assign to a VPC?

---

## Load Balancing (ELB/ALB/NLB)

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.131** What is a load balancer and why is it important?

**Q.132** What are the different types of load balancers in AWS?

**Q.133** What is the difference between Application Load Balancer (ALB) and Network Load Balancer (NLB)?

**Q.134** What is a Classic Load Balancer (CLB)?

**Q.135** What is a target group in the context of load balancing?

**Q.136** How do health checks work in AWS load balancers?

**Q.137** What is the difference between layer 4 and layer 7 load balancing?

**Q.138** How do you configure a basic Application Load Balancer?

**Q.139** What is listener in the context of load balancers?

**Q.140** Can a load balancer work across multiple availability zones?

### Additional Load Balancing Questions

**Q.141** When would you choose an Application Load Balancer (ALB) over a Network Load Balancer (NLB), and vice versa?

**Q.142** What is a target group in the context of ALB, and how is it used for routing traffic to instances?

**Q.143** Explain the concept of listeners and rules in load balancer configuration.

**Q.144** What are the health checks performed by AWS load balancers, and how do they impact instance health?

**Q.145** How can you ensure session persistence or stickiness for clients using a load balancer in AWS?

**Q.146** How does AWS ensure high availability for load balancers, and what are the best practices for achieving redundancy?

**Q.147** Explain the use of cross-zone load balancing in AWS, and when would you enable or disable it?

**Q.148** What is the importance of distributing instances across multiple Availability Zones (AZs) when using load balancers in AWS?

**Q.149** Explain the process of configuring SSL/TLS certificates for securing traffic between clients and the load balancer.

**Q.150** What is AWS Web Application Firewall (WAF), and how can it be integrated with a load balancer for application security?

**Q.151** What are blue-green deployments, and how can AWS load balancers be used to facilitate this deployment strategy?

**Q.152** What is connection draining (deregistration delay)?

**Q.153** How do you perform SSL/TLS offloading with load balancers?

**Q.154** What is path-based routing in ALB?

**Q.155** What is host-based routing in ALB?

**Q.156** Can you use a load balancer with Lambda functions?

**Q.157** What are the monitoring metrics available for load balancers?

**Q.158** How do you troubleshoot unhealthy targets in a load balancer?

**Q.159** What is the difference between internal and internet-facing load balancers?

**Q.160** Can you modify the load balancer type after creation?

---

## Auto Scaling

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.161** What is AWS Auto Scaling and why is it important?

**Q.162** What is an Auto Scaling Group?

**Q.163** What is the difference between desired capacity, minimum capacity, and maximum capacity?

**Q.164** What is a launch configuration?

**Q.165** What is a launch template?

**Q.166** What are scaling policies?

**Q.167** What is the difference between target tracking and step scaling?

**Q.168** How does Auto Scaling work with load balancers?

**Q.169** What triggers Auto Scaling to add or remove instances?

**Q.170** What is a cooldown period in Auto Scaling?

### Additional Auto Scaling Questions

**Q.171** Explain the primary components of AWS Auto Scaling.

**Q.172** What is the difference between horizontal and vertical scaling, and how does Auto Scaling facilitate horizontal scaling?

**Q.173** How do you determine the desired capacity and minimum capacity for an Auto Scaling group?

**Q.174** What is difference between Launch Template and Launch configuration?

**Q.175** Explain how scaling policies work in Auto Scaling. What are the different types of scaling policies?

**Q.176** How do you configure triggers and alarms for Auto Scaling policies using Amazon CloudWatch?

**Q.177** What is a cooldown period in Auto Scaling, and why is it important to configure it correctly?

**Q.178** What are the best practices for setting up Auto Scaling for stateful and stateless applications?

**Q.179** Explain how you would handle Auto Scaling for applications with varying workloads throughout the day (e.g., a news website with peak traffic times).

**Q.180** What strategies can you use to minimize costs while using Auto Scaling effectively?

**Q.181** How can you troubleshoot issues related to Auto Scaling, such as instances not launching or scaling events not triggering as expected?

**Q.182** What metrics and logs should you monitor to ensure the health and performance of Auto Scaling groups?

**Q.183** What actions would you take if an Auto Scaling group consistently launches instances with failures or if instances are frequently terminated due to scaling down?

**Q.184** What are lifecycle hooks in Auto Scaling, and how can they be used for advanced customization of instance scaling actions?

**Q.185** Explain the concept of mixed instances in an Auto Scaling group and its benefits.

**Q.186** What is predictive scaling in Auto Scaling?

**Q.187** How do you use Auto Scaling with Spot Instances?

**Q.188** What is warm pool in Auto Scaling?

**Q.189** How do you perform rolling updates with Auto Scaling?

**Q.190** What is instance refresh in Auto Scaling?

---

## ECS (Elastic Container Service)

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.191** What is Amazon ECS and what is it used for?

**Q.192** What is the difference between ECS and EKS?

**Q.193** What is a container in the context of ECS?

**Q.194** What is a task definition in ECS?

**Q.195** What is an ECS cluster?

**Q.196** What is an ECS service?

**Q.197** What are the two launch types in ECS?

**Q.198** What is the difference between EC2 launch type and Fargate launch type?

**Q.199** What is a task in ECS?

**Q.200** How does ECS integrate with other AWS services?

### Additional ECS Questions

**Q.201** What is Amazon ECR (Elastic Container Registry)?

**Q.202** How do you deploy a containerized application on ECS?

**Q.203** What is the ECS agent?

**Q.204** How does ECS handle load balancing?

**Q.205** What is the difference between a task and a service in ECS?

**Q.206** How do you configure auto-scaling for ECS services?

**Q.207** What are the networking modes available in ECS?

**Q.208** How do you manage secrets in ECS?

**Q.209** What is ECS service discovery?

**Q.210** How do you monitor ECS containers and tasks?

**Q.211** What is the difference between bridge and awsvpc network mode?

**Q.212** How do you perform blue-green deployments with ECS?

**Q.213** What is ECS Exec and when would you use it?

**Q.214** How do you troubleshoot failed tasks in ECS?

**Q.215** What is capacity provider in ECS?

**Q.216** How does ECS integrate with CloudWatch for logging?

**Q.217** What are the best practices for optimizing ECS costs?

**Q.218** How do you update task definitions in a running ECS service?

**Q.219** What is the maximum number of tasks that can run in an ECS service?

**Q.220** How do you handle stateful applications in ECS?

---

## CloudFront

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.221** What is Amazon CloudFront and what is it used for?

**Q.222** What is a CDN (Content Delivery Network)?

**Q.223** What is the difference between CloudFront and S3?

**Q.224** What is an origin in CloudFront?

**Q.225** What is a distribution in CloudFront?

**Q.226** What are edge locations?

**Q.227** How does CloudFront improve website performance?

**Q.228** What types of content can CloudFront deliver?

**Q.229** How do you create a CloudFront distribution?

**Q.230** What is caching in CloudFront?

### Additional CloudFront Questions

**Q.231** What is the difference between web distribution and RTMP distribution?

**Q.232** How does CloudFront handle SSL/TLS certificates?

**Q.233** What are signed URLs and signed cookies in CloudFront?

**Q.234** How do you invalidate cached content in CloudFront?

**Q.235** What is CloudFront geo-restriction?

**Q.236** How does CloudFront integrate with AWS WAF?

**Q.237** What is Lambda@Edge?

**Q.238** How do you configure custom error pages in CloudFront?

**Q.239** What is the difference between regional edge cache and edge location?

**Q.240** How do you monitor CloudFront performance?

**Q.241** What are the different cache behaviors in CloudFront?

**Q.242** How do you configure HTTPS with CloudFront?

**Q.243** What is origin failover in CloudFront?

**Q.244** How does CloudFront pricing work?

**Q.245** What is field-level encryption in CloudFront?

**Q.246** How do you troubleshoot CloudFront distribution issues?

**Q.247** What is the TTL (Time To Live) in CloudFront caching?

**Q.248** How do you use CloudFront with S3 for static website hosting?

**Q.249** What are the security best practices for CloudFront?

**Q.250** Can CloudFront cache dynamic content?

---

## CloudWatch

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.251** What is Amazon CloudWatch and what is it used for?

**Q.252** What are CloudWatch metrics?

**Q.253** What are CloudWatch alarms?

**Q.254** What are CloudWatch logs?

**Q.255** What is the difference between basic and detailed monitoring in CloudWatch?

**Q.256** How do you create a CloudWatch alarm?

**Q.257** What are custom metrics in CloudWatch?

**Q.258** What is a CloudWatch dashboard?

**Q.259** How long does CloudWatch retain metrics data?

**Q.260** What is a CloudWatch namespace?

### Additional CloudWatch Questions

**Q.261** What is CloudWatch Events (now Amazon EventBridge)?

**Q.262** How do you send logs to CloudWatch from EC2 instances?

**Q.263** What is the CloudWatch agent?

**Q.264** What are CloudWatch Insights?

**Q.265** How do you query logs in CloudWatch?

**Q.266** What is CloudWatch Synthetics?

**Q.267** What are composite alarms in CloudWatch?

**Q.268** How do you monitor AWS Lambda functions with CloudWatch?

**Q.269** What is CloudWatch Container Insights?

**Q.270** What is CloudWatch Application Insights?

**Q.271** How do you set up CloudWatch cross-account monitoring?

**Q.272** What are anomaly detection alarms in CloudWatch?

**Q.273** How do you export CloudWatch logs to S3?

**Q.274** What is CloudWatch Metric Math?

**Q.275** How do you create custom CloudWatch dashboards?

**Q.276** What are the different CloudWatch alarm states?

**Q.277** How do you troubleshoot missing metrics in CloudWatch?

**Q.278** What is the difference between CloudWatch Logs and CloudTrail?

**Q.279** How do you optimize CloudWatch costs?

**Q.280** What is CloudWatch ServiceLens?

---

## Route 53

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.281** What is Amazon Route 53 and what is it used for?

**Q.282** What is DNS (Domain Name System)?

**Q.283** What are the main features of Route 53?

**Q.284** What is a hosted zone in Route 53?

**Q.285** What are DNS records?

**Q.286** What is the difference between public and private hosted zones?

**Q.287** What is an A record?

**Q.288** What is a CNAME record?

**Q.289** How do you register a domain with Route 53?

**Q.290** What is TTL (Time To Live) in DNS?

### Additional Route 53 Questions

**Q.291** What are top-level domains (TLDs) and second-level domains, and how do they relate to Route 53?

**Q.292** Explain the primary services provided by Amazon Route 53.

**Q.293** Walk me through the process of registering a domain name with Amazon Route 53.

**Q.294** What are the differences between domain registration and DNS hosting, and how does Route 53 handle both?

**Q.295** How can you migrate a domain from another registrar to Route 53?

**Q.296** Explain the various routing policies supported by Route 53, including Simple, Weighted, Latency-Based, Geolocation, and Failover policies.

**Q.297** What is the purpose of a weighted routing policy, and when would you use it?

**Q.298** How does the latency-based routing policy work, and when is it beneficial for optimizing user experience?

**Q.299** What are health checks in Amazon Route 53, and how can they be used to monitor the health of resources?

**Q.300** How can you configure a failover routing policy with Route 53, and what role do health checks play in this scenario?

**Q.301** Discuss best practices for optimizing Route 53 for high availability and low latency.

**Q.302** Give examples of scenarios where you would use Route 53 for global load balancing, failover, or disaster recovery.

**Q.303** Explain how you can use Route 53 in conjunction with AWS services like Elastic Load Balancing (ELB) for scalable and resilient architectures.

**Q.304** Explain different types of records in Route 53 (Like A, AAAA, NS, SOA, etc.)

**Q.305** What is geoproximity routing in Route 53?

**Q.306** What is multivalue answer routing?

**Q.307** How does Route 53 traffic flow work?

**Q.308** What is Route 53 Resolver?

**Q.309** How do you troubleshoot DNS resolution issues with Route 53?

**Q.310** What is DNSSEC and does Route 53 support it?

---

## Lambda

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.311** What is AWS Lambda and what is it used for?

**Q.312** What is serverless computing?

**Q.313** What are the benefits of using Lambda?

**Q.314** What is a Lambda function?

**Q.315** What programming languages does Lambda support?

**Q.316** What is an event source in Lambda?

**Q.317** How does Lambda pricing work?

**Q.318** What is the maximum execution time for a Lambda function?

**Q.319** What is cold start in Lambda?

**Q.320** How do you trigger a Lambda function?

### Additional Lambda Questions

**Q.321** What programming languages are supported for writing Lambda functions, and how can you package and deploy them?

**Q.322** Describe the benefits of using AWS Lambda for application development and architecture.

**Q.323** What are event sources in Lambda, and how do they enable serverless event-driven applications?

**Q.324** Explain the use of Amazon EventBridge (formerly CloudWatch Events) in connecting event sources to Lambda functions.

**Q.325** What is concurrency in AWS Lambda, and how is it managed?

**Q.326** How does AWS Lambda automatically scale to accommodate high traffic or a large number of requests?

**Q.327** Explain the concept of "statelessness" in AWS Lambda, and how can you manage application state when necessary?

**Q.328** What is the benefit of using AWS SAM (Serverless Application Model) for defining and deploying Lambda-based serverless applications?

**Q.329** Discuss best practices for optimizing Lambda functions for cost, performance, and security.

**Q.330** What is Lambda layers and when would you use them?

**Q.331** How do you manage environment variables in Lambda?

**Q.332** What is the difference between synchronous and asynchronous invocation in Lambda?

**Q.333** What is provisioned concurrency in Lambda?

**Q.334** How do you handle errors in Lambda functions?

**Q.335** What is Lambda Destinations?

**Q.336** How do you monitor Lambda functions?

**Q.337** What is the maximum memory allocation for a Lambda function?

**Q.338** How do you connect Lambda to a VPC?

**Q.339** What are the limitations of AWS Lambda?

**Q.340** How do you deploy Lambda functions using CI/CD?

---

## CloudFormation

### ⭐ Essential Questions for Junior DevOps Engineers

**Q.341** What is AWS CloudFormation and what is it used for?

**Q.342** What is Infrastructure as Code (IaC)?

**Q.343** What is a CloudFormation template?

**Q.344** What is a CloudFormation stack?

**Q.345** What are the main sections of a CloudFormation template?

**Q.346** What is the difference between JSON and YAML templates in CloudFormation?

**Q.347** What are CloudFormation resources?

**Q.348** What are CloudFormation parameters?

**Q.349** What are CloudFormation outputs?

**Q.350** How do you create a stack in CloudFormation?

### Additional CloudFormation Questions

**Q.351** What are CloudFormation mappings?

**Q.352** What are CloudFormation conditions?

**Q.353** What is intrinsic function in CloudFormation?

**Q.354** What is the Ref function in CloudFormation?

**Q.355** What is the GetAtt function in CloudFormation?

**Q.356** How do you update a CloudFormation stack?

**Q.357** What are change sets in CloudFormation?

**Q.358** What is stack drift in CloudFormation?

**Q.359** How do you delete a CloudFormation stack?

**Q.360** What happens to resources when you delete a stack?

**Q.361** What is CloudFormation nested stack?

**Q.362** What are CloudFormation StackSets?
