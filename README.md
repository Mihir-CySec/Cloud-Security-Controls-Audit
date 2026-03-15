AWS Cloud Security Control Audit

Why this project exists
Cloud security audits are one of the most technically demanding and highest-value services in the IT audit and tech risk market. Every company running workloads on AWS needs someone who can assess their environment against a recognized benchmark, communicate findings with technical precision, and verify that remediations actually worked. This project demonstrates that capability end to end — from running aws cloudtrail describe-trails to issuing a formal audit report.

What's in this repo
FileWhat it representsDemoCloud_AWS_Security_Audit_Report_MihirTrivedi.docxFull audit report — executive summary, findings, compliant items, re-audit validation, appendicesDemoCloud_Findings_Summary.xlsxColor-coded findings tracker with risk dashboard and before/after remediation status

Engagement context
Client: DemoCloud — fictional startup running a web application on AWS
Auditor: Mihir Trivedi (read-only access granted for assessment)
Benchmark: CIS AWS Foundations Benchmark Level 1
Audit period: January–February 2026
Re-audit date: February 14, 2026

Findings summary
5 findings across Critical through Low severity:
Finding IDTitleCIS ControlRatingF-001CloudTrail disabled in non-primary regionsCIS 3.1HighF-002IAM policy grants * on S3 (excessive privilege)CIS 1.16CriticalF-003S3 bucket demoapp-bucket with public read ACLCIS 2.1.5CriticalF-004Root account missing MFACIS 1.5CriticalF-005Security group allows SSH from 0.0.0.0/0CIS 5.2High
All findings include: CIS Control ID, affected resource name, detection method (CLI command + output), risk rationale, and step-by-step remediation.

Technical evidence — CLI commands used
Each finding was detected using AWS CLI commands documented in the report and appendix:
bash# CloudTrail coverage check
aws cloudtrail describe-trails --include-shadow-trails

# IAM policy review
aws iam list-policies --scope Local
aws iam get-policy-version --policy-arn <arn> --version-id v1

# S3 bucket ACL check
aws s3api get-bucket-acl --bucket demoapp-bucket
aws s3api get-public-access-block --bucket demoapp-bucket

# Root MFA status
aws iam get-account-summary

# Security group rules
aws ec2 describe-security-groups --filters Name=ip-permission.from-port,Values=22
This isn't a checklist exercise — the report shows realistic CLI output and explains exactly what each result means and why it constitutes a finding.

Re-audit validation
After remediation was applied, each finding was re-tested and confirmed closed:
FindingPrevious StatusPost-Remediation StatusValidatedF-001 CloudTrailNon-compliantCompliantFeb 10, 2026F-002 IAM wildcardNon-compliantCompliantFeb 11, 2026F-003 Public S3Non-compliantCompliantFeb 11, 2026F-004 Root MFANon-compliantCompliantFeb 12, 2026F-005 SSH openNon-compliantCompliantFeb 13, 2026

Compliant items noted
Four controls confirmed passing at initial audit — included to demonstrate balanced, objective assessment (not just a findings dump):

CloudWatch log metric filters for unauthorized API calls
S3 bucket logging enabled on production buckets
Password policy meets CIS complexity requirements
VPC flow logs enabled on default VPC


Frameworks applied

CIS AWS Foundations Benchmark Level 1 — primary assessment standard
AWS Well-Architected Framework (Security Pillar) — referenced in recommendations
NIST SP 800-53 — control mapping in appendix


Skills demonstrated
Cloud Security Auditing AWS Security CIS Benchmarks IAM Policy Review S3 Security CloudTrail Security Groups AWS CLI Risk Rating Remediation Validation Technical Report Writing Excel Dashboards
