# Azure SRE Agent Demo

## Overview

This project demonstrates how Azure SRE, Observability, DevOps, and AI-powered Operations can work together to detect, investigate, and remediate production incidents.

The solution combines GitHub, Azure Static Web Apps, Application Insights, Azure Monitor, Grafana Cloud, and Azure SRE Agent into a single end-to-end workflow.

---

## Architecture

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
GitHub Actions CI/CD
    │
    ▼
Azure Static Web App
    │
    ▼
Application Insights
    │
    ▼
Azure Monitor
    │
    ▼
Grafana Cloud
    │
    ▼
Azure SRE Agent
```

---

## Components

### GitHub

Source control and deployment automation.

Responsibilities:

* Source code management
* Pull Requests
* CI/CD pipeline execution
* Deployment history tracking

Repository:

https://github.com/manishjha2088/sre-agent-demo

---

### GitHub Actions

Automates deployment of the application to Azure Static Web Apps.

Responsibilities:

* Continuous Integration
* Continuous Deployment
* Deployment validation
* Deployment traceability

---

### Azure Static Web Apps

Hosts the application.

Responsibilities:

* Global content delivery
* Secure static hosting
* Automatic deployments
* Preview environments

Application URL:

https://proud-desert-0b553eb0f.7.azurestaticapps.net

---

### Application Insights

Provides application telemetry.

Collected Data:

* Page Views
* Custom Events
* Exceptions
* Traces
* User Activity

---

### Azure Monitor

Provides alerting and operational monitoring.

Alert Examples:

* Availability below 99%
* Increased exception count
* Failed deployments
* Application degradation

---

### Grafana Cloud

Provides centralized observability dashboards.

Metrics:

* Availability
* Error Rate
* Deployment Events
* Application Health
* User Activity

---

### Azure SRE Agent

Performs AI-assisted incident investigation.

Capabilities:

* Alert Analysis
* Telemetry Correlation
* Root Cause Analysis
* Remediation Recommendations
* Incident Summaries
* Executive Reporting

---

## Demo Scenario

### Normal Operation

1. User accesses application.
2. Application loads successfully.
3. Application Insights collects telemetry.
4. Azure Monitor records healthy status.
5. Grafana dashboards show normal behavior.

---

### Failure Scenario

1. Developer deploys faulty code.
2. GitHub Actions deploys application.
3. Application begins generating exceptions.
4. Application Insights records failures.
5. Azure Monitor alert triggers.
6. Azure SRE Agent investigates incident.
7. Agent correlates deployment with failure.
8. Agent identifies root cause.
9. Agent recommends rollback.
10. Service is restored.

---

## Root Cause Analysis Example

Incident Summary:

A deployment introduced application errors immediately after release.

Evidence:

* Deployment event detected
* Exception spike detected
* User impact observed
* Error rate increased significantly

Root Cause:

Application code introduced a deployment defect.

Recommended Action:

Rollback deployment and perform validation testing.

Preventive Action:

Introduce automated deployment validation and canary testing.

---

## Business Value

### Reduced MTTR

AI-assisted investigation reduces time required to identify root causes.

### Improved Reliability

Continuous monitoring enables proactive issue detection.

### Increased Visibility

Centralized observability across Azure and Grafana.

### Operational Efficiency

Reduces manual troubleshooting effort.

---

## Technologies Used

* Azure Static Web Apps
* Azure Monitor
* Application Insights
* Azure SRE Agent
* Grafana Cloud
* GitHub
* GitHub Actions
* JavaScript
* HTML
* CSS

---

## Future Enhancements

* Azure OpenAI Integration
* Automated Remediation Workflows
* Service Health Dashboards
* Synthetic Availability Testing
* Multi-Service Correlation
* Cost Optimization Analysis
* FinOps Integration
* Chaos Engineering Scenarios

---
## Build Guide

This section documents the complete setup process used to build the Azure SRE Agent demonstration environment.

---

## Step 1 - Create GitHub Repository

Create a new repository:

```bash
sre-agent-demo
```

Clone locally:

```bash
git clone https://github.com/manishjha2088/sre-agent-demo.git

cd sre-agent-demo
```

---

## Step 2 - Create Project Structure

```bash
mkdir -p .github/workflows
mkdir -p src
```

Project layout:

```text
sre-agent-demo
│
├── .github
│   └── workflows
│
├── src
│   ├── index.html
│   ├── app.js
│   └── styles.css
│
└── README.md
```

---

## Step 3 - Configure Git

```bash
git config --global user.name "Manish Jha"
git config --global user.email "<github-email>"
```

---

## Step 4 - Deploy GitHub Pages

Create workflow:

```yaml
.github/workflows/deploy.yml
```

Configure GitHub Pages:

Settings → Pages → Source → GitHub Actions

Push code:

```bash
git add .

git commit -m "Initial SRE Agent Demo"

git push origin main
```

---

## Step 5 - Create Azure Static Web App

Install extension:

```bash
az extension add --name staticwebapp
```

Create resource:

```bash
az staticwebapp create \
  --name swa-sre-demo \
  --resource-group rg-srelab \
  --source https://github.com/manishjha2088/sre-agent-demo \
  --branch main \
  --location eastus2 \
  --login-with-github
```

Result:

```text
https://proud-desert-0b553eb0f.7.azurestaticapps.net
```

---

## Step 6 - Configure Azure Static Web App Workflow

Update:

```yaml
app_location: "src"
api_location: ""
output_location: ""
```

Commit:

```bash
git add .

git commit -m "Fix Azure Static Web App source path"

git push origin main
```

---

## Step 7 - Verify Deployment

Open:

```text
https://proud-desert-0b553eb0f.7.azurestaticapps.net
```

Verify application loads successfully.

---

## Step 8 - Create Application Insights

Existing resource used:

```text
Resource Group: rg-srelab
Application Insights: appi-zsefd2mxtlfy4
```

Verify:

```bash
az monitor app-insights component show \
  --app appi-zsefd2mxtlfy4 \
  --resource-group rg-srelab
```

---

## Step 9 - Integrate Application Insights

Retrieve connection string:

```bash
az monitor app-insights component show \
  --app appi-zsefd2mxtlfy4 \
  --resource-group rg-srelab \
  --query connectionString \
  -o tsv
```

Add SDK to:

```text
src/index.html
```

Track:

* Page Views
* Events
* Exceptions
* Deployment Activity

---

## Step 10 - Validate Telemetry

Query telemetry:

```bash
az monitor app-insights query \
  --app appi-zsefd2mxtlfy4 \
  --resource-group rg-srelab \
  --analytics-query "pageViews | order by timestamp desc | take 10"
```

Query custom events:

```bash
az monitor app-insights query \
  --app appi-zsefd2mxtlfy4 \
  --resource-group rg-srelab \
  --analytics-query "customEvents | order by timestamp desc | take 10"
```

---

## Step 11 - Build Incident Scenario

Create branch:

```bash
git checkout -b incident-demo
```

Introduce application failure.

Commit:

```bash
git add .

git commit -m "Introduce deployment failure"

git push origin incident-demo
```

---

## Step 12 - Azure SRE Agent Investigation

Investigation workflow:

1. Detect alert
2. Review deployment history
3. Correlate telemetry
4. Identify root cause
5. Recommend remediation
6. Generate RCA

---

## Step 13 - Demonstrate Rollback

Rollback deployment:

```bash
git revert <commit-id>

git push origin main
```

Validate recovery using:

* Azure Monitor
* Application Insights
* Grafana Cloud
* Azure SRE Agent

---

## Outcome

This demonstration shows a complete DevOps and SRE workflow:

Developer Commit
→ GitHub Actions
→ Azure Static Web App
→ Application Insights
→ Azure Monitor
→ Grafana Cloud
→ Azure SRE Agent
→ Root Cause Analysis
→ Remediation Recommendation

## Author

Manish Jha


