# AWS-ecommerce-architecture
Introduction

The number of ecommerce vendors is tremendously growing globally, and it might become very difficult to handle large traffic at different times of the day and different days of the year. This, in addition to building, managing, and maintaining IT infrastructure on-premises data centers can present challenges to their businesses’ scalability, performance, and growth. So, to make the workload lighter, is by embracing the cloud where we can use provided resources to manage our infrastructure easily.

An ecommerce application should be flexible and adaptable to various clients:

•	Mobile app (android and IOS)

•	Desktop app

•	Responsive web app

The client site of application should:

•	Serve product related information.

•	 Serve product images & videos.

•	Serve customer related data.

•	To take orders, provide order status and process refunds.

The backend then should be able:

•	Complete transaction with a payment gateway or gateways

•	Update the financial accounting system.

•	Put into and receive information from an inventory system or systems.

•	Put into and receive information from a fulfillment system or systems.

•	Put customer related information into a CRM (Customer Relationship Management).

•	Send notifications to customers & partners on order & account matters.

•	Show recommendations to customers.

•	Collect and process data for analysis.

Customers on the hand want to search and find products which they are interested in quickly and customers all around the world want to make purchase at any time. 
Customers would also expect the pages to load very fast and the application should be highly available. 

Ecommerce Architecture Base on Business Requirements

Base on our business requirement a simple ecommerce architecture should look like 
![image](https://user-images.githubusercontent.com/88759996/234212986-23e4213a-0740-4289-ade8-294142116247.png)

Managing this application becomes very difficult when the customer base grows. With the tools provided by AWS, we can build a compelling, highly performant, highly available, and scalable website with a searchable product catalog that is accessible with very low latency.

This architecture is made of several AWS services which are: amazon route 53, CloudFront, Cognito, amazon S3, amazon ECS, EC2, RDS, DynamoDB, ElastiCashe, OpenSearch service, amazon pinpoint, amazon personalize. It also contains a collection of polyglot microservices which are hosted on a container called amazon elastic container service (EC2 type) that represent domain constructs such as products, carts, orders, and users as well as services for search and recommendations. While both the e-commerce frontend application and back-office frontend is hosted EC2 Auto Scaling EC2 cluster environment. Both the frontend application makes the static content and web content served better by leveraging Amazon CloudFront and Amazon S3

AWS Ecommerce Architectural Diagram
![image](https://user-images.githubusercontent.com/88759996/234213509-aa80208d-55be-4cca-8675-e7b63683a91b.png)

System Overview

•	Amazon Route 53:  For making DNS request to the ecommerce application. It is a scalable and highly available Domain Name System service.

•	CloudFront: is a content distribution network (CDN) with edge locations around the globe. It can cache static and streaming content and deliver dynamic content with low latency from locations close to the customer.

•	Amazon S3: For storage. It stores all the static content such as images, videos, and log files from microservices like CloudFront.

•	Amazon Cognito: An authentication service used to authenticate users and manage users’ sessions.

•	Amazon RDS: To provide high availability, the user and orders databases are hosted redundantly on a multi-AZ (multi–Availability Zone) deployment of Amazon Relational Database Service (Amazon RDS) within private subnets that are isolated from the public Internet.

•	Amazon Personalize: Amazon Personalize provides similar item recommendations, search re-ranking based on user preferences, and product recommendations based on user item interactions.

•	Amazon Pinpoint: Amazon Pinpoint to add the ability to dynamically send welcome messages, abandoned cart messages, and messages with personalized product recommendations to the customers.

•	Amazon OpenSearch Service: Provide a highly scalable and fast search functionality.

•	Amazon DynamoDB: Amazon DynamoDB is a fully managed, high performance, NoSQL database service that is easy to set up, operate, and scale. It is used both as a session 

store for persistent session data, such as the shopping cart, and as the product database. Because DynamoDB does not have a schema, we have a great deal of flexibility in adding new product categories and attributes to the catalog.

•	Amazon ElastiCache: Amazon ElastiCache is used as a session store for volatile data and as a caching layer for the product catalog to reduce I/O (and cost) on DynamoDB.

•	Polyglot microservices: A collection of polyglot microservices host in amazon elastic container service that represent domain constructs such as products, carts, orders, and users as well as services for search and recommendations.

•	Ecommerce frontend application: The e-commerce frontend application is deployed by AWS EC2 Auto Scaling, which automatically handles the details of capacity provisioning, load balancing, auto scaling, and application health monitoring.

•	Back-office frontend application: The back-office frontend application is deployed by AWS EC2 Auto Scaling, which automatically handles the details of capacity provisioning, load balancing, auto scaling, and application health monitoring.

Important factors to take into consideration.

•	Scalability: The architecture is highly scalable, and it is scaled horizontally using auto scaling group base on scaling policies.

•	Performance: CloudFront delivers the application with very low latency and Amazon CloudWatch alarms are created on the Auto Scaling group for CPU utilization and to add/remove instances.

•	Security: Highly secured with strong security group policies and IAM roles.

•	Availability: The load balancer health check checks the health of the instances, and the load balancer and auto scaling group are multi-A-Z enabled.

•	Price Optimization: Since the application is used globally let’s consider 5million of users. These 5million users are not going to be active every day. So, let’s consider 1million active users per day, this therefore means we have 1million request per day. 

Memory optimized r6i.2xlarge = $0.3334/1yr and $0.2286/3yrs for a reserved instance

$0.2286 * 6 instances = 2.3334/1yr and $1.3716/3yrs

Route 53 : $0.60 per million queries/month for latency base = $0.60 x 5million queries per month = $3.0/month = $36.0/year

Amazon RDS: db.m6g.2xlarge Reserved Instance = $284.19 per month and $3,410.28 per year

Amazon DynamoDB: $1.25 per million write request units, $0.25 per million read request units, $0.10 per GB-month

Amazon Cognito: 5million active users per month * $0.00460/user

CloudFront: price class all $0.847/month and $10.164/year

Amazon S3: 1 TB of storage provisioned = $60.0/month

Amazon Pinpoint:$500 for 5million email per month, $5.0 for 5million push notifications per month, $510 for in app messaging per month

Amazon OpenSearch service: m6g.2xlarge.search = $257.69/month

Amazon Personalize: $0.018 per 100,000 users, there for, 5milllion users = $0.90 per month



