# AWS-Enterprise-IAM-Hardening
This project simulates a real-world enterprise cloud security scenario focused on enforcing least privilege access controls and detecting unauthorized privilege escalation attempts within an AWS environment.
# Objective: 
To design a secure IAM architecture that restricts operational users to only the permissions required for their role, while enabling security teams to monitor and investigate suspicious activity through audit logging.

# Problem Statement:
In enterprise environments, excessive IAM permissions increase the risk of:
- Privilege escalation.
- Insider threats.
- Accidental misconfiguration.
- Audit and compliance violations.

The goal was to:
- Restrict support engineers to EC2 operational tasks only.
- Prevent any IAM or logging modification actions.
- Enable centralized monitoring of failed or unauthorized attempts.
- Validate detection using AWS CloudTrail.

# SOLUTION OVERVIEW
Designed and implemented an enterprise-grade IAM security architecture in AWS to enforce least privilege, separation of duties, and audit visibility.
Created two role-based access control (RBAC) groups:
- SupportEngineers – Granted permission to start, stop, and describe EC2 instances only. No IAM or logging modification permissions were allowed.
- SecurityAuditors – Provided read-only access to IAM configurations and AWS CloudTrail logs to monitor activity and investigate security events without the ability to modify resources.

A test support user was created to simulate insider privilege escalation attempts, including creating IAM users, roles, and policies. All unauthorized actions resulted in AccessDenied, validating proper least privilege enforcement.

Enabled AWS CloudTrail (multi-region) to capture management events across the account. SecurityAuditors successfully reviewed failed IAM attempts through event history, analyzing:
- EventName
- UserIdentity
- SourceIPAddress
- ErrorCode (AccessDenied)
- EventTime

To further harden the environment, an explicit deny policy was implemented to block all IAM modification actions and prevent CloudTrail deletion or logging suspension. This ensures critical security controls remain protected even if broader permissions are mistakenly assigned in the future.

# Impact
This project demonstrates the design and validation of enterprise-grade IAM security controls within AWS, combining preventive security (access control) with detective security (logging and investigation).
It reflects real-world cloud security engineering practices used in production environments.
