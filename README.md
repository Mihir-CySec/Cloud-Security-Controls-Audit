AWS CLOUD SECURITY AUDIT
DemoCloud | CIS AWS Foundations Benchmark Level 1
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

A simulated cloud security audit of a deliberately misconfigured
AWS environment. Five findings from discovery to remediation
verification — including CLI evidence, risk ratings, and a
re-audit confirming all findings closed.

WHAT I BUILT
━━━━━━━━━━━━
Audit Report      Executive summary, 5 findings, re-audit results
Findings Tracker  Color-coded Excel with risk dashboard

THE WORK
━━━━━━━━
Assessed DemoCloud's AWS environment against CIS Level 1 using
AWS CLI commands — not a manual checklist. Found three Critical
findings (wildcard IAM policy, public S3 bucket, root account
missing MFA) and two High findings (CloudTrail gaps, SSH open
to 0.0.0.0/0). Documented each finding with the exact CLI
command used, realistic output, and step-by-step remediation.
Re-audited after fixes and confirmed all five findings closed.

FINDINGS
━━━━━━━━
F-001  HIGH      CloudTrail disabled in non-primary regions
F-002  CRITICAL  IAM policy grants * on S3
F-003  CRITICAL  S3 bucket demoapp-bucket publicly readable
F-004  CRITICAL  Root account has no MFA
F-005  HIGH      Security group allows SSH from anywhere

All five closed and re-validated between Feb 10–13, 2026.

CLI COMMANDS USED
━━━━━━━━━━━━━━━━━
aws cloudtrail describe-trails --include-shadow-trails
aws iam get-policy-version --policy-arn <arn> --version-id v1
aws s3api get-bucket-acl --bucket demoapp-bucket
aws iam get-account-summary
aws ec2 describe-security-groups --filters Name=ip-permission.from-port,Values=22

FRAMEWORKS
━━━━━━━━━━
CIS AWS Foundations Benchmark L1  |  AWS Well-Architected
NIST SP 800-53
