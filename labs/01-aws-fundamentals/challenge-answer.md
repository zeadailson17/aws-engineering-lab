# Lab 01 — Architecture Challenge

## 1. AWS Region Selection

I would choose `sa-east-1` (São Paulo, Brazil) as the primary AWS Region.

The main reason is the geographical proximity to the majority of the application's users, who are located in Brazil.

Hosting the application closer to its users is expected to reduce network latency and improve the overall user experience.

Before making the final decision, I would also evaluate:

- AWS service availability in the selected Region.
- Infrastructure and data transfer costs.
- Data residency and regulatory requirements.
- Connectivity with external systems and dependencies.
- Real latency measurements from the application's users.

## 2. High Availability Architecture

To achieve high availability, I would deploy the application across at least two Availability Zones within the selected Region.

The architecture would include:

- One VPC spanning multiple Availability Zones.
- Public subnets for the Application Load Balancer.
- Private subnets for application workloads.
- Application Load Balancer distributing traffic across healthy targets.
- EC2 Auto Scaling Group distributing application instances across Availability Zones.
- Amazon RDS configured with Multi-AZ for database availability.
- Amazon S3 for object storage.
- Monitoring and health checks to detect failures.

## 3. Failure Management

If one Availability Zone becomes unavailable:

1. The Application Load Balancer routes requests to healthy targets in the remaining Availability Zones.
2. Auto Scaling can replace unhealthy application instances.
3. Amazon RDS Multi-AZ can automatically fail over to its standby database instance.
4. Monitoring systems detect and report the incident.

The application should also avoid depending on local instance state, allowing workloads to operate through healthy instances in other Availability Zones.

## 4. Additional Resilience Considerations

Multi-AZ architecture protects against isolated Availability Zone failures, but it does not guarantee protection against an entire Region outage.

For workloads requiring regional disaster recovery, I would evaluate a secondary AWS Region, data replication, recovery procedures, and defined RTO and RPO objectives.

## Conclusion

My approach is to prioritize a highly available Multi-AZ architecture in `sa-east-1`, ensuring that critical components are distributed across independent Availability Zones.

A Multi-Region strategy would be considered when business continuity, regulatory requirements, or regional disaster recovery objectives justify the additional complexity and operational costs.

## 5. Multi-AZ Failure Scenario

### Initial Answer

The application continues serving requests through AZ B,
while RDS performs an automatic failover to the standby instance.

### Technical Assessment

The primary database failover can temporarily interrupt
existing database connections.

The application must re-establish connections using
retry mechanisms, exponential backoff and DNS refresh.

### Key Learnings

- Multi-AZ does not mean zero downtime.
- Application connections must recover after failover.
- Remaining AZ capacity must support the workload.
- Database recovery and application recovery are different.
- High availability must be validated through failure testing.