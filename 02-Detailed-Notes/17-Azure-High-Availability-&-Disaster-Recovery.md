# High Availability & Disaster Recovery (HA & DR)

## Definition

- High Availability (HA) ensures applications remain available even if a component fails.
- Disaster Recovery (DR) restores applications and infrastructure after major failures such as regional outages or natural disasters.
- Azure provides built-in services to improve availability and minimize downtime.

---

## Why is it used?

- Minimize downtime.
- Increase application availability.
- Protect against hardware failures.
- Recover from regional disasters.
- Ensure business continuity.
- Meet Service Level Agreements (SLAs).

---

## Key Features

- Availability Sets.
- Availability Zones.
- Region Pairs.
- Load Balancing.
- Geo-Redundant Storage (GRS).
- Azure Site Recovery.
- Backup and Recovery.

---

## Advantages

- Improved application uptime.
- Reduced business interruption.
- Better customer experience.
- Supports disaster recovery planning.
- High reliability.

---

## Disadvantages

- Additional infrastructure costs.
- More complex architecture.
- Requires planning and testing.

---

## Components

- Availability Sets
- Availability Zones
- Region Pairs
- Azure Load Balancer
- Geo-Redundant Storage
- Azure Site Recovery

---

## Workflow

```text
Application
      ↓
High Availability Services
      ↓
Failure Detected
      ↓
Automatic Recovery / Failover
      ↓
Business Continues
```

---

## Real-world Example

An e-commerce company deploys its application across multiple Availability Zones with a Load Balancer. If one zone fails, customer traffic automatically shifts to healthy zones.

---

## Interview Tip

"High Availability minimizes downtime during hardware failures, while Disaster Recovery restores services after major disasters."

---

## Quick Revision

- HA minimizes downtime.
- DR restores services.
- Availability Sets protect against hardware failures.
- Availability Zones protect against datacenter failures.
- Region Pairs protect against regional failures.
- ASR provides disaster recovery.

---

## Important Interview Questions

1. What is the difference between High Availability and Disaster Recovery?
2. Which Azure services improve High Availability?
3. Why is Disaster Recovery important?
4. What is Business Continuity?
5. How does Azure improve application availability?

---

# Availability Sets

## Definition

- Availability Sets protect Azure Virtual Machines from hardware failures and planned maintenance.
- Azure distributes VMs across different **Fault Domains** and **Update Domains**.

---

## Why is it used?

- Improve VM availability.
- Protect against hardware failures.
- Reduce planned maintenance impact.
- Meet Azure VM SLA requirements.

---

## Key Features

- Fault Domains.
- Update Domains.
- Supports multiple VMs.
- Improves availability.

---

## Advantages

- Protects against hardware failures.
- Supports planned maintenance.
- Easy to configure.
- Improves uptime.

---

## Disadvantages

- Protects only within a single Azure datacenter.
- Does not protect against datacenter failures.

---

## Components

### Fault Domain (FD)

- Group of hardware sharing the same power and network.
- Protects against hardware failures.

### Update Domain (UD)

- Group of VMs updated together during maintenance.
- Prevents all VMs from rebooting simultaneously.

---

## Workflow

```text
Availability Set
      ↓
Fault Domains
      ↓
Update Domains
      ↓
Virtual Machines
```

---

## Real-world Example

Two application servers are placed in an Availability Set. During Azure maintenance, only one VM is restarted while the other remains available.

---

## Interview Tip

"Availability Sets protect Virtual Machines from hardware failures and planned maintenance within a datacenter."

---

## Quick Revision

- Uses Fault Domains.
- Uses Update Domains.
- Single datacenter.
- VM protection.
- Improves SLA.

---

## Important Interview Questions

1. What is an Availability Set?
2. What is a Fault Domain?
3. What is an Update Domain?
4. When should Availability Sets be used?
5. How do Availability Sets improve availability?

---

# Availability Zones

## Definition

- Availability Zones are physically separate datacenters within the same Azure region.
- Each zone has independent power, cooling, and networking.

---

## Why is it used?

- Protect against datacenter failures.
- Improve application availability.
- Support mission-critical workloads.
- Increase fault tolerance.

---

## Key Features

- Physically separate datacenters.
- Independent infrastructure.
- Low-latency connectivity.
- High availability.

---

## Advantages

- Protects against datacenter failures.
- High SLA.
- Automatic fault isolation.
- Suitable for production workloads.

---

## Disadvantages

- Available only in supported Azure regions.
- Cross-zone traffic may incur costs.

---

## Workflow

```text
Zone 1
    │
Zone 2
    │
Zone 3
      ↓
Application Remains Available
```

---

## Real-world Example

A banking application runs across three Availability Zones. If Zone 1 fails, Zones 2 and 3 continue serving customers.

---

## Interview Tip

"Availability Zones protect applications against complete datacenter failures."

---

## Quick Revision

- Multiple datacenters.
- Same Azure region.
- High availability.
- Independent infrastructure.
- Higher SLA.

---

## Important Interview Questions

1. What is an Availability Zone?
2. How is an Availability Zone different from an Availability Set?
3. Why are Availability Zones important?
4. How many Availability Zones are available in a region?
5. What failures do Availability Zones protect against?

---

# Region Pairs

## Definition

- Region Pairs are two Azure regions located within the same geography and paired by Microsoft for disaster recovery.
- If one region experiences a major outage, services can fail over to the paired region.

---

## Why is it used?

- Regional disaster recovery.
- Data replication.
- Improve business continuity.
- Planned Azure maintenance.

---

## Key Features

- Automatic pairing.
- Regional redundancy.
- Sequential updates.
- Disaster recovery support.

---

## Advantages

- Regional protection.
- Improved availability.
- Better disaster recovery.
- Compliance support.

---

## Disadvantages

- Replication may have slight delay.
- Secondary region increases costs.

---

## Workflow

```text
Primary Region
      ↓
Replication
      ↓
Paired Region
```

---

## Real-world Example

If East US becomes unavailable, workloads can be recovered in West US (its paired region).

---

## Interview Tip

"Region Pairs protect workloads against complete Azure regional failures."

---

## Quick Revision

- Two Azure regions.
- Disaster recovery.
- Replication.
- Sequential updates.
- Regional resilience.

---

## Important Interview Questions

1. What are Azure Region Pairs?
2. Why are Region Pairs important?
3. Do all Azure regions have a pair?
4. How do Region Pairs improve availability?
5. What is replicated between Region Pairs?

---

# Load Balancing

## Definition

- Load Balancing distributes incoming network traffic across multiple servers or Virtual Machines.
- It prevents any single server from becoming overloaded.

---

## Why is it used?

- Improve availability.
- Distribute workload.
- Prevent server overload.
- Increase scalability.
- Improve application performance.

---

## Key Features

- Health probes.
- Automatic traffic distribution.
- High availability.
- Public and Internal Load Balancers.

---

## Advantages

- Better performance.
- High availability.
- Improved scalability.
- Fault tolerance.

---

## Disadvantages

- Requires multiple backend servers.
- Incorrect health probes affect routing.

---

## Types

| Service | Layer | Purpose |
|----------|-------|---------|
| Azure Load Balancer | Layer 4 | TCP/UDP traffic |
| Azure Application Gateway | Layer 7 | HTTP/HTTPS traffic |

---

## Workflow

```text
Users
     ↓
Load Balancer
     ↓
Healthy Virtual Machines
```

---

## Real-world Example

Four web servers are placed behind an Azure Load Balancer to distribute customer requests evenly.

---

## Interview Tip

"Load Balancing distributes traffic across healthy servers to improve availability and performance."

---

## Quick Revision

- Traffic distribution.
- Health probes.
- Layer 4 and Layer 7.
- High availability.
- Scalability.

---

## Important Interview Questions

1. What is Load Balancing?
2. Why is Load Balancing important?
3. What are Health Probes?
4. Difference between Load Balancer and Application Gateway?
5. What layer does Azure Load Balancer operate on?

---

# Geo-Redundant Storage (GRS)

## Definition

- Geo-Redundant Storage (GRS) automatically replicates Azure Storage data to a secondary Azure region.
- It protects against regional outages and disasters.

---

## Why is it used?

- Protect against regional failures.
- Increase durability.
- Improve Disaster Recovery.
- Secure business data.

---

## Key Features

- Six copies of data.
- Replication to paired region.
- Automatic replication.
- High durability.

---

## Advantages

- Regional protection.
- High durability.
- Automatic replication.
- Business continuity.

---

## Disadvantages

- Higher storage cost.
- Replication delay may occur.

---

## Workflow

```text
Primary Storage
       ↓
Geo Replication
       ↓
Secondary Region
```

---

## Real-world Example

Customer files stored in East US are automatically replicated to West US using GRS.

---

## Interview Tip

"GRS protects Azure Storage data by replicating it to another Azure region."

---

## Quick Revision

- Six copies.
- Paired region.
- Automatic replication.
- Disaster protection.

---

## Important Interview Questions

1. What is Geo-Redundant Storage?
2. Why use GRS?
3. How many copies does GRS maintain?
4. What is the difference between LRS and GRS?
5. Does GRS improve Disaster Recovery?

---

# Azure Site Recovery (ASR)

## Definition

- Azure Site Recovery (ASR) is Azure's Disaster Recovery service that continuously replicates workloads to another Azure region or site.
- It enables automatic failover and failback during disasters.

---

## Why is it used?

- Protect applications.
- Minimize downtime.
- Disaster recovery.
- Replicate Virtual Machines.
- Business continuity.

---

## Key Features

- Continuous replication.
- Test Failover.
- Planned Failover.
- Automatic recovery.
- Failback.

---

## Advantages

- Minimal downtime.
- Business continuity.
- Automated Disaster Recovery.
- Supports Azure and on-premises.

---

## Disadvantages

- Replication storage cost.
- Requires DR planning.

---

## Workflow

```text
Primary Site
      ↓
Replication
      ↓
Secondary Azure Region
      ↓
Failover
```

---

## Real-world Example

A production Virtual Machine is replicated to another Azure region. During a regional outage, ASR starts the replicated VM automatically.

---

## Interview Tip

"Azure Site Recovery provides Disaster Recovery through continuous replication and failover."

---

## Quick Revision

- Disaster Recovery.
- Replication.
- Failover.
- Failback.
- Test Failover.

---

## Important Interview Questions

1. What is Azure Site Recovery?
2. What is Failover?
3. What is Failback?
4. What is Test Failover?
5. How does ASR reduce downtime?

---

# Business Continuity Planning (BCP)

## Definition

- Business Continuity Planning (BCP) is the process of ensuring critical business operations continue during and after unexpected disruptions.
- It combines High Availability, Backup, Disaster Recovery, monitoring, and recovery planning.

---

## Why is it used?

- Reduce business downtime.
- Protect customer services.
- Meet compliance requirements.
- Recover quickly from failures.
- Improve organizational resilience.

---

## Key Features

- Risk assessment.
- Backup strategy.
- Disaster Recovery planning.
- High Availability.
- Recovery testing.
- Incident response.

---

## Advantages

- Continuous business operations.
- Reduced financial loss.
- Better customer trust.
- Faster recovery.

---

## Disadvantages

- Requires planning and regular testing.
- Additional infrastructure costs.

---

## Components

### Backup

- Protects business data.

### High Availability

- Keeps applications online.

### Disaster Recovery

- Restores services after disasters.

### Monitoring

- Detects failures quickly.

### Recovery Testing

- Validates recovery procedures.

---

## Workflow

```text
Business Operations
        ↓
Unexpected Failure
        ↓
HA + Backup + DR Activated
        ↓
Business Continues
```

---

## Real-world Example

A financial company uses Availability Zones, Azure Backup, Azure Site Recovery, Geo-Redundant Storage, and Azure Monitor to ensure online banking remains available during disasters.

---

## Interview Tip

"Business Continuity Planning combines High Availability, Backup, and Disaster Recovery to keep business services running."

---

## Quick Revision

- Backup protects data.
- High Availability minimizes downtime.
- Disaster Recovery restores infrastructure.
- Geo-Replication protects regions.
- Continuous monitoring.
- Regular recovery testing.

---

## Important Interview Questions

1. What is Business Continuity Planning?
2. How is BCP different from Disaster Recovery?
3. Why should Disaster Recovery plans be tested?
4. Which Azure services support Business Continuity?
5. What is the relationship between High Availability, Backup, and Disaster Recovery?

---

# Availability Set vs Availability Zone vs Region Pair

| Feature | Availability Set | Availability Zone | Region Pair |
|---------|------------------|-------------------|-------------|
| Scope | Single Datacenter | Multiple Datacenters | Multiple Azure Regions |
| Protects Against | Hardware Failure & Planned Maintenance | Datacenter Failure | Regional Failure |
| Fault Domains | Yes | No | No |
| Update Domains | Yes | No | No |
| Geographic Separation | No | Yes (within same region) | Yes (different regions) |
| Best For | VM Availability | Mission-Critical Applications | Disaster Recovery |
| Typical Use | Multiple VMs in one datacenter | Highly Available Production Apps | Business Continuity & Regional DR |
