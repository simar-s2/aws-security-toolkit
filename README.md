# aws-security-toolkit

**Five small, independently deployable modules that take an AWS Organization from default settings to a monitored, patched, tamper-resistant baseline. Each one ships as a Terraform module and as CloudFormation with a one-command deploy script.**

This repository is the index. The code lives in the module repositories below, so you can adopt one without the others.

## Modules

| Repository | What it does | Runs in |
|---|---|---|
| [org-security-baseline](https://github.com/simar-s2/org-security-baseline) | CloudTrail, GuardDuty, Security Hub (FSBP) and AWS Config in every account, with logs in a locked, encrypted log-archive account | Management, log archive and security accounts |
| [account-baseline](https://github.com/simar-s2/account-baseline) | One idempotent command for the account settings Security Hub flags on every new account: public access blocks, EBS encryption, password policy, default VPC report | Each account (script, Terraform, or an org-wide StackSet) |
| [org-patch-manager](https://github.com/simar-s2/org-patch-manager) | SSM Patch Manager in every account through a StackSet that enrolls new accounts automatically, with a tag deciding whether an instance may reboot | Management account, deploys to every account |
| [ssm-access](https://github.com/simar-s2/ssm-access) | Keyless instance access with Session Manager, plus SSH over SSM for VS Code with keys the instance accepts for 60 seconds | Each workload account |
| [security-digest](https://github.com/simar-s2/security-digest) | A daily Slack digest of Security Hub findings across the organization, with optional real-time alerts | Security account |

## License

[MIT](LICENSE)
