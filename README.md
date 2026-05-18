
# DriftGuard : Risk-Aware Terraform Reconciliation Engine

DriftGuard is a risk-aware infrastructure reconciliation system built to continuously detect, classify, and respond to Terraform drift across AWS environments.
Instead of blindly auto-remediating every infrastructure change, DriftGuard evaluates operational risk first and dynamically decides how the system should respond.
Built as an internal infrastructure governance prototype using Terraform, GitHub Actions, AWS, Python, Slack, and GitHub Issues.

--- 

# 🚀 Features
- Continuous Terraform drift detection
- Risk-aware drift classification
- Severity-based remediation workflow
- Automatic Terraform reconciliation
- Slack alert routing by severity
- GitHub Issues audit trail
- Terraform JSON plan parsing
- Multi-environment support (dev + prod)
- Remote Terraform state management
- Infrastructure governance & visibility

--- 

# 🛠 Tech Stack
|  Component | Technology  |
|---|---|
| Infrastructure as Code | Terraform | 
| Cloud Provider | AWS |
| Risk Engine | Python | 
| Notification | Slack Webhooks |
| Audit Trail | Github Issues |
| Remote Backend + State Locking | AWS S3 |

--- 

# 🏗️ Architecture
```
GitHub Actions Scheduler
          ↓
Terraform Plan Generation
          ↓
Terraform JSON Parser
          ↓
Risk Classification Engine
          ↓
Decision Layer
 ┌────────┼───────────┐
 ↓        ↓           ↓
AutoFix  Escalation  Alerting
          ↓
Slack Routing Engine
          ↓
GitHub Audit Trail

```

--- 

# ⚙️ How It Works
- GitHub Actions triggers scheduled Terraform drift checks
- Terraform generates a plan and exports JSON output
- Python risk engine analyzes infrastructure changes
- Drift is assigned a severity score
- Decision layer determines remediation behavior
- Alerts are routed to Slack channels dynamically
- High/Critical drift events create GitHub Issues
- Infrastructure is reconciled based on severity rules

--- 

# 🔍 Severity Model
|  Severity | Action  |
|---|---|
| LOW  | Auto-remediate silently |
| MEDIUM | Auto-remediate + Slack alert |
| HIGH | Create GitHub Issue + require approval |
| CRITICAL | Freeze remediation + escalate immediately |

--- 

## 📌 Example Risk Weights
```
	RISK_WEIGHTS = {
    "security_group_open_ingress": 90,
    "iam_policy_change": 85,
    "s3_public_access": 80,
    "instance_type_change": 40,
    "asg_capacity_change": 35,
    "missing_tags": 10
}
```
