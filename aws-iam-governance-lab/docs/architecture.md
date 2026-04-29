# Architecture Overview

## Organizational Structure
- Management Account hosts AWS Organizations and IAM Identity Center
- Member Accounts:
  - NovaTech-Dev
  - NovaTech-Prod

## Logging Architecture
- Organization Trail enabled in Management Account
- Centralized S3 bucket stores CloudTrail logs

## Access Model
- Developers → Dev only
- Auditors → Read-only everywhere
- Admins → Full access everywhere