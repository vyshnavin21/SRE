# Site Reliability Engineering (SRE) — Learning Notes

Personal notes on SRE fundamentals, concepts, and how the role fits alongside DevOps and traditional operations.

---

## What is SRE?

**Site Reliability Engineering (SRE)** focuses on building highly scalable and reliable software systems. It is a combination of **software engineering** work and **IT operations** work.

| Role | Primary Focus |
|---|---|
| **Software Engineer** | Code development, automation (reducing manual work) |
| **IT Operations / Systems Engineer** | Infrastructure design, maintaining servers/instances, availability |
| **SRE Engineer** | Automates operations, improves reliability, ensures systems stay available |

In simple terms:
- Developers **build** applications.
- Operations teams **deploy and maintain** them.
- SRE engineers **automate operations, improve reliability, and ensure availability**.

**Goal:** Reduce manual work and prevent outages.

---

## DevOps vs SRE

### DevOps Engineer Workflow
```
Developers push code → GitHub (code repository)
        ↓
   Jenkins (CI/CD)
        ↓
     Docker (containerization)
        ↓
   Kubernetes (orchestration)
```

### SRE Engineer's Core Responsibilities
- **Automation** — reducing toil
- **Monitoring** — configuring alerts and dashboards
- **Incident Management** — responding to and resolving outages
- **Error Budgets** — balancing reliability with feature velocity
- Managing deployments and releases
- Capacity planning and scaling
- Disaster recovery and backups

---

## Operating Systems Commonly Used
- **Linux**: Ubuntu, RedHat, CentOS
- **Windows**

---

## Automation & Toil

**Toil** = manual, repetitive operational work that doesn't add lasting value.

SRE uses automation to reduce toil and build systems that are more scalable and reliable (reducing downtime through automation).

### Example: Automating a Service Restart

**Scenario:**
You have a Linux server. An application runs on top of it. Using a monitoring tool, you notice the service goes down at the same time every day.

**Manual (non-scalable) approach:**
1. Log in to the server
2. Check if the service is up or down
3. Restart the service or check the logs

Doing this every day manually is a waste of time — this is **toil**.

**Automated (SRE) approach:**
Write a shell script that:
```
Go to the system
   → Check if the service is up or down
       → If down, restart the service automatically
```

This is a simple example of how SRE uses **scripting/automation** to eliminate toil.

---

## Monitoring

Monitoring means configuring alerts based on key metrics, for example:
- Disk space usage crossing a threshold
- CPU/memory utilization spikes
- Service downtime or failed health checks

---

## Incident Management

Incident management covers:
- How you **handle** an incident
- Which **teams** you involve
- How you **reduce downtime**
- Coordinating with other teams that own specific services (e.g., a partner team managing a particular microservice)

---

## Error Budgets

An **error budget** is the acceptable amount of downtime or failure allowed within a given period (commonly one month), based on the agreed SLA/SLO.

**Example:**
- If the SLA is 99.9% uptime, the error budget is the remaining 0.1% — no one can provide 100% uptime.
- Suppose an "Amazon" application has multiple teams. A "Samsung" team manages a specific microservice. Both teams agree on an **SLA of 99.99% availability** for that microservice over a one-month period. This means a small, agreed-upon amount of downtime is acceptable.

Error budgets help teams decide whether to focus on **new feature releases** or **reliability improvements** — if the budget is being exhausted, releases may need to slow down.

---

## Key SRE Concepts: SLA, SLO, SLI

| Term | Meaning | Example |
|---|---|---|
| **SLA** (Service Level Agreement) | The commitment made to customers. Failing to meet it may result in penalties or service credits. | 99.9% uptime promised to customers |
| **SLO** (Service Level Objective) | The internal target value set for a metric. | 99.95% internal uptime target |
| **SLI** (Service Level Indicator) | The actual measured value of that metric (availability, latency, error rate, success rate), gathered from monitoring tools/logs. | Measured uptime = 99.96% |

**Putting it together:**
- **SLA** = 99.9% uptime *promised* to customers
- **SLO** = 99.95% *internal target*
- **SLI** = 99.96% *actual measured* uptime

---

## Summary: What an SRE Does

- Monitors application and infrastructure health
- Handles incident response and troubleshooting
- Automates repetitive operational tasks (reduces toil)
- Manages deployments and releases
- Improves system reliability and performance
- Performs capacity planning and scaling
- Plans for disaster recovery and backups
- Coordinates with other teams on error budgets and SLAs

---

*Notes compiled for personal learning and reference.*
