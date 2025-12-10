---
title: "Event 6"
date: "2025-11-17"
weight: 6
chapter: false
pre: " <b> 4.6. </b> "
menu:
  main:
    name: "Event 6"
    weight: 6
---

# Summary Report: “Cloud Mastery Series #3: Security on AWS”

## Event Objectives

### Introduce AWS AI/ML and Generative AI

- To provide participants with a clear understanding of AWS AI/ML and generative AI services, including their roles in modern application development.

### Build Practical AI Knowledge

- To equip attendees with foundational and practical skills to design, build, and deploy AI/ML and generative AI solutions on AWS.

### Encourage Hands-On Learning

- To enable participants to experience real-world AI workflows through demonstrations and guided examples.

### Strengthen Community and Knowledge Sharing

- To foster collaboration and networking within the local AWS and AI/ML community.

### Speakers

- ***

## Key Highlights

### Challenges of Manual Infrastructure (“ClickOps”)

- Deployments take time, causing delays.
- Prone to manual errors and inconsistent configurations across environments.
- Difficult for teams to collaborate and maintain reproducible setups.

### Introduction to Infrastructure as Code (IaC)

- Manage cloud resources through code rather than manual console operations.
- Benefits: automation, scalability, reproducibility, and reduced provisioning errors.

### AWS CloudFormation

- AWS native IaC service using YAML or JSON templates to define and deploy stacks.
- Automatically creates, updates, and deletes resources as a unified unit.
- Supports drift detection to identify and fix deviations from templates.

### AWS Cloud Development Kit (CDK)

- Framework for defining IaC using familiar programming languages like Python, TypeScript, or Java.
- Constructs at multiple levels: L1 (direct CloudFormation mapping), L2 (developer-friendly defaults), L3 (pre-built patterns).
- CLI for initializing projects, synthesizing templates, deploying stacks, and detecting drifts.

### Choosing IaC Tools

- Consider single vs. multi-cloud, team expertise (developers vs. operations), and ecosystem compatibility.
- Comparison with Terraform, which uses HCL for cross-provider support.

### Docker and Containers

- Containers are lightweight, portable units including applications and dependencies.
- Dockerfiles ensure consistent images across development, testing, and production.
- Amazon ECR for secure image storage, scanning, and management.

### AWS Container Orchestration Services

- **Amazon ECS**: managed Docker orchestration with EC2 or Fargate.
- **Amazon EKS**: Kubernetes clusters with auto-scaling and updates.
- **AWS App Runner**: serverless deployment of web apps from code or images.
- Comparison: ECS is simpler and AWS-integrated; EKS offers flexibility and Kubernetes standards.

### CI/CD on AWS

- Source control with **CodeCommit**, using GitFlow or trunk-based development.
- Build & test with **CodeBuild**, deployment via **CodeDeploy** (blue/green, canary, rolling).
- Orchestration with **CodePipeline** for end-to-end automation.
- Demo showing a full pipeline from commit to production.

### Monitoring and Observability

- **AWS CloudWatch** for metrics, logs, dashboards, and alerts.
- **AWS X-Ray** for request tracing and identifying bottlenecks.
- Best practices: alerting, on-call rotations, full-stack visibility.

### DevOps Best Practices & Case Studies

- Advanced strategies: feature flags, A/B testing, automated testing integration.
- Incident management: blameless postmortems, lessons from startups and enterprises.

## Key Takeaways

### DevOps Mindset

- Promote collaboration between development and operations to accelerate delivery.
- Track metrics like DORA to measure deployment speed and reliability.
- Foster a culture of continuous improvement based on business needs.

### Technical Practices

- Use IaC for automated, version-controlled infrastructure to prevent errors.
- Leverage CDK constructs for reusable patterns in complex setups.
- Implement container orchestration with ECS or EKS according to workloads and team skills.
- Build robust CI/CD pipelines for frequent, low-risk releases.

### Observability & Reliability

- Integrate CloudWatch and X-Ray for proactive monitoring and rapid troubleshooting.
- Use deployment strategies like canary releases to minimize downtime.
- Perform regular drift checks and apply lifecycle policies for container management.

### Modernization Approach

- Assess current setups before migrating to microservices or containers.
- Implement in phases, experimenting with tools like App Runner for quick wins.
- Measure outcomes through cost savings, faster iterations, and improved agility.

### Applying to Work

- Incorporate Git strategies and CodePipeline into workflows for better automation.
- Try CDK for IaC in pilot projects to improve developer productivity.
- Set up observability dashboards to enhance incident response times.
- Conduct event storming to model container-based architectures.
- Pursue AWS DevOps certifications to advance career paths.

## Event Experience

- **Learning from experts:** AWS Community Builders shared practical knowledge, demos, and examples of microservices deployments.
- **Hands-on technical learning:** Explored CI/CD pipelines, IaC, and container orchestration; learned ECS vs. EKS trade-offs; monitored and remediated configuration drift.
- **Effective use of AWS tools:** CDK simplifies IaC using code, App Runner supports rapid deployment, and observability tools optimize application performance.
- **Networking & interaction:** Q&A and group discussions allowed exchanging ideas about tools and career guidance, aligning technology with business goals.

### Lessons Learned

- Automating IaC and CI/CD reduces risks and improves efficiency.
- Balanced container orchestration ensures scalability without complexity.
- Observability and blameless postmortems foster a resilient DevOps culture.
