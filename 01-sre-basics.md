# Site Reliability Engineering (SRE) — Learning Notes

Personal notes on SRE fundamentals, concepts, and incident management — for later revision.

---

## 1. What is SRE?

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

**SRE's main purpose:** Providing reliability and ensuring customer satisfaction.

---

## 2. DevOps vs SRE

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

## 3. Operating Systems Commonly Used
- **Linux**: Ubuntu, RedHat, CentOS
- **Windows**

---

## 4. Automation & Toil

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

## 5. Monitoring

Monitoring means configuring alerts based on key metrics, for example:
- Disk space usage crossing a threshold
- CPU/memory utilization spikes
- Service downtime or failed health checks

**As an SRE, the first thing to do is monitor the application.** If there's no alerting system in place, configure one. When an issue occurs, learn from it and make sure it never repeats — either by collaborating with other teams or getting to the root cause and using automation to reduce future downtime.

---

## 6. Incident Management

Incident management covers:
- How you **handle** an incident
- Which **teams** you involve
- How you **reduce downtime**
- Coordinating with other teams that own specific services (e.g., a partner team managing a particular microservice)

### Activities in Successful Incident Management

```
Detect incident → Log incident → Classify incident → Diagnose incident
        → Resolve incident → Close incident → Review incident
```

### 6.1 Incident Detection / Reporting
- **Monitoring Systems**: Continuous monitoring of systems, applications, and infrastructure to detect abnormalities, anomalies, or deviations from expected behavior.
- **Alerting**: Configuring mechanisms to notify the right personnel/teams when predefined thresholds or conditions are breached.
- **User Reports**: Customers may report incidents via customer support, feedback forms, or service status pages.
- **Internal Reports**: Team members and automated systems may generate incident reports based on observed issues.

### 6.2 Incident Triage
- **Prioritization**: Evaluate the severity and impact of the incident to prioritize the response, based on potential impact on users and business operations.
- **Assignment**: Assign responsibilities to the appropriate individuals or teams based on expertise and availability.

### 6.3 Incident Response
- **Communication**: Establish channels to coordinate the response. Notify relevant stakeholders, including internal teams and, if necessary, customers.
- **Documentation**: Begin documenting the incident — initial observations, actions taken, and any relevant information for resolution.

### 6.4 Resolution
- **Mitigation**: Implement temporary fixes or workarounds to restore service functionality quickly.
- **Permanent Fixes**: Develop and deploy permanent solutions that address the root cause and prevent recurrence.

### 6.5 Communication and Reporting
- **Status Updates**: Provide regular updates to stakeholders throughout the incident lifecycle.
- **Closure**: Communicate resolution to internal teams and, if applicable, customers.

### 6.6 Post-Incident Review (PIR)
- **Learning Opportunity**: Analyze the incident response, identify areas for improvement, and learn from the experience.
- **Documentation**: Document lessons learned, update runbooks/documentation, and share insights with the broader team to improve future incident responses.

> Following a well-defined incident management process helps organizations minimize incident impact, improve system resilience, and enhance overall service reliability.

### Example Toolchain by Stage

| Stage | Example Tools |
|---|---|
| Incident Detection / Monitoring | New Relic, SolarWinds |
| Alerting | OpsGenie |
| User Reports | ServiceNow, Jira |
| Communication | Slack, OpsGenie |
| Documentation | Confluence |
| Permanent Fixes / Resolution | Jira, ServiceNow |

---

## 7. Error Budgets

An **error budget** is the acceptable amount of downtime or failure allowed within a given period (commonly one month), based on the agreed SLA/SLO.

**Example:**
- If the SLA is 99.9% uptime, the error budget is the remaining 0.1% — no one can provide 100% uptime.
- Suppose an "Amazon" application has multiple teams. A "Samsung" team manages a specific microservice. Both teams agree on an **SLA of 99.99% availability** for that microservice over a one-month period. This means a small, agreed-upon amount of downtime is acceptable.

Error budgets help teams decide whether to focus on **new feature releases** or **reliability improvements** — if the budget is being exhausted, releases may need to slow down.

---

## 8. Key SRE Concepts: SLA, SLO, SLI

| Term | Meaning | Example |
|---|---|---|
| **SLA** (Service Level Agreement) | The commitment made to customers. Failing to meet it may result in penalties or service credits. | 99.9% uptime promised to customers |
| **SLO** (Service Level Objective) | The internal target value set for a metric. | 99.95% internal uptime target, or 95% of requests under 200ms |
| **SLI** (Service Level Indicator) | The actual measured value of a metric (availability, latency, error rate, success rate), gathered from monitoring tools/logs. | Measured uptime = 99.96% |

**Putting it together:**
- **SLA** = 99.9% uptime *promised* to customers
- **SLO** = 99.95% *internal target*
- **SLI** = 99.96% *actual measured* uptime

---

## 9. Observability & Anti-Fragility

- **Observability**: Understanding system performance using logs and monitoring data.
- **Anti-fragility**: A system's ability to benefit from shocks or failures — becoming stronger and more reliable over time, rather than just surviving disruptions.

---

## 10. Summary: What an SRE Does

- Monitors application and infrastructure health
- Handles incident response and troubleshooting
- Automates repetitive operational tasks (reduces toil)
- Manages deployments and releases
- Improves system reliability and performance
- Performs capacity planning and scaling
- Plans for disaster recovery and backups
- Coordinates with other teams on error budgets and SLAs

---

*Notes compiled for personal learning and reference. Revisit and expand as more topics are covered.*
