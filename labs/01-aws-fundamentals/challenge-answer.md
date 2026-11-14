# Lab 01 — Architecture Challenge: Reference Answer

> **Important:** This is a suggested reference answer prepared for study. It is not the learner's personal answer. Rewrite it in your own words after reviewing the trade-offs.

## Scenario

A company has a web application used primarily by people in Brazil. It requires high availability, a separate database, file storage, and room to scale.

## 1. Which Region would you select, and why?

I would begin by evaluating **South America (São Paulo), `sa-east-1`**, because the primary users are in Brazil. Keeping the main workload near its users is a reasonable starting point for reducing network latency. Before making the final decision, I would verify that all required services and features are available in that Region, measure application latency, compare total cost (including data transfer), and confirm regulatory and data-residency requirements.

I would not choose a Region based on geography alone. Requirements and measurements should drive the final decision.

## 2. How would you design for an AZ failure?

I would deploy the application across at least two Availability Zones in `sa-east-1`:

- An internet-facing Application Load Balancer configured with subnets in at least two AZs.
- Application compute in private subnets in both AZs, with multiple instances or tasks and health checks.
- A scaling or replacement mechanism so unhealthy application capacity can be replaced.
- A database deployment configured for Multi-AZ operation, if supported by the selected engine and compatible with the application's recovery requirements.
- Monitoring, alerting, backups, and regular failover/recovery tests.

The application should avoid relying on local instance storage for important user state. Sessions and shared data should be stored in suitable shared or managed services so another healthy application instance can continue serving requests.

## 3. Where would the database and file storage live?

I would place the database in private database subnets across multiple AZs and restrict access so only the application tier can connect to the database port. I would select an appropriate RDS Multi-AZ configuration after deciding the engine, recovery objectives, and read/write requirements.

I would store uploaded files in an S3 bucket in the selected Region. S3 Standard is designed for data redundancy across multiple Availability Zones. The application can use an S3 Gateway VPC Endpoint to access S3 from the VPC without requiring a public IP or NAT Gateway for that S3 traffic. Bucket policies and IAM permissions should follow least privilege.

## 4. What does the high-level architecture look like?

1. Users resolve the application DNS name.
2. Requests reach the regional Application Load Balancer.
3. The load balancer routes traffic to healthy application instances/tasks in private subnets across AZs.
4. The application accesses the database through private networking.
5. The application accesses S3 through an S3 VPC Gateway Endpoint.
6. Monitoring and alerting provide operational visibility.

See [`architecture.mmd`](./architecture.mmd) for the diagram source.

## 5. What limitations or trade-offs should be considered?

- Multi-AZ does not guarantee zero downtime. Connection interruption, database failover, health-check timing, and application retry behavior must be considered.
- Two AZs improve resilience against an AZ-level issue, but they do not protect against every Region-wide event. A multi-Region disaster-recovery design is a separate requirement with additional complexity and cost.
- NAT Gateways in each AZ can reduce cross-AZ dependencies for outbound traffic, but increase cost. The design should use VPC endpoints for supported AWS services where appropriate and evaluate actual egress needs.
- S3 is a regional service; the application should not assume that the bucket is deployed into a subnet or a specific AZ.
- Capacity must be sufficient in the surviving AZ(s) to handle the workload during a failure.
- Backups, restore tests, observability, and operational runbooks are necessary; architecture diagrams alone do not prove recoverability.

## 6. What I would validate before production

- Required services and features are available in `sa-east-1`.
- Load balancer health checks and routing work as expected.
- Application instances/tasks can be replaced and scaled.
- The application remains functional when an AZ's application targets become unhealthy.
- Database failover behavior and application reconnection logic meet the recovery objectives.
- S3 access is private where intended and IAM/bucket policies enforce least privilege.
- Backups can be restored and recovery procedures are documented.
- CloudWatch metrics, logs, dashboards, and alarms cover critical dependencies.
- Cost estimates include NAT Gateways, load balancing, database Multi-AZ, storage, and data transfer.

## 7. Personal answer — complete this section

After studying the reference answer, write your own response without copying it verbatim.

**Region choice and justification:**

_Write your answer here._

**How I would handle an AZ failure:**

_Write your answer here._

**Database and object-storage design:**

_Write your answer here._

**Main risks and trade-offs:**

_Write your answer here._

## Sources

- [AWS Regions and Availability Zones](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions-availability-zones.html)
- [AWS Regions](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions.html)
- [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Amazon S3 data durability](https://docs.aws.amazon.com/AmazonS3/latest/userguide/DataDurability.html)
- [Amazon RDS Multi-AZ deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)
