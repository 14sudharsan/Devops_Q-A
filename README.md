# Devops_Q-A


AWS (Detailed Grouping with Answers)

1. IAM / Security / Access Control
Q: What’s your approach to automating IAM role provisioning (including trust relationships, SAML/OIDC federation) across multiple accounts?
A: Use Infrastructure as Code tools like Terraform or CloudFormation to define IAM roles centrally, then deploy across accounts. Trust relationships should be configured using IAM policy documents, with federation via SAML/OIDC for identity providers. Automation ensures consistency, compliance, and easier lifecycle management.

Q: How do you automate EC2 start/stop , SAML and IAM role creation using the Automation and integrate with Service Now Catalog?
A: AWS Systems Manager Automation documents (SSM documents) can automate EC2 start/stop and IAM tasks. These can be exposed via ServiceNow Catalog integration using AWS Service Management Connector, allowing self-service actions while enforcing guardrails.

Q: Describe how you’d build an automation pipeline that identifies unused IAM roles, keys, and security groups and remediates them safely.
A: Use AWS Config and custom Lambda functions to detect unused roles/keys. Collect metrics such as last-used timestamps, then apply automated workflows to disable, notify owners, and eventually delete. Security groups can be scanned for zero-reference, then removed with approval-based automation.

Q: How do you automate the setup of cross-account AssumeRole policies while ensuring least privilege?
A: Define AssumeRole trust policies as code and push them using Terraform or CloudFormation StackSets. Enforce least privilege by granting only specific actions to designated principals. Automated policy linting tools (like OPA) can validate before deployment.

Q: What are best practices to automate rotating IAM access keys and secrets across thousands of workloads?
A: Use AWS Secrets Manager or Systems Manager Parameter Store to rotate and distribute secrets automatically. Applications should consume credentials via SDKs rather than hardcoding. Rotation frequency should align with compliance policies and integrate with CI/CD pipelines.

Q: How do you enforce KMS key policies and rotation automatically across an enterprise environment?
A: Enable automatic key rotation in AWS KMS, and use AWS Config rules to ensure compliance. Non-compliant keys can be detected and remediated with automation pipelines, ensuring encryption standards are enforced across all accounts.

Q: How do you manage users in multiple AWS accounts?
A: Implement AWS SSO or IAM Identity Center for centralized identity management. Federation with corporate IdPs (Okta, Azure AD) allows single sign-on. Automation with Terraform/SSO APIs helps in onboarding/offboarding at scale.

Q: How would you use Python/Boto3 scripts to map IAM roles to EC2 instances across all accounts?
A: Iterate through accounts using boto3 STS AssumeRole, list EC2 instances and their attached IAM roles. Cross-reference roles with policies to generate a dependency map. This aids audits and least privilege validation.

Q: What are Trust relationship?
A: A trust relationship is a policy in an IAM role defining which entities (users, roles, accounts, or services) can assume that role. It allows secure delegation of permissions across accounts or services using sts:AssumeRole.

Q: What are Inline policies and Customer Managed Policies?
A: Inline policies are embedded directly in a single IAM entity (user/group/role) and deleted with it. Customer Managed Policies are standalone, reusable policies managed by the customer, allowing centralized control and versioning.

---

2. S3 / Storage
Q: How would you detect and auto-remediate public S3 buckets or overly permissive security groups?
A: Use AWS Config managed rules (e.g., s3-bucket-public-read-prohibited). Violations can trigger automation (Lambda/SSM) to remove public access and notify teams. For SGs, automation can remove 0.0.0.0/0 rules unless explicitly whitelisted.

Q: How do you secure private S3 content via CloudFront when multiple services (e.g., APIs, apps) consume the same bucket?
A: Use CloudFront Origin Access Control (OAC) or Origin Access Identity (OAI) to restrict direct bucket access. Signed URLs or cookies provide fine-grained access for multiple consumers while maintaining centralized security at the CDN layer.

Q: How would you use Python/Boto3 scripts to enforce encryption for all new S3 buckets?
A: A boto3 script can scan all buckets, check encryption settings, and apply default SSE-S3/KMS encryption. Automation can be scheduled via Lambda + EventBridge to enforce compliance continuously.

Q: How do you automate resource lifecycle management (EBS snapshots, AMI cleanup, S3 object expiration)?
A: Implement lifecycle policies in S3, use Data Lifecycle Manager (DLM) for EBS snapshots and AMI cleanup. Automation scripts or Lambda functions can ensure periodic cleanup of unused resources to save cost.

---

3. CloudFront / CDN / WAF / Shield
Q: How do you build a reusable automation framework to provision CloudFront distributions with private S3 origins?
A: Use Terraform modules or CloudFormation templates with variables for OAI/OAC, signed URLs, and cache behaviors. This ensures repeatable deployments across applications while enforcing security standards.

Q: How would you automate provisioning of CloudFront + WAF + Shield Advanced as a standard service pattern?
A: Create a template that provisions CloudFront distributions with integrated WAF ACLs and Shield protection. Automate deployment via IaC pipelines, ensuring all apps follow the same security baseline.

Q: How do you enforce CloudFront cache policies and origin failover automatically across multiple applications?
A: Define standard cache policies in IaC modules and enforce them with Config rules. Failover configurations (multi-origin setup) should be built into reusable templates to ensure consistency.

Q: How do you integrate CloudFront with private API Gateway endpoints or ALBs securely?
A: Use VPC links or Lambda@Edge for authentication. CloudFront communicates with private endpoints using secure channels while denying direct internet access to the backend services.

---

4. Logging / Monitoring / Guardrails
Q: How would you build an automation that generates standardized landing zone guardrails (SCPs, IAM boundaries, Config rules) for new AWS accounts?
A: Use AWS Control Tower or custom landing zone automation to bootstrap new accounts. Automation provisions SCPs, IAM boundaries, and config rules as part of the account creation process, ensuring security guardrails from day one.

Q: How do you automate centralized logging setup (CloudTrail, Config, VPC Flow Logs, GuardDuty) for every account in AWS Organizations?
A: Use organization-level CloudTrail and delegated administrator accounts for Config/GuardDuty. Automation scripts can enforce log delivery to a central S3 bucket and SIEM integration for monitoring.

Q: How do you integrate automation workflows with Security Hub, Macie, GuardDuty, and Wiz?
A: Enable findings aggregation in Security Hub, and automate remediation using EventBridge + Lambda. Findings can be pushed to ticketing tools like ServiceNow for continuous compliance management.

Q: How would you automate the deployment of Service Control Policies across Organizational Units (OUs) with exceptions?
A: Use AWS Organizations APIs or Terraform StackSets to push SCPs at OU level. Exceptions can be managed by tagging accounts and excluding them via conditional policies.

---

5. Governance / Compliance / Policy as Code
Q: How would you enforce standardized tagging policies and auto-remediate non-compliant resources using automation?
A: Use AWS Config rules to detect missing tags and trigger Lambda automation to add defaults or notify owners. Tools like Service Catalog TagOptions can enforce tagging at provisioning.

Q: What’s your approach to policy as code (e.g., AWS Config, OPA, or Terraform Sentinel)?
A: Define compliance rules in code and integrate them in CI/CD pipelines. For example, OPA Gatekeeper can validate Kubernetes manifests, while Terraform Sentinel enforces rules during terraform plan/apply.

Q: How do you enforce compliance guardrails without blocking developer velocity?
A: Implement a phased pipeline (warn → auto-remediate → block). Developers get alerts first, automation fixes common issues, and blocking happens only when critical violations persist.

Q: How do you handle automation idempotency and rollback in large-scale AWS workflows?
A: Use transaction-like patterns: automation should check current state before applying changes (idempotency). Rollback is managed using checkpoints, snapshots, or version-controlled IaC for quick recovery.

Q: How do you implement AWS tagging for resources?
A: Define a tagging strategy (environment, owner, cost center) and enforce via Service Catalog and IaC. Retroactive tagging can be handled with Lambda or CLI scripts.

Q: How do you tag existing AWS resources using automation?
A: Use boto3 scripts or Systems Manager automation documents to apply tags at scale. AWS Tag Editor can be used for bulk updates, while automation ensures consistency across accounts.

---

6. Cost Optimization / Resource Lifecycle
Q: What’s your approach to automating cost governance?
A: Identify unused or idle resources with AWS Trusted Advisor, Compute Optimizer, or custom scripts. Automate cleanup of snapshots, idle RDS/EC2, and orphaned ELBs. Integrate with budgeting alerts for proactive cost control.

Q: How would you use Python/Boto3 scripts to identify unused Elastic IPs and release them?
A: Use EC2 describe-addresses API, filter unassociated IPs, and call release-address for cleanup. Automation can notify owners before releasing to avoid impact.

Q: If we have 50 servers that need to be shut down when idle, how will you do it?
A: Implement CloudWatch alarms for low CPU utilization, trigger Lambda/SSM automation to stop instances. Scheduled stop/start automation via EventBridge can also optimize usage.

---

7. Automation / Pipelines / Self-service
Q: How would you integrate ServiceNow Catalog with AWS Service Catalog or Lambda workflows?
A: Use AWS Service Management Connector for ServiceNow to expose AWS services in the catalog. Requests trigger Lambda or Service Catalog provisioning, providing governance with self-service.

Q: How would you automate the provisioning of API Gateway endpoints with custom domains, WAF, and Lambda authorizers?
A: Create reusable templates defining API Gateway, WAF integration, and Lambda authorizers. Deploy via IaC pipelines to ensure repeatable deployments across environments.

Q: How do you integrate Jenkins/GitHub Actions pipelines with Terraform/CloudFormation?
A: Use CI/CD pipelines to run terraform plan/apply or cloudformation deploy. Add policy-as-code validation and security scans before deployment to enforce best practices.

Q: What’s your approach to creating automation libraries (Python/Boto3) that can be reused across CoE teams?
A: Build modular Python libraries for common tasks (e.g., tagging, patching, compliance). Store in artifact repositories (PyPI, CodeArtifact) and enforce reuse in projects to avoid duplication.

Q: How do you manage multi-account Lambda automation frameworks?
A: Create a central automation account with IAM roles in spoke accounts. Lambda in central account assumes roles to perform actions, simplifying governance and reducing duplication.

---

8. General AWS / Hands-on
Q: How would you automate AWS account creation with guardrails (SCPs, Config, IAM baselines)?
A: Use AWS Control Tower or custom bootstrapping scripts integrated with AWS Organizations APIs. Automation applies SCPs, IAM baselines, and Config rules on account creation, ensuring compliance from the start.

Q: How do you build a framework to automatically generate a resource dependency map (EC2 → ENI → SG → IAM → S3)?
A: Use boto3 to crawl resources and relationships, store them in a graph database (e.g., Neo4j). Visualization helps in impact analysis and auditing dependencies.

Q: How do you automate patch management across EC2 and RDS instances using SSM Patch Manager and Config?
A: Define patch baselines in Systems Manager, schedule patching via maintenance windows, and enforce compliance via AWS Config. Automation ensures non-compliant instances are remediated.

Q: How would you enforce ring-fencing controls in AWS using automation?
A: Implement SCPs and VPC Service Control Policies to block lateral traffic. Automation validates rules continuously and auto-remediates misconfigured networks.

Q: What are the AWS Services that you have worked?
A: List core services (EC2, S3, RDS, Lambda, CloudFront, IAM, CloudWatch, Config, Control Tower, etc.) with examples of how you used them in projects.

Q: How will you deploy a 3 tier application in AWS?
A: Deploy using VPC with public/private subnets, ALB in public, app servers in private, RDS in isolated subnet. Use ASG for scalability, IAM for secure access, and IaC for repeatability.

Q: I have lambda function that takes a long time to execute, how will you troubleshoot?
A: Analyze CloudWatch logs and X-Ray traces to identify bottlenecks. Optimize code, adjust memory allocation (affects CPU), or break tasks into Step Functions for better scaling.

Q: Have you created a Golden AMI and how do you share it with different AWS accounts?
A: Golden AMIs are built with Packer or EC2 Image Builder, hardened with security agents. They can be shared across accounts by modifying launch permissions or distributing via AWS Marketplace.

Q: How many servers are you currently handling?
A: Answer should reflect scale (e.g., 200+ EC2 across multiple accounts) and emphasize automation-first management.

Q: How do you patch the servers?
A: Use SSM Patch Manager or Ansible automation to deploy patches. Define maintenance windows, test in staging, and report compliance. Automation ensures security and consistency.
