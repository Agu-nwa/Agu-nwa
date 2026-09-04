<div align="center">

# Charles Chukwunonso

### AWS Cloud Engineer · Solutions Architecture · Linux

I design and build secure, reliable, and cost-aware systems on AWS.

[![Portfolio](https://img.shields.io/badge/Portfolio-View%20Website-FF9900?style=flat-square&logo=amazonwebservices&logoColor=white)](https://agu-nwa.github.io/Agu-nwa/)
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
flowchart LR
    Users([Internet users])

    subgraph AWS["AWS Cloud"]
        direction LR
        CF[CloudFront]
        S3[(Private S3 bucket)]

        subgraph VPC["VPC · 10.0.0.0/16"]
            direction TB
            ALB[Application Load Balancer]
            TG[Target group]

            subgraph ASG["Auto Scaling group · 2–4 instances"]
                direction LR
                subgraph AZA["Availability Zone A"]
                    EC2A[EC2 · Nginx]
                end
                subgraph AZB["Availability Zone B"]
                    EC2B[EC2 · Nginx]
                end
            end

            Endpoint[RDS endpoint]
            Primary[(PostgreSQL primary)]
            Standby[(PostgreSQL standby)]
        end
    end

    Users -->|Dynamic traffic| ALB
    ALB -->|Health-checked requests| TG
    TG --> EC2A & EC2B
    EC2A & EC2B --> Endpoint
    Endpoint --> Primary
    Primary -. Synchronous replication .-> Standby

    Users -->|Static content| CF
    CF -->|Origin access| S3

    classDef external fill:#f8fafc,stroke:#2563eb,color:#0b1f33,stroke-width:2px;
    classDef aws fill:#102a43,stroke:#ff9900,color:#f8fafc,stroke-width:2px;
    classDef compute fill:#163a59,stroke:#7dd3fc,color:#f8fafc;
    classDef data fill:#0b1f33,stroke:#7dd3fc,color:#f8fafc;
    class Users external;
    class ALB,TG,CF,S3 aws;
    class EC2A,EC2B compute;
    class Endpoint,Primary,Standby data;
    style AWS fill:#0b1f33,stroke:#29445d,color:#f8fafc
    style VPC fill:#102a43,stroke:#7dd3fc,color:#f8fafc
    style ASG fill:#0b1f33,stroke:#2563eb,color:#f8fafc
    style AZA fill:#102a43,stroke:#29445d,color:#f8fafc
    style AZB fill:#102a43,stroke:#29445d,color:#f8fafc
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
    Visitor([Website visitor]) -->|HTTP · port 80| WebRule[HTTP rule]
    Admin([Administrator]) -->|SSH · port 22| SSHRule[Restricted SSH rule]

    subgraph AWS["AWS Cloud"]
        subgraph SG["Security group"]
            WebRule
            SSHRule
        end
        subgraph EC2["Ubuntu EC2 instance"]
            Nginx[Nginx service]
            Content[Deployed web content]
            Nginx --> Content
        end
    end

    WebRule --> Nginx
    SSHRule -->|Key-based access| EC2
    Content -->|HTTP response| Visitor

    classDef external fill:#f8fafc,stroke:#2563eb,color:#0b1f33,stroke-width:2px;
    classDef control fill:#102a43,stroke:#7dd3fc,color:#f8fafc;
    classDef aws fill:#163a59,stroke:#ff9900,color:#f8fafc;
    class Visitor,Admin external;
    class WebRule,SSHRule control;
    class Nginx,Content aws;
    style AWS fill:#0b1f33,stroke:#29445d,color:#f8fafc
    style SG fill:#102a43,stroke:#7dd3fc,color:#f8fafc
    style EC2 fill:#102a43,stroke:#ff9900,color:#f8fafc
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
flowchart LR
    Admin([Administrator]) -->|Key-based SSH| Server[Ubuntu server on EC2]

    Server --> Discover

    subgraph Discover["Read-only discovery"]
        direction TB
        Identity[Identity · hostname · OS]
        Capacity[CPU · memory · disk · uptime]
        Software[Kernel · architecture · packages]
        Runtime[Processes · services · network]
        Evidence[Filesystem · configuration · logs]
    end

    Identity & Capacity & Software & Runtime & Evidence --> Baseline[Baseline report]
    Baseline --> Next[Prioritized next actions]

    classDef external fill:#f8fafc,stroke:#2563eb,color:#0b1f33,stroke-width:2px;
    classDef system fill:#102a43,stroke:#ff9900,color:#f8fafc,stroke-width:2px;
    classDef inspect fill:#163a59,stroke:#7dd3fc,color:#f8fafc;
    classDef output fill:#2563eb,stroke:#7dd3fc,color:#f8fafc,stroke-width:2px;
    class Admin external;
    class Server system;
    class Identity,Capacity,Software,Runtime,Evidence inspect;
    class Baseline,Next output;
    style Discover fill:#0b1f33,stroke:#29445d,color:#f8fafc
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
