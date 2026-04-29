# AWS IAM Governance Lab

Enterprise-style AWS IAM governance implementation demonstrating multi-account access control, centralized identity management, least-privilege permissions, and organization-wide audit logging.

---

## Project Overview

This project simulates how an IAM / Cloud Security Analyst would design and implement access governance in a real-world AWS environment using AWS-native identity and security services.

A fictional company (**NovaTech Solutions**) required centralized workforce access management across multiple AWS accounts while enforcing:

* Role-Based Access Control (RBAC)
* Least Privilege Access
* Production Environment Segregation
* Privileged Access Management
* Centralized Audit Logging
* Identity Governance Best Practices

---

## Business Scenario

NovaTech Solutions operates separate AWS accounts for Development and Production workloads.

The company needed a secure IAM governance model that would:

* Allow developers to work only in development environments
* Allow security auditors to review both environments without modification rights
* Allow administrators privileged access through tightly controlled admin roles
* Capture and audit all privileged activity centrally across the AWS Organization

---

## Architecture Diagram

Can be found in the diagram folder

---

## Access Model

Can be found in the diagram folder

---

## AWS Services Used

* AWS Organizations
* AWS IAM Identity Center
* AWS IAM
* AWS CloudTrail
* Amazon S3

---

## Implemented Components

### AWS Organizations

Configured a multi-account AWS Organization with:

* Management Account
* NovaTech-Dev Account
* NovaTech-Prod Account

---

### IAM Identity Center

Configured centralized workforce authentication and account access management.

Implemented:

* Centralized AWS Access Portal
* User / Group Management
* Permission Set Assignments

---

### RBAC Group Structure

Created workforce groups representing business roles:

* Developers
* SecurityAuditors
* CloudAdmins

---

### Permission Sets

Configured permission sets aligned to business requirements:

| Permission Set        | Purpose                    |
| --------------------- | -------------------------- |
| Developer-Dev-Access  | Limited development access |
| Auditor-ReadOnly      | Read-only audit visibility |
| CloudAdmin-FullAccess | Administrative access      |

---

### Least Privilege IAM Policy

Created custom least-privilege developer policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ViewEC2AndS3",
      "Effect": "Allow",
      "Action": [
        "ec2:Describe*",
        "s3:ListAllMyBuckets",
        "s3:GetBucketLocation"
      ],
      "Resource": "*"
    }
  ]
}
```

---

## AWS Account Structure

| AWS Account        | Purpose                                 |
| ------------------ | --------------------------------------- |
| Management Account | Central Governance / Identity / Logging |
| NovaTech-Dev       | Development Environment                 |
| NovaTech-Prod      | Production Environment                  |

---

## Access Matrix

| Role             | Dev Account        | Prod Account |
| ---------------- | ------------------ | ------------ |
| Developer        | Limited Dev Access | No Access    |
| Security Auditor | Read Only          | Read Only    |
| Cloud Admin      | Full Access        | Full Access  |

---

## Security Controls Implemented

* Centralized workforce authentication via IAM Identity Center
* Group-based Role-Based Access Control (RBAC)
* Least-privilege developer permissions
* Development / Production environment separation
* Developers restricted from Production
* Privileged access isolated to CloudAdmins group
* Organization-wide CloudTrail logging enabled
* Centralized audit logs stored in S3

---

## Validation & Testing

Validated access assignments by testing each user role through the AWS Access Portal.

### Developer Validation

Confirmed:

* Access to NovaTech-Dev
* No visibility into NovaTech-Prod

---

### Security Auditor Validation

Confirmed:

* Read-only access to NovaTech-Dev
* Read-only access to NovaTech-Prod

---

### Cloud Admin Validation

Confirmed:

* Full privileged access to both environments

---

## Audit Validation

Validated organization-wide CloudTrail audit logging by performing a privileged IAM administrative action in a member account.

### Simulated Administrative Event

Created temporary IAM user:

```text
test-temp-user
```

---

### CloudTrail Verification

Confirmed CloudTrail captured the following event:

| Field             | Value             |
| ----------------- | ----------------- |
| Event Name        | CreateUser        |
| Event Source      | iam.amazonaws.com |
| User              | clara.admin       |
| Resource Affected | test-temp-user    |


---

## Repository Structure

```text
aws-iam-governance-lab/
├── README.md
│
├── diagrams/
│   ├── architecture-diagram.png
│   └── access-model-diagram.png
│
├── docs/
│   ├── architecture.md
│   ├── implementation-notes.md
│   ├── security-decisions.md
│   └── audit-validation.md
│
├── policies/
│   └── developer-dev-access-policy.json
│
└── screenshots/
    ├── organizations/
    ├── identity-center/
    ├── permission-sets/
    ├── assignments/
    ├── testing/
    └── cloudtrail/

```

---

## Supporting Documentation

* Architecture Notes
* Implementation Notes
* Security Decisions
* Audit Validation
  Can be found in the doc folder 

---

## Key Skills Demonstrated

* AWS Organizations Governance
* IAM Identity Center Administration
* AWS IAM Policy Authoring
* Role-Based Access Control (RBAC)
* Least Privilege Design
* Privileged Access Management
* CloudTrail Audit Monitoring
* Identity Governance & Administration (IGA)
* Multi-Account AWS Security Architecture

---

## Future Enhancements

* Implement Service Control Policies (SCPs)
* Add AWS Config Compliance Monitoring
* Configure CloudWatch Security Alerting
* Enforce MFA for Workforce Identities
* Integrate External Identity Provider (Okta / Microsoft Entra ID)

---

## Resume Summary

Designed and implemented a multi-account AWS IAM governance environment using AWS Organizations, IAM Identity Center, permission sets, least-privilege IAM policies, and CloudTrail audit logging to simulate enterprise IAM analyst responsibilities.
