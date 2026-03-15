════════════════════════════════════════════════════════════════
AWS CLOUD SECURITY AUDIT — DEMOCloud
CIS AWS Foundations Benchmark Level 1
════════════════════════════════════════════════════════════════
 
Simulated cloud security audit of a deliberately misconfigured
AWS environment, assessed against CIS AWS Foundations Benchmark
Level 1. Includes five detailed findings, CLI-based evidence,
risk-rated remediation steps, and a re-audit validation section
confirming closure — the full arc of a real cloud security
engagement.
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHY THIS PROJECT EXISTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
Cloud security audits are one of the most technically demanding
and highest-value services in IT audit and tech risk. Every
company running workloads on AWS needs someone who can assess
their environment against a recognized benchmark, communicate
findings with technical precision, and verify that remediations
actually worked. This project demonstrates that capability end
to end — from running CLI commands to issuing a formal audit
report.
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHAT'S IN THIS REPO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
  DemoCloud_AWS_Security_Audit_Report_MihirTrivedi.docx
  → Full audit report — executive summary, 5 findings,
    compliant items, re-audit validation, CLI appendix
 
  DemoCloud_Findings_Summary.xlsx
  → Color-coded findings tracker with risk dashboard
    and before/after remediation status
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ENGAGEMENT CONTEXT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
  Client        DemoCloud — fictional startup, AWS-hosted web app
  Auditor       Mihir Trivedi (read-only access granted)
  Benchmark     CIS AWS Foundations Benchmark Level 1
  Audit period  January – February 2026
  Re-audit      February 14, 2026
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FINDINGS SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
  ID      CIS Control   Rating     Title
  ──────  ────────────  ─────────  ──────────────────────────────────────
  F-001   CIS 3.1       High       CloudTrail disabled in non-primary regions
  F-002   CIS 1.16      CRITICAL   IAM policy grants * on S3 (excessive privilege)
  F-003   CIS 2.1.5     CRITICAL   S3 bucket demoapp-bucket with public read ACL
  F-004   CIS 1.5       CRITICAL   Root account missing MFA
  F-005   CIS 5.2       High       Security group allows SSH from 0.0.0.0/0
 
Each finding includes: CIS Control ID, affected resource name,
detection method with CLI command and output, risk rationale,
and step-by-step remediation instructions.
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TECHNICAL EVIDENCE — CLI COMMANDS USED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
  CloudTrail coverage
    aws cloudtrail describe-trails --include-shadow-trails
 
  IAM policy review
    aws iam list-policies --scope Local
    aws iam get-policy-version --policy-arn <arn> --version-id v1
 
  S3 public access check
    aws s3api get-bucket-acl --bucket demoapp-bucket
    aws s3api get-public-access-block --bucket demoapp-bucket
 
  Root MFA status
    aws iam get-account-summary
 
  Security group rules
    aws ec2 describe-security-groups \
      --filters Name=ip-permission.from-port,Values=22
 
The report includes realistic CLI output for each command and
explains exactly what each result means and why it constitutes
a finding — this is not a checklist exercise.
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RE-AUDIT VALIDATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
After remediation, all five findings were re-tested and confirmed
closed:
 
  Finding           Before            After         Validated
  ────────────────  ────────────────  ────────────  ──────────────
  F-001 CloudTrail  Non-compliant     Compliant     Feb 10, 2026
  F-002 IAM *       Non-compliant     Compliant     Feb 11, 2026
  F-003 Public S3   Non-compliant     Compliant     Feb 11, 2026
  F-004 Root MFA    Non-compliant     Compliant     Feb 12, 2026
  F-005 SSH open    Non-compliant     Compliant     Feb 13, 2026
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMPLIANT ITEMS NOTED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
Four controls confirmed passing at initial audit — included to
demonstrate a balanced, objective assessment:
 
  · CloudWatch log metric filters for unauthorized API calls
  · S3 bucket logging enabled on all production buckets
  · Password policy meets CIS complexity requirements
  · VPC flow logs enabled on default VPC
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FRAMEWORKS APPLIED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
  · CIS AWS Foundations Benchmark Level 1 (primary standard)
  · AWS Well-Architected Framework — Security Pillar
  · NIST SP 800-53 — control mapping in appendix
 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SKILLS DEMONSTRATED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 
  Cloud Security Auditing  ·  AWS Security  ·  CIS Benchmarks
  IAM Policy Review  ·  S3 Security  ·  CloudTrail Analysis
  Security Group Assessment  ·  AWS CLI  ·  Risk Rating
  Remediation Validation  ·  Technical Audit Reporting
  Excel Risk Dashboards  ·  Bash / Linux CLI
 
