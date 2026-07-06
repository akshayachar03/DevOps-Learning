# Architecture Design in Azure

## Definition

- Architecture Design is the process of designing Azure solutions that are secure, scalable, highly available, cost-effective, and easy to manage.
- A well-designed architecture follows Azure Well-Architected Framework principles such as Reliability, Security, Performance Efficiency, Cost Optimization, and Operational Excellence.

---

## Why is it used?

- Build reliable cloud applications.
- Improve scalability.
- Increase security.
- Minimize downtime.
- Reduce operational costs.
- Support business growth.

---

## Key Features

- High Availability.
- Scalability.
- Fault Tolerance.
- Disaster Recovery.
- Security.
- Cost Optimization.
- Automation.

---

## Advantages

- Better performance.
- Improved reliability.
- Easier maintenance.
- Lower operational risk.
- Future-proof infrastructure.

---

## Disadvantages

- Requires proper planning.
- More complex architectures increase management effort.
- Highly available designs may increase costs.

---

## Components

- Compute
- Networking
- Storage
- Security
- Monitoring
- Identity
- Disaster Recovery

---

## Real-world Example

An online banking application is deployed across multiple Availability Zones with Azure Load Balancer, Azure SQL Database, Azure Firewall, and Azure Site Recovery to ensure continuous availability.

---

## Interview Tip

"A good Azure architecture should always be secure, scalable, highly available, and cost optimized."

---

## Quick Revision

- Reliability.
- Security.
- Scalability.
- High Availability.
- Disaster Recovery.
- Cost Optimization.

---

## Important Interview Questions

1. What is Azure Architecture Design?
2. What are the goals of a good cloud architecture?
3. What are the Azure Well-Architected Framework pillars?
4. Why is architecture planning important?
5. What makes an architecture highly available?

---

# Three-Tier Architecture

## Definition

- Three-Tier Architecture separates an application into three independent layers:
  - Presentation Layer
  - Application Layer
  - Database Layer
- Each layer performs a specific function and can be managed independently.

---

## Why is it used?

- Improve scalability.
- Simplify maintenance.
- Increase security.
- Separate application responsibilities.
- Support independent scaling.

---

## Key Features

- Layer separation.
- Independent scaling.
- Better security.
- Easier troubleshooting.
- Modular architecture.

---

## Advantages

- High maintainability.
- Better performance.
- Improved security.
- Easy upgrades.
- Flexible scaling.

---

## Disadvantages

- More infrastructure.
- Increased deployment complexity.

---

## Architecture

```text
Users
   │
Azure Application Gateway
   │
Web Tier (App Service / VM)
   │
Application Tier (API / AKS / VM)
   │
Database Tier (Azure SQL / Cosmos DB)
```

---

## Azure Services

| Layer | Azure Service |
|---------|--------------|
| Presentation | App Service, VM, Static Web Apps |
| Application | App Service, AKS, VM Scale Sets |
| Database | Azure SQL Database, PostgreSQL, Cosmos DB |

---

## Real-world Example

An e-commerce website uses App Service for the frontend, AKS for APIs, and Azure SQL Database for storing orders.

---

## Interview Tip

"Three-Tier Architecture separates presentation, business logic, and database layers for better scalability and maintainability."

---

## Quick Revision

- Three layers.
- Independent scaling.
- Better security.
- Easier maintenance.
- Modular.

---

## Important Interview Questions

1. What is Three-Tier Architecture?
2. What are the three layers?
3. Why is Three-Tier Architecture used?
4. Which Azure services fit each layer?
5. What are its advantages?

---

# Hub-and-Spoke Network

## Definition

- Hub-and-Spoke is a network topology where a central Hub VNet connects multiple Spoke VNets.
- Shared services are placed in the Hub, while applications reside in the Spokes.

---

## Why is it used?

- Centralize networking.
- Improve security.
- Simplify management.
- Reduce network complexity.
- Support large enterprises.

---

## Key Features

- Central Hub.
- Multiple Spokes.
- Shared services.
- VNet Peering.
- Centralized Firewall.

---

## Advantages

- Better security.
- Easier network management.
- Scalable.
- Shared infrastructure.

---

## Disadvantages

- Hub becomes critical.
- Requires proper network planning.

---

## Architecture

```text
              Hub VNet
      Firewall | VPN | DNS
        /        |        \
       /         |         \
Spoke VNet1  Spoke VNet2  Spoke VNet3
```

---

## Hub Components

- Azure Firewall
- VPN Gateway
- Bastion
- DNS
- Shared Services

---

## Real-world Example

An enterprise hosts Finance, HR, and Sales applications in separate Spoke VNets connected to a centralized Hub containing Azure Firewall and VPN Gateway.

---

## Interview Tip

"Hub-and-Spoke centralizes networking and security while isolating application workloads."

---

## Quick Revision

- Central Hub.
- Multiple Spokes.
- Shared Firewall.
- Shared VPN.
- Enterprise networking.

---

## Important Interview Questions

1. What is Hub-and-Spoke Architecture?
2. What services are placed in the Hub?
3. Why use Hub-and-Spoke?
4. What is VNet Peering?
5. How does Hub improve security?

---

# Azure Landing Zone

## Definition

- An Azure Landing Zone is a pre-configured Azure environment that follows Microsoft's best practices for governance, networking, identity, security, and resource organization.
- It provides a standardized foundation for deploying workloads.

---

## Why is it used?

- Standardize Azure environments.
- Accelerate cloud adoption.
- Improve governance.
- Enforce security.
- Simplify deployments.

---

## Key Features

- Management Groups.
- Policies.
- RBAC.
- Networking.
- Identity.
- Monitoring.
- Security.

---

## Advantages

- Standardized deployment.
- Secure foundation.
- Easy scalability.
- Enterprise ready.

---

## Disadvantages

- Initial setup requires planning.
- May be more than required for small organizations.

---

## Components

- Management Groups
- Subscriptions
- Resource Groups
- Azure Policy
- Networking
- Monitoring
- Security

---

## Workflow

```text
Landing Zone
      ↓
Governance
      ↓
Networking
      ↓
Identity
      ↓
Deploy Applications
```

---

## Real-world Example

A multinational company creates a Landing Zone before migrating 500 applications into Azure to ensure every workload follows company standards.

---

## Interview Tip

"A Landing Zone is a secure, governed, and standardized Azure environment prepared before deploying workloads."

---

## Quick Revision

- Standard environment.
- Governance.
- Networking.
- Security.
- Identity.
- Enterprise foundation.

---

## Important Interview Questions

1. What is an Azure Landing Zone?
2. Why is a Landing Zone important?
3. What services are included?
4. When should a Landing Zone be created?
5. How does it improve governance?

---

# Secure Architecture

## Definition

- Secure Architecture protects Azure resources using identity, networking, encryption, monitoring, and governance.
- It follows the **Zero Trust** security model.

---

## Why is it used?

- Protect applications.
- Secure data.
- Prevent unauthorized access.
- Meet compliance.
- Reduce security risks.

---

## Key Features

- Microsoft Entra ID.
- RBAC.
- Azure Firewall.
- NSGs.
- Key Vault.
- Microsoft Defender.
- Microsoft Sentinel.

---

## Advantages

- Strong security.
- Compliance.
- Better visibility.
- Reduced attack surface.

---

## Disadvantages

- More security controls increase complexity.
- Advanced security features may increase cost.

---

## Architecture

```text
Users
   │
Microsoft Entra ID
   │
Application Gateway + WAF
   │
Azure Firewall
   │
Application
   │
Azure Key Vault
   │
Database
```

---

## Real-world Example

An online banking system uses WAF, Azure Firewall, Key Vault, Defender for Cloud, and Microsoft Sentinel to secure customer data.

---

## Interview Tip

"A secure Azure architecture combines identity, network security, encryption, and monitoring."

---

## Quick Revision

- Zero Trust.
- RBAC.
- Firewall.
- Key Vault.
- Defender.
- Sentinel.

---

## Important Interview Questions

1. What is Secure Architecture?
2. What is Zero Trust?
3. Which Azure services improve security?
4. Why is Key Vault important?
5. What is the role of Azure Firewall?

---

# Highly Available Architecture

## Definition

- Highly Available Architecture ensures applications continue running despite hardware failures, maintenance, or datacenter outages.

---

## Why is it used?

- Reduce downtime.
- Improve reliability.
- Meet SLAs.
- Increase customer satisfaction.

---

## Key Features

- Availability Zones.
- Availability Sets.
- Load Balancer.
- Auto Scaling.
- Azure Backup.
- Azure Site Recovery.

---

## Advantages

- Better uptime.
- Improved reliability.
- Automatic recovery.
- Fault tolerance.

---

## Disadvantages

- Higher infrastructure costs.
- More complex deployment.

---

## Architecture

```text
Users
   │
Load Balancer
   │
VM Zone 1
VM Zone 2
VM Zone 3
   │
Azure SQL Database
```

---

## Real-world Example

A streaming platform runs web servers across three Availability Zones with Azure Load Balancer.

---

## Interview Tip

"High Availability ensures services continue running during failures without noticeable downtime."

---

## Quick Revision

- Availability Zones.
- Load Balancer.
- Fault tolerance.
- Auto Scaling.
- Site Recovery.

---

## Important Interview Questions

1. What is High Availability?
2. How do Availability Zones improve HA?
3. What is fault tolerance?
4. Which Azure services improve availability?
5. What is the role of a Load Balancer?

---

# Scalable Architecture

## Definition

- Scalable Architecture allows applications to handle increasing or decreasing workloads by automatically adding or removing resources.

---

## Why is it used?

- Handle traffic spikes.
- Improve performance.
- Reduce costs.
- Optimize resources.

---

## Key Features

- Horizontal Scaling.
- Vertical Scaling.
- Auto Scaling.
- Load Balancing.

---

## Advantages

- Better performance.
- Cost optimization.
- Automatic scaling.
- Improved customer experience.

---

## Disadvantages

- Scaling rules require proper configuration.
- Rapid scaling may increase costs.

---

## Types

| Type | Description |
|------|-------------|
| Vertical Scaling | Increase CPU/RAM of one server |
| Horizontal Scaling | Add more servers |

---

## Architecture

```text
Users
   │
Load Balancer
   │
VM1 VM2 VM3 VM4
```

---

## Real-world Example

An online ticket booking system automatically scales from 2 VMs to 20 VMs during festival bookings.

---

## Interview Tip

"Horizontal scaling is generally preferred in cloud environments because it improves availability and fault tolerance."

---

## Quick Revision

- Auto Scaling.
- Horizontal scaling.
- Vertical scaling.
- Load Balancer.
- Performance optimization.

---

## Important Interview Questions

1. What is Scalable Architecture?
2. Difference between Horizontal and Vertical Scaling?
3. What is Auto Scaling?
4. Why is horizontal scaling preferred?
5. Which Azure services support Auto Scaling?

---

# Multi-Region Architecture

## Definition

- Multi-Region Architecture deploys applications across two or more Azure regions.
- It provides protection against complete regional failures and improves global performance.

---

## Why is it used?

- Disaster Recovery.
- Reduce latency.
- Improve availability.
- Serve global users.
- Business continuity.

---

## Key Features

- Multiple Azure regions.
- Geo-replication.
- Traffic routing.
- Regional failover.
- Global availability.

---

## Advantages

- Regional disaster protection.
- Better user experience.
- High availability.
- Business continuity.

---

## Disadvantages

- Higher deployment cost.
- More complex management.
- Data synchronization challenges.

---

## Architecture

```text
              Azure Traffic Manager
                     │
        ┌────────────┴────────────┐
        │                         │
 East US Region             West Europe Region
        │                         │
 Application             Application
        │                         │
 Geo-Replicated Database
```

---

## Common Azure Services

- Azure Traffic Manager
- Azure Front Door
- Azure Site Recovery
- Geo-Redundant Storage (GRS)
- Azure SQL Geo-Replication

---

## Real-world Example

A multinational e-commerce company hosts applications in East US and West Europe. Users are automatically routed to the nearest healthy region using Azure Front Door.

---

## Interview Tip

"Multi-Region Architecture protects against regional failures and provides low-latency access for global users."

---

## Quick Revision

- Multiple regions.
- Disaster Recovery.
- Traffic Manager.
- Azure Front Door.
- Geo-Replication.
- Business continuity.

---

## Important Interview Questions

1. What is Multi-Region Architecture?
2. Why use multiple Azure regions?
3. Difference between Availability Zones and Multi-Region Architecture?
4. Which Azure services support Multi-Region deployments?
5. What is Geo-Replication?

---

# Architecture Comparison

| Architecture | Primary Purpose | Common Azure Services |
|--------------|-----------------|-----------------------|
| Three-Tier | Separate application layers | App Service, AKS, Azure SQL |
| Hub-and-Spoke | Centralized networking | VNet Peering, Azure Firewall, VPN Gateway |
| Landing Zone | Standardized Azure environment | Management Groups, Policy, RBAC |
| Secure Architecture | Protect applications and data | Key Vault, Firewall, Defender, Sentinel |
| Highly Available Architecture | Minimize downtime | Availability Zones, Load Balancer, ASR |
| Scalable Architecture | Handle changing workloads | VMSS, AKS, Auto Scale, Load Balancer |
| Multi-Region Architecture | Disaster recovery & global access | Front Door, Traffic Manager, GRS, ASR |
