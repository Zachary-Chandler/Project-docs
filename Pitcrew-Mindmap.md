# Project Pitcrew — Internship Mind Map

This repository contains my project mind map for **Project Pitcrew**, the work I completed during my Site Reliability Engineering internship at Toyota Financial Services.

The purpose of this document is to keep a detailed record of the project—not only the final results, but also the **work completed, successes, failures, experiments, debugging, testing, and lessons learned** throughout development.

---

# Project Overview

**Project:** Project Pitcrew  
**Role:** Site Reliability Engineering (SRE) Intern  
**Organization:** Toyota Financial Services (TFS)  
**Location:** Plano, TX  
**Internship:** May 18, 2026 – July 27, 2026  
**Primary Focus:** Automated remediation, service reliability, monitoring, infrastructure simulation, testing, and the migration of the project from Docker-based development toward Kubernetes/EKS.

## Core Goal

Project Pitcrew was built around an automated remediation pipeline:

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

The goal was to detect service/resource problems, determine the appropriate rule and severity, execute a remediation action, and provide visibility into what happened.

---

# Technologies & Tools

- Python
- Flask
- AWS
- Docker
- Kubernetes
- Minikube / MiniStack
- EKS
- Dynatrace
- ServiceNow
- Git / GitHub
- GitHub Actions
- Jira
- React
- Docker Compose
- Helm
- OTel / OpenTelemetry
- Visual Studio Code

---

# Complete Commit Timeline & Trials

## Phase 1: Foundation — Early Commits

The first phase established the basic application and began integrating external services.

### Work Completed

- Built a basic self-hosted Flask server calling the Dynatrace API.
- Added affected-entity output to the self-hosted dashboard.
- Updated `requirements.txt`.
- Cleaned up the repository structure.
- Added `servicenow_client.py`.
- Performed the first merge into `main`.
- Added an alert handler that could trigger ServiceNow incidents and work notes.
- Stabilized the ServiceNow integration.

### Trial & Error

The ServiceNow API required multiple attempts to get the integration working correctly. Work notes and their JSON format were particularly difficult.

### Lesson

External API integrations need to be tested carefully before building additional automation on top of them.

---

# Phase 2: Testing & Dynatrace Mapper

This phase focused on converting Dynatrace webhook information into the internal format used by the project.

### Work Completed

- Created `dynatrace_mapper.py`.
- Added test cases for the Dynatrace mapper.
- Improved the log parser using pattern matching.
- Moved away from fragile fixed-line offsets.
- Added comments to the code.
- Added data stretching to the dashboard data frame.

### Trial & Error

The project initially relied on fixed offsets when parsing information. Pattern matching proved to be more reliable.

### Lesson

**Pattern matching is better than fixed offsets**, and automated tests help prevent regressions.

---

# Phase 3: Memory Remediation

The project expanded from basic detection into resource remediation.

### Work Completed

- Added memory-fixing capabilities.
- Added memory removal, buildup, and a test container.
- Integrated memory functionality into the rule engine.
- Fixed errors created by file-directory changes.
- Added complex memory tests using random file remediation.
- Tested that cleanup was surgical rather than destructive.

### Trial & Error

File-directory reorganization broke imports. This became a recurring problem as the project structure evolved.

Memory remediation also needed to be tested using realistic scenarios instead of simply allocating and freeing memory.

### Lesson

Resource remediation needs realistic failure scenarios and careful cleanup behavior.

---

# Phase 4: Dashboard & Presentation

This phase focused on showing remediation results and documenting project progress.

### Work Completed

- Updated the dashboard to show before/after CPU, disk, memory, and network information.
- Added proper header comments to scripts.
- Updated the 12-week project plan.
- Created Week 5 presentation materials.

### Success

The dashboard provided visual evidence that remediation was working.

---

# Phase 5: EC2 / ECS AWS Support — First Attempt

The project began expanding its infrastructure simulation and AWS support.

### Work Completed

- Added EC2 and ECS simulation files and clients.
- Improved the dashboard.
- Added more UI/UX improvements.
- Addressed code-review change requests.
- Fixed issues blocking EC2/ECS rule execution.
- Improved error handling, resilience, and memory management.
- Added environment-variable loading for `SNOW_FAKE_MODE`.

### Major Trial & Error

- EC2/ECS rules were not executing because the condition format was wrong.
- An AWS-local target type was tried and later reverted.
- `SNOW_FAKE_MODE` was not being loaded correctly, which resulted in ServiceNow calls reaching protection unexpectedly.

### Lesson

Configuration and environment variables must be loaded correctly before external integrations are exercised.

---

# Phase 6: AWS Disk Alert Mapping

This phase focused on AWS disk alerts and expanding the resource simulation.

### Work Completed

- Added Dynatrace-to-AWS alert type mapping for `aws_disk`.
- Added simulated AWS disk alerts for end-to-end testing.
- Added matched-rule and before/after information to the dashboard.
- Added basic AWS CPU and AWS memory support.
- Created AWS CPU/memory simulation containers.
- Corrected import paths after restructuring.
- Separated fill and simulation behavior for AWS CPU/memory.
- Added `__init__.py` to the fill CPU package.
- Added missing Dockerfile spacing for `stress-ng` installation.

### Trial & Error

- Missing `__init__.py` caused `ModuleNotFoundError`.
- Dockerfile syntax caused `stress-ng` installation problems.
- Import paths repeatedly broke as the repository structure changed.
- An attempt was made to reuse Docker fill behavior for AWS simulation before separating the concepts.

---

# Phase 7: Merge Conflicts & Refactors

This phase involved restructuring the application and integrating multiple branches.

### Work Completed

- Added AWS alert types to the dashboard simulation dropdown.
- Fixed imports for the Flask blueprints refactor.
- Merged the main branch into testing.
- Improved AWS disk rules.
- Fixed DevTab issues.
- Added detection for remote remediation based on service health.
- Fixed DevTab merge conflicts.
- Added the project mind map.

### Major Trial & Error

- Flask blueprint refactoring moved files and broke imports.
- Changing `app = Flask(...)` to `create_app()` broke test fixtures.
- MiniStack/S3 removal broke invalid Docker commands for fake EC2.
- DevTab merge conflicts caused JSX parsing failures because of mismatched tags.
- Okta administration requirements blocked some endpoints and required `AUTH_DISABLED` behavior.

### Lesson

Large refactors require regression testing because changes to project structure can break imports, fixtures, and integrations in multiple places.

---

# Daily Activity Calendar

## Week 1 — May 21–23 — Foundation

### May 21
- Built the basic Flask server calling the Dynatrace API.
- Set up `.gitignore`.

### May 22
- Got affected entities outputting to the self-hosted dashboard.

---

## Week 2 — May 27–28 — ServiceNow Integration

### May 27
- Added `servicenow_client.py`.
- Wired the alert handler to ServiceNow incidents and work notes.
- Hit multiple integration errors while getting the workflow working.

### May 28
- Created `dynatrace_mapper.py`.
- Wrote the first unit tests for the mapper.

---

## Week 3 — June 1–5 — Memory Remediation

### June 1
- Added memory capabilities.
- Added removal and buildup behavior.
- Created a test container.
- Improved the log parser.

### June 2
- Integrated memory into the rule engine.

### June 3
- Added dashboard before/after metrics for all resource types.
- Fixed file-directory errors.

### June 4
- Added header comments for code quality.
- Updated the 12-week plan.

### June 5
- Continued work on memory scenarios and validation.

---

## Week 4 — June 8–12 — Memory Scenarios + Dashboard

### June 8
- Added more memory use cases.
- Developed realistic memory-after-remediation scenarios.
- Merged updates.

### June 9
- Built scenario/test containers.
- Fixed ServiceNow-related errors.
- Moved work into the executor structure.

### June 10
- Fixed additional memory errors.
- Added the Mermaid architecture diagram.
- Updated `.gitignore`.

### June 12
- Merged the dashboard update pull request.

---

## Week 5 — June 15–18 — AWS / EC2 / ECS

### June 15
- Added MiniStack and EC2/ECS simulation files and clients.
- Created an AWS-local target type before later reverting that approach.
- Fixed error handling.
- Improved the dashboard.

### June 16
- Main Jira task work:
  - Added `aws_disk` mapping.
  - Added `simulate_aws_disk`.
  - Added before/after dashboard information.
  - Added bare-bones AWS CPU and memory support.
  - Worked with multiple bug fixes involving imports, Dockerfile space, and learning the structure.

### June 17
- Fixed the EC2 container with a realistic blast scenario.
- Added AWS types to the dashboard dropdown.
- Fixed test imports after the Flask blueprint refactor.

### June 18
- Improved AWS disk rules.
- Continued work on making remediation more surgical and precise.

---

## Week 6 — June 22 — AWS CPU Logic + DevTab Redesign

### June 22
A major development day focused on CPU classification and DevTab behavior.

Work included:

- Designed CPU classification logic.
- Added configurable thresholds.
- Created graduated responses.
- Wrote 28+ new test cases.
- Developed the MiniStack CPU concept.
- Added CPU/memory severity scaling.
- Added severity scaling for all resource types.
- Added auto-detect behavior.
- Added a Dynatrace stub pipeline.
- Fixed `AUTH_DISABLED`.
- Resolved DevTab merge conflicts.
- Added information to the DevTab.

---

## Week 7 — June 25–30 — Rule Wizard + GitOps

### June 25
- Built a multi-step RuleWizard component.
- Added step reordering.
- Added conditional templates based on event type.
- Added tooltip support.
- Added GitOps rule sourcing from a separate GitHub repository.
- Updated the mind map.
- Added Profile & Settings views.
- Added a Calendar component.

### June 26
- Fixed a blank-screen bug.
- Merged the rule-wizard pull request.
- Added GitHub push/PR integration for rules.
- Added the `/rules` endpoint.
- Fixed sources using the local `rule_loader`.

### June 29
- Merged GitOps PR #50.
- Added line charts/sparklines to the before/after dashboard.

### June 30
- Added the MiniStack AWS CPU proof-of-concept for CPU remediation.
- Merged the AWS branch with the main branch.
- Fixed `RULES_DIR` and GitOps bugs.
- Merged a rules PR.

---

## Week 8 — July 1 — QoL Blitz + ServiceNow Link

### July 1
A large quality-of-life and UI integration day.

Work included:

- Added the ServiceNow link button to the incident page.
- Set up S3.
- Set up GitHub PATM.
- Merged an S3 branch.
- Fixed dev YAML.
- Added loading spinners.
- Added notifications.
- Added severity indicators.
- Added animated success and reflect behavior.
- Added Web Audio API.
- Built accessibility modes.
- Added high-contrast and colorblind options.
- Added language selection.
- Added hidden accessibility/voice features.
- Added keyboard shortcuts.
- Added hidden/easter-egg behavior.

---

## Week 8 Continued — July 6 — UX Polish & A11y Split

### July 6
- Moved the ServiceNow link to the Dashboard.
- Added a Recent Activity integration row.
- Split Settings and Accessibility into separate pages.
- Moved Accessibility into a dedicated area.
- Added keyboard navigation.
- Fixed focus behavior.
- Cleaned up unused files.

---

## Week 9 — July 7–8 — EKS / OTel Integration

### July 7
Built the initial EKS/OpenTelemetry infrastructure:

- Created a Kind cluster.
- Deployed an OpenTelemetry collector with Helm.
- Added a sample instrumented application.
- Added Kubernetes API endpoints.
- Added `/k8s/status`.
- Added `/k8s/deploy-demo`.
- Added `/k8s/logs`.
- Added the DevTab EKS/OTel section.
- Added namespace searching.
- Added environment-variable configuration.
- Added built-in collector deployment.
- Updated the README with EKS/OTel setup instructions.

### July 8
- Connected OTel Demo to Dynatrace.
- Configured telemetry flow.
- Verified traces and metrics arriving in Dynatrace.
- Identified partial-success warnings for unsupported metric types.

---

## Week 10 — July 9 — K8s Simulation, Pods, Helm Chart + Docker Compose

### July 9
- Migrated `pitcrew-disk` and `pitcrew-term` Docker containers into Kubernetes deployments.
- Created a simulation namespace.
- Added deployment and pod management.
- Added K8s status and logs.
- Added a base image using Python 3.11 Slim, Bash, `stress-ng`, and `curl`.
- Created the Docker Compose stack for local development.
- Added a backend/frontend container setup.
- Added auto-rebuild behavior.
- Built the Helm chart.
- Added a K8s configuration dashboard.
- Added local dev configuration.
- Delegated K8s remediation actions to another team member.

---

## Week 11 — July 10–13 — EKS Transition + Patches

### July 10
- Added a K8s external-access tunnel.
- Migrated to Helm 4.
- Added persistent logging using PVCs.
- Added EKS deployment patches.
- Added HPA for external remediation.
- Added a redeployment script.
- Got the remediation engine working in K8s.

### July 13
- Got EKS access from teammates.
- Fixed Docker Compose issues.
- Coordinated with Mike/Neal/Sergi for EKS access.
- Planned the CI/CD path using GitHub Actions → ECR → EKS.

---

## Week 12 — July 14–16 — Refactors + Documentation

### July 14
- Pulled refactor and GitOps changes.
- Moved scripts into `scripts/`.
- Removed old handling.
- Planned CI/CD work.
- Continued work on the microservices refactor.

### July 15
Documentation blitz:

- Created a user guide.
- Created an operator guide.
- Updated onboarding material.
- Added a deployment guide with a decision tree.
- Reorganized the `docs/` folder.
- Added a "Why Pitcrew Exists" section to the README.
- Updated the `.env.example`.
- Created a consolidated deployment guide.
- Added environment-variable references.
- Created a codebase guide.
- Added file-by-file descriptions.
- Updated documentation for non-technical users.
- Removed old MiniStack references when moving toward AWS/SSM.

### July 16
- Continued documentation and architecture cleanup.
- Updated documentation for the new microservices structure.
- Updated README content.
- Improved the dashboard and DevTab behavior.
- Continued work on the Kubernetes transition.

---

## Week 13 — July 20–22 — Dashboard UX + Bug Fixes

### July 20
- Fixed a widget dashboard edit-mode bug where the X button triggered navigation instead of deleting.
- Improved manual resolve behavior.
- Added a custom event bus.
- Added Nginx cache-busting headers.
- Improved DevTab behavior.

### July 21
- Deployed fixes to Kubernetes.
- Fixed `Preserve Manually` behavior.
- Added smooth tab transitions.
- Added profile panel animation.
- Added initial accessibility and UI polish.

### July 22
- Updated keyboard shortcuts.
- Added a tooltip layer.
- Improved deployment guidance for non-technical users.
- Added a guided tour.
- Added a final presentation polish pass.

---

## Week 14 — July 27 — Handoff

### July 27
- Completed the final mind map update.
- Prepared the project for handoff to the full-time developer.

---

# Overall Trial & Error

The project involved a significant amount of debugging and experimentation.

## ServiceNow

- API integration required multiple attempts.
- Work-note JSON formatting was difficult.
- Environment variables were not initially loading as expected.
- A fake-mode configuration issue resulted in ServiceNow calls reaching protection unexpectedly.

## Python / Project Structure

- Missing `__init__.py` files caused import errors.
- File-directory reorganizations repeatedly broke imports.
- Flask blueprint refactoring caused additional import failures.
- Changing the Flask application structure broke test fixtures.

## Docker

- Dockerfile syntax caused installation failures.
- `stress-ng` installation required correction.
- Docker Compose and container configuration needed repeated adjustment.
- Local AWS simulation initially reused concepts that were better separated.

## AWS

- EC2/ECS rules initially failed because the condition format was incorrect.
- An AWS-local target approach was tried and later reverted.
- AWS disk rules were initially too aggressive.
- Simulation behavior required additional testing and refinement.

## Kubernetes

- Namespace behavior needed to be separated for simulation.
- EKS access required coordination.
- Deployment and persistent logging configuration required iteration.
- Docker-to-Kubernetes migration introduced additional infrastructure work.

## Frontend / DevTab

- Merge conflicts caused JSX parsing failures.
- Incorrect tags caused broken rendering.
- Refactors created blank-screen bugs.
- UI behavior needed repeated testing after major merges.

---

# Overall Successes

The project ultimately achieved a large portion of the planned automation and infrastructure work.

## Completed Before Handoff

- Full auto-remediation pipeline:
  - Dynatrace
  - Rule engine
  - Executor
  - ServiceNow
- Seven alert types covering disk, memory, CPU, network, and other resource conditions.
- React dashboard with before/after remediation visibility.
- Widget system for dashboard/resource visualization.
- Full payload/rule matching with human-review enrichment.
- Audit logging for actions.
- Manual resolve functionality.
- Guided tours, keyboard shortcuts, accessibility, easter eggs, and other UI features.
- OpenTelemetry integration.
- Docker Compose development environment.
- Helm chart and EKS deployment work.
- Documentation rewritten for non-technical onboarding.
- `.env.example` files for local setup.
- 78+ unit tests passing.
- Smooth UI transitions, dark/light mode, profile panel animation, and guided UI polish.

---

# Project Metrics

The mind map recorded the following project-level metrics:

- **70+ commits** across the project.
- **78+ unit tests passing**.
- **40+ existing files modified**.
- **25+ new files created**.
- **8+ merge conflicts resolved**.
- Multiple pull requests merged.
- Multiple major architecture changes completed.
- Docker-based services migrated toward Kubernetes/EKS.
- Multiple resource types supported for automated remediation.

---

# Docker-to-K8s Migration Epic — Final Status

The migration work covered:

1. Dockerize Flask backend.
2. Dockerize React frontend.
3. Add K8s manifests for backend.
4. Add K8s manifests for frontend.
5. Migrate simulation containers into K8s deployments.
6. Execute local K8s deployments.
7. Build the DevTab for K8s workflow.
8. Add RBAC and ServiceAccount configuration.
9. Add K8s remediation actions such as rollout, restart, scale, and pod deletion.
10. Write tests for Pitcrew K8s behavior.
11. Deploy to real EKS.
12. Document the process.

---

# Architecture Evolution

The project evolved substantially throughout the internship.

## Starting Point

```text
Flask
  ↓
Dynatrace API
  ↓
Dashboard
```

## Expanded Automation

```text
Dynatrace
  ↓
Alert / Mapper
  ↓
Rule Engine
  ↓
Executor
  ↓
Remediation
  ↓
ServiceNow
```

## Infrastructure Simulation

```text
AWS / MiniStack
       ↓
Docker Containers
       ↓
Failure Simulation
       ↓
Remediation
       ↓
Before / After Validation
```

## Kubernetes / EKS Direction

```text
Dynatrace / OTel
       ↓
Pitcrew
       ↓
Kubernetes
       ↓
EKS
       ↓
Automated Remediation
```

---

# What Was Learned

## 1. Failure Is Part of Development

A large portion of the project was spent fixing things that did not work on the first attempt. Those failures were useful because they exposed weaknesses in the architecture and integration points.

## 2. Automation Needs Verification

A remediation action is not enough by itself. The system needs to verify that the service or resource actually recovered.

## 3. Testing Needs Realistic Failures

Memory allocation, CPU pressure, disk problems, service failures, and container issues need to be simulated realistically to determine whether an automated remediation system will behave correctly.

## 4. Architecture Changes Have Consequences

Moving files, changing Flask initialization, restructuring integrations, and migrating from Docker to Kubernetes can break existing code even when the new architecture is better.

## 5. Documentation Matters

The project eventually included user, operator, deployment, onboarding, and architecture documentation so that the system could be understood by people who did not build it.

---

# Handoff

The internship project reached a handoff point on **July 27, 2026**.

The final mind map was updated and the project was prepared for continued development by a full-time developer.

---

# Remaining / Future Work

The following items were identified for continued development:

1. Public AWS Application Load Balancer access for EKS.
2. CI/CD pipeline using GitHub Actions → ECR → EKS.
3. Terraform-based AWS resource management.
4. Full integration testing on EKS.
5. Dynatrace alert rules connected directly to the Pitcrew webhook.
6. ServiceNow tickets for whitelisted service warnings.
7. Threshold configuration through the DevTab UI.
8. Internationalization / UI label translation.

---

# Final Reflection

Project Pitcrew was not just a project where I built features. It was an opportunity to work through the full development process:

```text
Idea
 ↓
Prototype
 ↓
Integration
 ↓
Testing
 ↓
Failure
 ↓
Debugging
 ↓
Refactoring
 ↓
More Testing
 ↓
Automation
 ↓
Infrastructure Migration
 ↓
Documentation
 ↓
Handoff
```

This mind map exists to preserve that process.

The goal is to remember **what I built, what I broke, what I fixed, what worked, what did not work, and what I learned from each step**.
