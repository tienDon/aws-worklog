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

### Provide Foundational Knowledge of AWS Security Pillars

- Introduce the five pillars of the AWS Well-Architected Security Framework and explain the role of the Security Pillar in designing secure and resilient cloud architectures.

### Strengthen Cloud Security Skills

- Equip participants with essential knowledge to identify risks, build multi-layered protection, and implement industry-standard security measures on AWS.

### Improve Practical Understanding Through Demonstrations

- Help attendees gain hands-on awareness through demos such as IAM policy simulation, threat detection scenarios, incident handling workflows, and resource protection techniques.

### Foster Networking and Knowledge Sharing

- Encourage collaboration and knowledge exchange within the local AWS engineering community in Vietnam.

### Speakers

- **Kha Van (AWS)** – Host / Facilitator
- **Tran Duc Anh**: Cloud Security Engineer Trainee, AWS Cloud Club Captain SGU
- **Nguyen Tuan Thinh**: Cloud Engineer trainee
- **Nguyen Do Thanh Dat**: Cloud engineer Trainee
- **Thinh Lam**: FCJer
- **Viet Nguyen**: FCJer

---

## Key Highlights

### Shared Responsibility Model & Security Foundations

- Clarified the division of responsibilities between AWS and customers.
- Introduced core security principles: _Least Privilege_, _Zero Trust_, and _Defense in Depth_.
- Discussed common cloud vulnerabilities and threat patterns observed in Vietnam.

### Identity & Access Management (IAM)

- Covered IAM Users, Roles, Policies, and AWS security best practices.
- Demonstrated AWS IAM Identity Center (SSO), permission sets, and centralized identity management.
- Emphasized MFA enforcement, credential rotation, and IAM policy validation using simulation tools.

### Detection & Monitoring

- CloudTrail at the Organization level for unified logging.
- GuardDuty for threat intelligence and behavior anomaly detection.
- Security Hub for centralized security posture checks based on CIS and AWS best practices.
- EventBridge used for automating alerting and remediation actions.

### Infrastructure Protection

- VPC security: segmentation, subnet isolation, Security Groups vs NACLs.
- Use of AWS WAF, AWS Shield, and AWS Network Firewall.
- Workload protection: EC2 hardening, container image scanning, and runtime threat detection.

### Data Protection

- Encryption at-rest and in-transit for S3, EBS, RDS, and other AWS services.
- AWS KMS: key policies, key rotation, grants, and permission boundaries.
- Secrets Manager and Parameter Store for secure secrets lifecycle management.
- Data classification, access guardrails, and governance controls.

### Incident Response

- Explained the AWS incident response lifecycle and best practices.
- Reviewed multiple real-world playbooks:
  - Compromised IAM credentials
  - Publicly exposed S3 buckets
  - Malware detection in cloud workloads
- Showed workflows to snapshot, isolate, collect logs, and recover workloads.
- Demonstrated automated remediation using Lambda and Step Functions.

---

## Key Takeaways

### Security Mindset

- Security is a continuous process, not a one-time setup.
- Apply _least privilege_ consistently and enforce role-based access.
- Build security into design stages, not after deployment.

### Cloud Security Best Practices

- Enable mandatory logging: CloudTrail Organization, GuardDuty.
- Prefer IAM Roles over long-term access keys.
- Enforce encryption-by-default across all services.
- Perform configuration drift detection to maintain consistency.

### Observability & Threat Detection

- Combine CloudWatch, Security Hub, and GuardDuty for deep visibility.
- Use severity-based alerting integrated with Slack or email.
- Implement distributed tracing with X-Ray for microservices troubleshooting.

### Incident Preparedness

- Standardize incident playbooks and runbooks.
- Automate security responses for high-risk events.
- Conduct periodic security game days to practice real scenarios.

### Applying to Work

- Reassess current environments for Well-Architected compliance.
- Establish baseline security for IAM, logging, networking, and encryption.
- Deploy Security Hub and GuardDuty across multi-account environments.
- Integrate scanning into CI/CD and container workflows.
- Explore the AWS Security Specialty certification.

---

## Event Experience

- **Learning from AWS Experts:**  
  Attendees benefited from real-world insights, best practices, and practical demos delivered by AWS engineers and Community Builders.

- **Hands-on Learning:**  
  Participants observed live simulations of IAM access checks, organization-wide logging setups, GuardDuty threat findings, and incident response flows.

- **Effective Use of AWS Security Tools:**  
  Tools like CloudTrail, GuardDuty, Security Hub, KMS, and WAF demonstrated how to build continuous protection and monitoring capabilities.

- **Networking & Community Interaction:**  
  Q&A sessions and group discussions allowed participants to share experiences, gain career insights, and align technical decisions with business goals.

### Lessons Learned

- Multi-layered security ensures resilience even if one layer fails.
- Logging and monitoring are essential, not optional.
- Automation reduces human error and accelerates response time.
- Blameless postmortems and open communication help teams improve continuously.
