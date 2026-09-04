<div align="center">

# Charles Chukwunonso

### AWS Cloud Engineer · Solutions Architecture · Linux

I design and build secure, reliable, and cost-aware systems on AWS.

[![Portfolio](https://img.shields.io/badge/Portfolio-View%20Website-B8D8F8?style=flat-square&logo=amazonwebservices&logoColor=061A2B)](https://agu-nwa.github.io/Agu-nwa/)
[![AWS Projects](https://img.shields.io/badge/AWS-View%20Projects-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white)](https://github.com/Agu-nwa?tab=repositories)
[![GitHub](https://img.shields.io/badge/GitHub-Agu--nwa-181717?style=flat-square&logo=github)](https://github.com/Agu-nwa)

</div>

## About

I design and deploy AWS solutions with a focus on security, reliability, performance, and cost. My work covers cloud architecture, networking, Linux administration, and infrastructure operations.

This portfolio shows what I've built, the services I've used, and the decisions behind each solution.

## Featured projects

### [Highly Available AWS Web Architecture](https://github.com/Agu-nwa/-aws-ha-arch)

A highly available web architecture running across two Availability Zones, with elastic compute, managed PostgreSQL, and separate delivery paths for application and static traffic.

**Stack:** VPC · EC2 · ALB · Auto Scaling · RDS PostgreSQL · S3 · CloudFront · IAM<br>
**Implemented:** Multi-AZ compute, health-based traffic distribution, EC2 replacement testing, RDS standby replication, and private S3 delivery through CloudFront<br>
**Documentation:** [Architecture and traffic flow](https://github.com/Agu-nwa/-aws-ha-arch/blob/main/architecture/architecture.md) · [Design decisions](https://github.com/Agu-nwa/-aws-ha-arch/blob/main/architecture/decisions.md)

<details>
<summary><strong>View architecture diagram</strong></summary>

```mermaid
flowchart TB
    Users([Internet Users]) --> ALB[Application Load Balancer]
    Users --> CF[Amazon CloudFront]
    CF --> S3[(Private Amazon S3 Bucket)]
    subgraph VPC[Amazon VPC - 10.0.0.0/16]
        ALB --> TG[Target Group]
        subgraph ASG[Auto Scaling Group - Min 2 / Max 4]
            EC2A[EC2 + Nginx - AZ A]
            EC2B[EC2 + Nginx - AZ B]
        end
        TG --> EC2A
        TG --> EC2B
        EC2A --> Endpoint[RDS Endpoint]
        EC2B --> Endpoint
        Endpoint --> Primary[(RDS PostgreSQL Primary)]
        Primary -. Synchronous replication .-> Standby[(RDS PostgreSQL Standby)]
    end
```

</details>

---

### [EC2 + Nginx Web Server](https://github.com/Agu-nwa/AWS-Personal-Project)

An Ubuntu web server deployed on Amazon EC2 and configured to serve a web page with Nginx.

**Stack:** EC2 · Security Groups · Ubuntu · Nginx · SSH<br>
**Implemented:** Instance provisioning, key-based remote access, HTTP access rules, Nginx installation, and web content deployment

<details>
<summary><strong>View deployment flow</strong></summary>

```mermaid
flowchart LR
    Visitor([Website Visitor]) -->|HTTP| SG[Security Group]
    Admin([Administrator]) -->|SSH| SG
    SG --> EC2[Ubuntu EC2 Instance]
    EC2 --> Nginx[Nginx Web Server]
    Nginx --> Page[Hosted Web Page]
```

</details>

---

### [Server Discovery & Baseline Assessment](https://github.com/Agu-nwa/Server-Discovery-and-Baseline-Assessment)

A documented assessment of an Ubuntu EC2 server used to understand its current state before configuration, migration, or hardening work.

**Stack:** EC2 · Ubuntu · SSH · Linux administration<br>
**Assessed:** Identity, operating system, kernel, storage, memory, uptime, packages, filesystem, configuration, and logs

<details>
<summary><strong>View assessment flow</strong></summary>

```mermaid
flowchart TB
    Admin([Administrator]) -->|SSH with key| EC2[Ubuntu Server on EC2]
    EC2 --> Identity[User, hostname & OS]
    EC2 --> Resources[Disk, memory & uptime]
    EC2 --> System[Kernel, architecture & packages]
    EC2 --> Files[Filesystem & configuration]
    EC2 --> Logs[System log review]
    Identity --> Report[Baseline Summary]
    Resources --> Report
    System --> Report
    Files --> Report
    Logs --> Report
```

</details>

## Technical skills

| Area | Services and tools |
|---|---|
| Cloud architecture | AWS Well-Architected principles, high availability, scalability, fault isolation |
| Compute | Amazon EC2, Auto Scaling, Linux, Nginx |
| Networking | Amazon VPC, subnets, routing, Security Groups, Application Load Balancer |
| Storage and data | Amazon S3, Amazon RDS, Amazon EBS |
| Security | IAM, least privilege, network separation, key-based SSH access |
| Operations | Health checks, server baselining, logs, monitoring fundamentals |

## Current work

- Building AWS architectures across the Solutions Architect Associate domains
- Turning architecture designs into repeatable Infrastructure as Code
- Adding monitoring, backup, recovery, and cost estimates to existing projects
- Improving technical documentation and architecture decision records

## Contact

I'm open to cloud engineering opportunities, AWS projects, and conversations with other people working in cloud.

[Portfolio website](https://agu-nwa.github.io/Agu-nwa/) · [GitHub projects](https://github.com/Agu-nwa?tab=repositories)
