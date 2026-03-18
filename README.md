
# Terraform Drift Detection & Auto-Remediation

Automated system to detect and remediate infrastructure drift in real-time using Terraform, GitHub Actions, and AWS.

Designed to simulate production-grade infrastructure governance with continuous reconciliation, audit visibility, and self-healing capabilities.

--- 

# 🚀 What This Project Does
- Detects infrastructure drift every 1 minute
- Automatically remediates drift using ```terraform apply```
- Tracks drift events via GitHub Issues (audit trail)
- Supports multi-environment setup (dev + prod)
- Enforces infrastructure consistency without manual intervention

# 🧠 Why This Exists
In real systems, infrastructure drift happens due to:
- Manual changes in AWS Console 
- External scripts/tools. 
- Misconfigurations over time

This project implements a continuous reconciliation model:

> Terraform state + GitHub Actions act as the source of truth enforcement layer

# 🏗️ Architecture
```
GitHub (Code + Workflows)
        │
        ▼
GitHub Actions (CI/CD + Drift Detection)
        │
        ├───────────────┐
        ▼               ▼
   AWS Infrastructure   S3 Backend (State + Locking)
 (VPC, ALB, ASG, EC2)       ↑
        │                   │
        └──── Drift ────────┘
                Detection

+ GitHub Issues → Audit trail
+ Slack (optional) → Alerts

```

# ⚙️ Core Components

|  Component | Purpose  |
|---|---|
| Terraform | Defines desired infrastructure state | 
| S3 Backend | Centralized state + locking |
| GitHub Actions | Executes CI/CD + drift detection | 
| Drift Workflow | Detects + auto-fixes drift |
| GitHub Issues | Tracks drift events (audit + visibility) |

# 🔄 How It Works

-  GitHub Actions triggers every minute
-  Terraform plan compares actual vs. desired state
-  If drift detected (exit code 2): auto-apply fixes
-  Create/close GitHub issues and Slack notifications
	

# 🧪 How Drift is Handled
- Infrastructure modified outside Terraform
- Drift workflow runs (every 1 min)
- terraform plan detects mismatch
- GitHub Issue created
- terraform apply restores state
- Issue closed automatically

# 📌 Key Takeaways
- Demonstrates real-world drift problem + solution
- Implements continuous infra reconciliation
- Combines CI/CD + security enforcement
- Shows production-oriented Terraform practices
