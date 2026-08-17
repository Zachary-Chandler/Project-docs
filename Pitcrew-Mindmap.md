# Project Pitcrew — Internship Mind Map

## Overview

**Project:** Project Pitcrew  
**Role:** Site Reliability Engineering (SRE) Intern  
**Organization:** Toyota Financial Services (TFS) — Plano, TX  
**Internship:** May 18, 2026 – August 2026  
**Focus:** Automated remediation of web services and infrastructure

Project Pitcrew was an automation platform focused on moving from manually responding to service failures toward an automated detection, remediation, and verification workflow.

---

## Core Goal

The overall project direction was:

```text
Detect Problem
      ↓
Identify / Classify Failure
      ↓
Determine Severity
      ↓
Select Remediation
      ↓
Execute Remediation
      ↓
Verify Recovery
      ↓
Record / Escalate When Needed
```

The work involved connecting monitoring and service information to automated remediation logic while testing how the system behaved under different failure conditions.

---

# Major Technologies

- Python
- AWS
- Docker
- Minikube / Ministack
- Kubernetes
- Dynatrace
- ServiceNow
- React
- Git / GitHub
- Jira
- Visual Studio Code

---

# Project Areas

## 1. Alert & Incident Flow

Worked with the flow from an observed service problem toward an actionable incident.

Key concepts included:

- Alert discovery
- Service identification
- Failure classification
- Severity handling
- ServiceNow incidents
- Work notes
- Webhooks
- Automated remediation
- Recovery verification

---

## 2. ServiceNow Integration

Early work included building and debugging ServiceNow integration.

### Important progression

- Created a basic self-hosted Flask service calling the Dynatrace API.
- Added affected-entity output.
- Added `servicenow_client.py`.
- Worked through the ServiceNow API structure.
- Added alert-handler behavior for SNOW incidents and work notes.
- Stabilized the integration after multiple API and JSON-format issues.

### Trial / Error

The ServiceNow API required multiple attempts to get the request and work-note formats correct.

**Lesson:** API integrations need careful validation of request structure, payload format, and failure behavior.

---

# 3. Dynatrace Integration

Dynatrace was used as a source of service and monitoring information.

Work included:

- Calling Dynatrace APIs.
- Discovering affected entities.
- Mapping service information.
- Working with alert information.
- Building a Dynatrace mapper.
- Connecting monitoring information to remediation logic.

---

# 4. Testing & Dynatrace Mapper

A major project phase focused on testing the system and improving the Dynatrace mapping process.

Testing included:

- Simulated service failures.
- Container-based testing.
- Resource-condition testing.
- Failure cleanup.
- Remediation validation.
- Testing severity and rule behavior.
- Verifying that the system responded correctly to different failure conditions.

---

# 5. AWS / Minikube / Container Work

The project included local simulation of AWS-related infrastructure using Minikube / Ministack.

Work shown in the project timeline included:

- AWS CPU and memory simulation.
- AWS disk simulation.
- EC2 / ECS-related testing.
- Docker container testing.
- Container resource conditions.
- Kubernetes pods and namespaces.
- Dashboard simulation.
- Testing AWS resource rules.

### Example Problems Investigated

- Dockerfile syntax problems.
- Python package/import problems.
- Missing `__init__.py` files.
- Container resource conditions.
- Incorrect AWS target types.
- Kubernetes namespace behavior.
- Service availability and dependency problems.

---

# 6. Severity & Rule Logic

The project included logic for determining how serious an event was and what response should occur.

The severity system was designed around conditions such as:

- Informational events
- Warning conditions
- More serious service failures
- Critical failures

Rules were tested to ensure that severity affected the correct response rather than causing every event to receive the same treatment.

---

# 7. Automated Remediation

The central direction of Project Pitcrew was automated remediation.

The intended pipeline was:

```text
Dynatrace
   ↓
Rule Engine
   ↓
Executor
   ↓
Remediation
   ↓
ServiceNow
```

The project also included verification after remediation so that the system could determine whether the service actually recovered.

---

# 8. Testing Failures on Purpose

A significant part of the work involved intentionally creating failure conditions to see how the automation responded.

Examples included:

- Service failures
- Container failures
- CPU / memory pressure
- Disk-related conditions
- Configuration problems
- API failures
- Dependency problems
- Invalid or incomplete inputs

This helped identify weaknesses in the remediation process before relying on it for real operational scenarios.

---

# Complete Commit Timeline & Trials

## Phase 1 — Foundation

Early commits focused on getting the basic platform and integrations working.

### Major work

- Basic self-hosted Flask server calling Dynatrace API.
- Affected-entity output.
- Dependency updates.
- Repository cleanup.
- Initial ServiceNow integration.
- Git merge workflow.
- Alert-handler integration.
- Stabilization after ServiceNow integration problems.

### Key Lesson

Start with a working foundation and validate each external integration before building additional automation on top of it.

---

## Phase 2 — Testing & Dynatrace Mapper

The next phase focused on testing the system and mapping monitoring information into usable remediation data.

Areas included:

- Dynatrace entity mapping.
- Failure simulation.
- Container testing.
- Resource testing.
- Alert classification.
- Remediation validation.

---

## Phase 3 — AWS / Infrastructure Simulation

Work expanded into AWS-style infrastructure testing.

Examples:

- CPU simulation.
- Memory simulation.
- Disk simulation.
- AWS target handling.
- Containerized simulation.
- Dashboard testing.

---

## Phase 4 — Rule Engine / Severity

Work moved toward making the remediation system more intelligent.

The system needed to determine:

1. What happened?
2. Which service was affected?
3. How severe was the issue?
4. Should automation run?
5. Which remediation should be selected?
6. Did remediation succeed?

---

## Phase 5 — AWS / EC2 / ECS Work

The project included testing AWS-related resource behavior and simulation files.

Work included:

- Minikube / Ministack simulation.
- EC2 / ECS-related configuration.
- AWS CPU and memory simulation.
- AWS disk simulation.
- Dashboard dropdown / target selection.
- Error handling improvements.
- Docker and Python import fixes.

---

## Phase 6 — AWS CPU / Memory & DevTab Redesign

Work included developing CPU classification logic and configurable thresholds.

The design included:

- CPU classification.
- Graduated responses.
- Configurable thresholds.
- DevTab redesign.
- Severity settings.
- Testing of CPU and memory behavior.
- Dynatrace stub / simulated alert pipeline.

---

## Phase 7 — Merge Conflicts & Refactors

Later development involved combining changes and restructuring parts of the project.

Work included:

- Resolving merge conflicts.
- Refactoring Flask blueprints.
- Pulling refactored code into testing branches.
- Correcting imports after restructuring.
- Reviewing AWS disk rules.
- Fixing overly aggressive rule behavior.

### Key Lesson

Refactoring can improve architecture but can also introduce widespread breakage, so changes need to be tested after major structural modifications.

---

# Challenges & How They Were Solved

| Challenge | What Went Wrong | Fix / Approach | Lesson |
|---|---|---|---|
| ServiceNow hit production | Error occurred during startup | Load the required dependency / initialization correctly | Load required dependencies early |
| Missing `__init__.py` | Python could not find the package | Added the missing package file | Python package structure matters |
| Dockerfile spacing | `stress-ng` installation failed | Corrected Dockerfile syntax | Docker syntax must be validated |
| AWS local target type | Executor behavior did not match the intended target | Reverted to the existing AWS target type | Keep interfaces consistent |
| EC2 / ECS rule matching | Condition format was incorrect | Corrected event type / severity format | Test rules with unit tests |
| Namespace behavior | Kubernetes pods were being queried from the wrong namespace | Separated simulation namespace behavior | Namespace isolation matters |
| Service dependencies | A service could fail because another dependency was unavailable | Added dependency-aware handling | Remediation must consider dependencies |
| Merge conflicts | Refactoring caused widespread import / structure issues | Reworked imports and merged changes carefully | Refactors require regression testing |

---

# Weekly Progress Highlights

## Week 5 — AWS / EC2 / ECS

- Added Minikube / Ministack simulation files.
- Worked with EC2 / ECS simulation.
- Tested AWS CPU and memory behavior.
- Added AWS disk simulation.
- Improved error handling.
- Fixed Dockerfile and import-path issues.
- Worked on AWS target selection and dashboard behavior.

## Week 6 — AWS CPU Logic + DevTab Redesign

- Designed CPU classification logic.
- Added configurable thresholds.
- Created graduated responses.
- Wrote additional test cases.
- Worked on DevTab layout and severity settings.
- Added simulated alert behavior.
- Resolved DevTab merge conflicts.

## Week 7 — Rule Wizard + GitOps

- Continued work on the rule-building workflow.
- Worked with remediation-rule configuration.
- Continued integration and testing.
- Improved the connection between configuration and automated remediation.

---

# Completed Before Handoff

The project documentation showed several major areas completed before handoff.

### Completed / Demonstrated

- Full auto-remediation pipeline:

```text
Dynatrace → Rule Engine → Executor → ServiceNow
```

- Multiple alert / resource categories.
- Automated rule and remediation behavior.
- Testing using simulated failures.
- AWS / container simulation.
- Dashboard and DevTab work.
- Rule and severity configuration.
- ServiceNow ticket / work-note integration.

---

# Planned / Remaining Work

The project documentation also identified future work areas, including:

1. Public AWS Application Load Balancer access for EKS.
2. CI/CD pipeline using GitHub Actions → ECR → EKS.
3. Terraform-based AWS resource management.
4. Full integration testing on EKS.
5. Dynatrace alert rules connected directly to the Pitcrew webhook.
6. ServiceNow tickets for selected service warnings.
7. Threshold configuration through the Dev UI.
8. Internationalization / UI label translation.

---

# Key Technical Takeaways

## Automation

The internship focused on replacing repetitive manual operational work with automated detection and remediation.

## Systems Thinking

Problems often crossed multiple layers:

```text
Monitoring
   ↓
API
   ↓
Application
   ↓
Container
   ↓
Infrastructure
   ↓
Remediation
```

Understanding how these layers interacted was essential for diagnosing failures.

## Debugging

A large part of the work involved identifying why an automated workflow failed, correcting the underlying problem, and then testing the fix.

## Testing

Rather than only testing successful behavior, the project intentionally simulated failures to determine whether the system could recover correctly.

## Reliability

The goal was not simply to restart a service. The automation needed to determine the problem, select an appropriate response, execute it safely, and verify the result.

---

# Resume-Relevant Summary

**Site Reliability Engineering Intern at Toyota Financial Services, contributing to Project Pitcrew, an automated remediation platform for web services. Developed and tested Python-based remediation workflows using AWS, Docker, Minikube/Kubernetes, Dynatrace, and ServiceNow. Troubleshot API, container, infrastructure, configuration, and resource-related failures while developing automated detection, severity classification, remediation, and recovery-validation workflows.**

---

# Skills Demonstrated

- Python
- Site Reliability Engineering
- Cloud Infrastructure
- AWS
- Docker
- Kubernetes / Minikube
- Dynatrace
- ServiceNow
- API Integration
- Automation
- Incident Response
- Troubleshooting
- Testing
- Git / GitHub
- Agile Development
- Jira
- Systems Thinking
