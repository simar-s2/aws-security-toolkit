<div align="center">

<img src="docs/images/logo.svg" width="112" alt="aws-security-toolkit logo">

# aws-security-toolkit

**Five small tools that take an AWS organization from default settings to monitored, patched and hard to tamper with.**

[![Modules: 5](https://img.shields.io/badge/modules-5-111827?style=flat)](#modules)
[![Terraform 1.7+](https://img.shields.io/badge/Terraform-1.7%2B-7B42BC?style=flat&logo=terraform&logoColor=white)](#modules)
[![AWS CloudFormation](https://img.shields.io/badge/AWS-CloudFormation-FF9900?style=flat)](#modules)
[![Tests: no AWS account needed](https://img.shields.io/badge/tests-no_AWS_account_needed-2ea44f?style=flat)](#tested)
[![License: MIT](https://img.shields.io/badge/license-MIT-3b82f6?style=flat)](LICENSE)

<br>

<img src="https://raw.githubusercontent.com/simar-s2/security-digest/main/docs/images/demo.gif" width="820" alt="A terminal preview of the daily digest: findings by severity, counts per account, patch status and new CVEs.">

<sub>The daily digest from security-digest, previewed in a terminal with sample findings.</sub>

</div>

<a name="modules"></a>
## 🧩 The modules

This repo is the index. The code lives in the five repos below, and you can use any one of them without the others.

| | Module | What it does |
|---|---|---|
| <img src="docs/images/org-security-baseline.svg" width="40" alt=""> | [org-security-baseline](https://github.com/simar-s2/org-security-baseline) | Turns on audit logs and threat detection in every account, and keeps the logs where those accounts can't touch them |
| <img src="docs/images/account-baseline.svg" width="40" alt=""> | [account-baseline](https://github.com/simar-s2/account-baseline) | One command to fix the settings Security Hub flags on every new account |
| <img src="docs/images/org-patch-manager.svg" width="40" alt=""> | [org-patch-manager](https://github.com/simar-s2/org-patch-manager) | Patches EC2 instances in every account, with a tag deciding which ones may reboot |
| <img src="docs/images/ssm-access.svg" width="40" alt=""> | [ssm-access](https://github.com/simar-s2/ssm-access) | Reach instances with no open ports and no SSH keys stored on them |
| <img src="docs/images/security-digest.svg" width="40" alt=""> | [security-digest](https://github.com/simar-s2/security-digest) | Posts a daily summary of security findings to Slack |

Each one comes as a Terraform module and as CloudFormation with a one-command deploy script.

## 🔬 How they fit

```mermaid
flowchart LR
    baseline["org-security-baseline<br/>turns on detection"] --> hub["Security Hub<br/>findings"]
    account["account-baseline<br/>fixes account settings"] --> hub
    access["ssm-access<br/>makes instances manageable"] --> patch["org-patch-manager<br/>patches them"]
    patch --> hub
    hub --> digest["security-digest<br/>posts to Slack"]
```

The full picture, across every account: [docs/DESIGN.md](docs/DESIGN.md).

## ⚡️ Run it

You need an AWS organization with a management account, a log-archive account and a security tooling account. Deploy in this order:

1. [org-security-baseline](https://github.com/simar-s2/org-security-baseline#run-it), across those three accounts.
2. [account-baseline](https://github.com/simar-s2/account-baseline#run-it), from the management account, to cover every account.
3. [ssm-access](https://github.com/simar-s2/ssm-access#run-it), in each workload account.
4. [org-patch-manager](https://github.com/simar-s2/org-patch-manager#run-it), from the management account.
5. [security-digest](https://github.com/simar-s2/security-digest#run-it), in the security account.

## 💰 Cost

GuardDuty, Security Hub and AWS Config are the paid parts, billed per account and region. GuardDuty and Security Hub each start with a 30-day free trial, which shows your real numbers before you commit. The other modules cost little.

<a name="tested"></a>
## 🧪 How it's tested

`make test` in any module runs against a mocked AWS, so it needs no account and costs nothing. Linters and security checks run in CI. These tests check the code's logic, not how real AWS responds, so try a module in a test organization first.

## 📄 License

[MIT](LICENSE)
