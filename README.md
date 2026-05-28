# AWS IAM Security Audit & Remediation Project

## Overview

This project demonstrates a hands-on AWS IAM security audit and remediation exercise using AWS native IAM tools and manual policy reviews.

Multiple IAM and S3 security misconfigurations were intentionally created, identified, analyzed, and remediated following AWS security best practices.

---

## AWS Services Used

- AWS IAM
- IAM Credential Report
- IAM Access Analyzer
- Amazon S3

---

## Key Security Concepts Demonstrated

- IAM Security Auditing
- Least Privilege Access
- IAM Policy Review
- Public S3 Exposure Detection
- MFA Enforcement
- Security Remediation
- IAM Governance

---

## Security Findings & Remediation

| Finding | Severity | Detection Method | Remediation |
|---|---|---|---|
| MFA disabled for admin user | High | Credential Report | Enabled MFA |
| Public S3 bucket access | Critical | IAM Access Analyzer | Blocked public access |
| Wildcard IAM role permissions | High | Manual IAM Review | Restricted permissions |

---

# Finding 1 — MFA Disabled

## Issue

An IAM administrative user was configured without MFA protection.

## Risk

If credentials are compromised, attackers could gain full administrative access to the AWS account.

## Detection

Detected using IAM Credential Reports.

## Remediation

Enabled virtual MFA using an authenticator application.

## Validation

Credential report and IAM console confirmed MFA activation.

---

# Finding 2 — Public S3 Bucket

## Issue

An S3 bucket was configured with public read access through bucket policy permissions.

## Risk

Sensitive data exposure to external users.

## Detection

Detected using IAM Access Analyzer.

## Remediation

- Removed public bucket policy
- Enabled Block Public Access settings

## Validation

Access Analyzer findings cleared after remediation.

---

# Finding 3 — Wildcard IAM Role Permissions

## Issue

An IAM role contained overly permissive wildcard permissions.

### Before Policy

```json
{
  "Effect": "Allow",
  "Action": "*",
  "Resource": "*"
}
```

## Risk

Violates least privilege principles and increases privilege escalation risk.

## Detection

Detected through manual IAM policy review.

## Remediation

Replaced wildcard permissions with restricted S3 read-only permissions.

### After Policy

```json
{
  "Effect": "Allow",
  "Action": [
    "s3:GetObject",
    "s3:ListBucket"
  ],
  "Resource": "*"
}
```

## Validation

Validated restricted access and reduced permissions scope.

---

## Key Learnings

- Importance of MFA for privileged accounts
- Risks of public S3 exposure
- Dangers of wildcard IAM permissions
- Principle of Least Privilege
- IAM auditing and remediation workflow
- Security governance using AWS IAM

---

## Outcome

Successfully performed a complete IAM security audit and remediation exercise by identifying security risks, validating findings, applying remediations, and verifying compliance improvements using AWS IAM best practices.
