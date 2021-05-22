## Basics



### Compute



Elastic Compute Cloud(EC2)



名词解释: 

* Launch configuration:

* Autoscaling group:

* Load balancer: 只能在同一个region 中进行balance

* Target group:

* Elastic IP 是跟着Accounts走的 可以assign给不同的instance

* Pricing

* On-Demand instance: 按秒计价收费

* Spot EC2 instance: 可能会被随时interrupt stop/terminate 可以选Spot Block来限定一个确定时间



* Dedicated Hosts:

* Reserved instance: 签订长期合约 1年/3年

\* Standard

\* Convertible: 可以更改instance type, OS, payment option

\* AMI(Amazon Machine Image): reusable template include OS + additional installations

\* Status

\* Running

\* Stop: 关机 但是EBS还attach

\* Terminate: 停止使用整个instance, root device volume is deleted

\* Root Device Volumes: contains the image used to boot the instance

\* Instance Store-backed instance: Stop之后就被删除 不存在stop状态 只有Running 和 Terminate

\* Amazon EBS-backed instance: 会保留在EBS中

**重点 / 考点**

\* Launch configuration 如果需要进行修改的话 必须要新建一个 不能在之前的config上修改

\* 三种 Scaling policy

\* step scaling policy: a set of metrics

\* simple: single metrics

\* target tracking: dynamic + specific metric

\* Placement group的区别

\* 选择一个合适类型的instance

\* vCPU-based On-Demand Instance limit per region

\* EC2 Termination policy: terminate 哪一个instance的policy



### Networking



#### VPC: Virtual Private Cloud



**名词解释**

* Route Table: contains a set of rules, called routes, that are used to determine where network traffic is directed
* Subnet: a range of IP addresses in your VPC. add AWS resources into a specified subnet.
* Public subnet: resources that must be connected to the internet
* Private subnet: for resources that won't be connected to the internet.
* Internet gateway: instaces <=> public internet
* NAT gateways: private IP <=> NAT <=> public internet
* Egress-only internet gateways: IPv6 traffic
* Elastic Network Interface(ENI): virtual network interface you can attach to an instance in VPC
* Elastic IP address: a reserved public IP address you can assign to any EC2 instance in a particular region
* Security Group(instance level): a virtual firewall control inbound and outbound traffic for your **instances**
* Network Access Control List(NACL): **subnet** level additional firewall
* NAT: Network Address Translation 在public IP 和 private IP 之间做切换来解决公共IP数量不足的问题
* VPC Endpoint: 用来和其他不在VPC内部的AWS建立connection, 比如S3, DynamoDB
* Interface Endpoints
* Gateway Endpoints

* DHCP server: assign a computer an IP address + Subnet mask + Default gateway + DNS server 否则用人工添加会很麻烦

* VPC Flow Logs: capture information about the **IP traffic** going to and from network interfaces in your VPC

* VPC Peering: connect the different VPCs(between your VPCs, or with a VPC in another AWS account) 两个network之间的instance都可以相互通信



**Default vs. Non-Default VPC:**

\* Default include internet gateway, private IPv4 address + public IPv4 address

\* Non-Default: Subnets that you create in your non-default VPC and additional subnets that you create in your default VPC are called non-default subnets

\* **only private IPv4 address**, no public IPv4 address unless you specifically assign one at launch

\* need to attach an internet gateway and associating an Elastic IP address with the instance

**Security Group vs. Network ACL:**

\* Security Group:

\* instance level

\* only support allow rules

\* stateful: return traffic is automatically allowed, regardless of any rules

\* evaluate all rules before deciding whether to allow traffic

\* Network ACL (NACL):

\* subnet level

\* support allow rules and deny rules

\* stateless: return traffic must be explicitly allowed by rules

\* process rules in number order when deciding whether to allow traffic(有冲突的时候取number小的/更靠前的)

**重点 / 考点:**

\* Bastion host

\* NAT Gateway / NAT Instance: 只出不进 禁止public network的traffic



#### Direct Connect



#### Route 53



### Storage



#### S3 Simple Storage Service

S3: simple web services interface to store and retrieve any amount of data from anywhere on the web.

* safe place to store files
* It is Object-based storage

* The data is spread across multiple devices and facilities
* S3 is a universal namespace. must be unique globally -> web address

* Object based

* Key: name of the object

* Value: data and is made up of a sequence of bytes

* Version ID: version

* Metadata: Data about the data you are storing

* Subresources

* Access Control Lists

* Consistency Model:

* Read After Write for PUTS of new Objects

* Eventual Consistency: overwrites PUTS and DELETES





S3 Storage Class:

* S3 Standard

* S3 - IA : 更便宜 更少的操作频率

* S3 One Zone - IA: 只在一个region内操作 不涉及到多个region间的调用

* S3 - Intelligent Tiering: 动态调整价格

* S3 Glacier: for data archiving. retrieval times from mins to hours

* S3 Glacier Deep Archive: 最便宜的 retrieval time of 12 hours

* S3 URI and Amazon Resource Name(ARN)

* Reduced Redundancy Storage (RRS) is an Amazon S3 storage option that enables customers to store noncritical, reproducible data at lower levels of redundancy than Amazon S3’s standard storage.



S3 Encryption:

* Server-Side Encryption – Request Amazon S3 to encrypt your object before saving it on disks in its data centers and then decrypt it when you download the objects.

* Client-Side Encryption – Encrypt data client-side and upload the encrypted data to Amazon S3. In this case, you manage the encryption process, the encryption keys, and related tools.





### Database

### Application Management

### Security and Identity

### Application Integration

#### SNS

**名词解释**

**重点 / 考点**

#### SQS

**名词解释**

* Long/Short Polling
* Visibility Timeout

**重点 / 考点**







## Case Study



AWS case studies: https://aws.amazon.com/solutions/case-studies/

Netflix on AWS: https://aws.amazon.com/solutions/case-studies/netflix/

Intuit on AWS: https://aws.amazon.com/solutions/case-studies/Intuit/



## 错题整理



## Service 对比

EFS vs. EBS

S3 vs. EFS vs. EBS





### Step Functions 

**名词解释**

**重点 / 考点**

### AWS CloudFormation

**名词解释**

**重点 / 考点**
### AWS Config 
**名词解释**

**重点 / 考点**

\### EC2

**名词解释**

\* Key pairs:



##### Placement groups:

* Cluster: 全部instance在同一个group中

* Partition: spread EC2 instances across logical partitions

* Spread: 每个instance相互独立 can span multiple AZ in the same Region





* Security groups:

* Load balancers:

* Volumes(EBS):









**名词解释**

* Lambda@Edge



**重点 / 考点**

\* Lambda Destination

*



\* 支持的操作

\* cross region

\* cross account

\* 不支持的操作

\* Overlapping CIDR blocks: IP 不能重叠 ![db24b80640923b62f2f7927f01d56e78.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p251)

\* Transitive peering: A => B => C 不能传递 ![4b0c13140f83c1510ff678557d040507.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p252)

\* Edge to edge routing through a gateway or private connection 不能extend![17395441248bdabb30d557c0cc9dbfcd.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p253)

https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html

\#### Compare



\### API Gateway

可以Set up 各种API



\## Security & Identity

\### IAM

![4ad504016a173143504726a72fd3d87f.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p283)

本质是对你的account账号上的资源进行一种更细致的管理

Reference:

[深入理解IAM和访问控制-知乎陈天](https://www.zhihu.com/column/p/20330438)

**名词解释**

\* IAM Role / Group / User

\* Groups: a collection of IAM users, you can attach access control policies to a group

![ce7efb044607b482c9c9906226fb8e1f.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p284)

\* Users: user是在你的account之内的 可以用另外的账号密码进行登录

![d404e163175cd52ce0b85f9750f95712.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p285)

\* Roles: IAM User can assume a role to temporarily take on different permissions for a specific task. 针对于某一个具体资源或者服务使用的临时授权 更加领过

\* Policies

\* Identity providers

**重点 / 考点**

IAM policy 和 Access Keys的区别

Access Key 是给EC2用的, 作为一种认证信息来使用，不是用来加密的

STS: 发一个临时token来做认证 等价于IAM的Access Key

Key pairs .pem file 用来登录EC2

STS: Security Token Service

**Q&A**:

identity provider 是什么?

Active Directory

SAML 2.0-Based ?

SSL encryption: encrypt data when in-transit

\### KMS (Key Management Service)

![b189dc085e5d8e1718e97ad0fb9c67ab.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p281)

\## Compliance

\### CloudWatch

**名词解释**

**重点 / 考点**

\* Memory Utilization 不是default的, 需要手动set up 【在console里面确认】

\### CloudTrail

**名词解释**

**重点 / 考点**

【问题】

KMS: Key Management Service

IAM





## 

\* Use a customer master key (CMK) stored in AWS Key Management Service (AWS KMS).

\* Use a master key that you store within your application. 如果用的是自定义的key，可以不share给AWS,更加安全

in transit: as it travels to and from Amazon S3

at rest: while it is stored on disks in Amazon S3 data centers

\* Bucket Policy:

[aws-doc-example-bucket-policies]( https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html)

![d8f058a890e5e90e6829d6742305a774.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p280)

read-after-write consistency moPUT: PUT + DELETE

\* Transfer Acceleration: 从哪里transfer到哪里? 在全球各地的S3 发送到一个中心S3-bucket来集中处理数据用的需要额外收费，对于时效性敏感的数据适用. Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket.

Versioning: 什么的version S3 bucket的version? multiple versions of the same file

\* Lifecycle management

![d10a689da22c97ddd365f769d4296588.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p277)

\* Cross-region replication (set in replication rule Destination)

![940baaf4e1beca7aef77672a128667b4.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p278)

\* S3 bucket properties

\* Version

\* Server access logging

\* Static website hosting

\* Object-level logging: record object-level API activity by using CloudTrail data events.

\* Tags: a key-value pair that represents a label that you assign to a bucket

\* Transfer acceleration: fast,easy, and secure transfers of files over long distances between your client and an S3 bucket.

\* Events: S3 bucket events

\* expedited retrieval for S3 Glacier

\* A presigned URL: gives you access to the object identified in the URL, provided that the creator of the presigned URL has permissions to access that object. All objects and buckets by default are private. The presigned URLs are useful if you want your user/customer to be able to upload a specific object to your bucket, but you don't require them to have AWS security credentials or permissions. 类似于Google doc的分享链接

eventual consistency model:

可能会看到已经被删除的object因为还没有最终同步

read-after-write consistency: ?? 这是什么一致性

为什么需要不同的一致性

不同操作的consistency model是不同的 需要进行一个 ??

**重点 / 考点**

Athena: query service to analyze data directly in S3 using standard SQL

\### EBS (Elastic Block Store)

persistent storage: the storage is independent outside the life span of an EC2 instance.

Solid state drives (SSD) — Optimized for **transactional workloads** involving frequent read/write operations with small I/O size, where the dominant performance attribute is IOPS.

Hard disk drives (HDD) — Optimized for **large streaming workloads** where the dominant performance attribute is throughput.

\* SSD

![de468441f924dfa3de0b90ead98d7ba9.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p267)

small data-analytical boot volume

\* HDD

![6491e5a424a29f195ca0e0564897bee2.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p268)

large and sequential I/O

Throughput vs. IOPS

Here is a list of important information about EBS Volumes:

\* When you create an EBS volume in an Availability Zone, it is automatically replicated within that zone to prevent data loss due to a failure of any single hardware component.

\* An EBS volume can only be attached to one EC2 instance at a time.

\* After you create a volume, you can attach it to any EC2 instance in the same Availability Zone

\* An EBS volume is off-instance storage that can persist independently from the life of an instance. You can specify not to terminate the EBS volume when you terminate the EC2 instance during instance creation.

\* EBS volumes support **live configuration** changes while in production which means that you can modify the volume type, volume size, and IOPS capacity without service interruptions.

\* Amazon EBS encryption uses 256-bit Advanced Encryption Standard algorithms (AES-256)

Use Data Lifecycle Manager(DLM) to automate the creation of EBS snapshot

OLTP: Transactional e.g. store user data, passwords, previous transactions...

OLAP: Analitical e.g. what is the most sold product

https://stackoverflow.com/questions/21900185/what-are-oltp-and-olap-what-is-the-difference-between-them

\### EFS (Elastic File System)

EFS 的life cycle policy 最多只有90天

Mount Target

\#### Compare





\### AWS Storage Gateway

3 types:

\* File Gateway

\* Volume Gateway

\* Tape Gateway

EC2 security group

\#### Compare

Data Sync vs. Storage Gateway vs. Data Migration Service

\* Data Sync: 从本地的on-premise上传到远端AWS上

**重点 / 考点**

\* 需要用Hybrid cloud structure的时候考虑用Storage Gateway

\## Database

\### DynamoDB

![196978c8b75da818e293e978bf14e0e3.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p282)

关键字: AWS fully-managed, scalable, No-SQL(Key-Value pair), highly available

**名词解释**

\* DynamoDB Streams: captures a time-ordered sequence of item-level modifications in any DynamoDB table and stores this information in a log for up to 24 hours. Applications can access this log and view the data items as they appeared before and after they were modified, in near-real time.

默认是Diable的,需要手动Enable

**重点 / 考点**

\* DynamoDB Streaming 可以直接trigger Lambda

\### Relational Database Service (RDS)

synchronous data replication in RDS ?

RDS Read Replica -> Asynchronous Replica

\#### Compare

Read Replicas vs. Multi-AZ Deployments

\### Amazon Redshift

A cloud warehouse: enhance VPC之后就可以使用VPC的服务

\* OLAP systems

\* Enhanced VPC Routing: supports the use of standard VPC features

【问题】

Data Sync

St
