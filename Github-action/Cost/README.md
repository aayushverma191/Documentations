
# GitHub Actions Pricing Guide
Comparison of Self-Hosted Runners vs GitHub-Hosted (Managed) Runners

---
# Table of Contents

- [Overview](#overview)
- [Repository Visibility Explained](#repository-visibility-explained)
  - [Public Repository](#public-repository)
  - [Private Repository](#private-repository)
- [Self-Hosted Runner Pricing](#self-hosted-runner-pricing)
  - [Formula](#formula)
  - [Example Usage](#example-usage)
  - [More Examples](#more-examples)
- [GitHub Hosted Runner Pricing](#github-hosted-runner-pricing)
  - [Example](#example)
- [Example Scenario](#example-scenario)
- [Pros and Cons](#pros-and-cons)
  - [GitHub Hosted](#github-hosted)
  - [Self Hosted](#self-hosted)
- [Recommendation](#recommendation)
- [References](#references)

## Overview

GitHub Actions supports two execution models:

1. **GitHub-hosted runners**
   - Infrastructure managed by GitHub
   - Pay based on runner minutes
   - No server maintenance required

2. **Self-hosted runners**
   - Infrastructure managed by you
   - Runner can run on:
     - AWS EC2
     - GCP VM
     - Kubernetes
     - On-prem server
   - You manage maintenance and scaling

---

# Repository Visibility Explained

GitHub pricing for self-hosted runners depends on repository visibility.

## Public Repository

A public repository means:

- Anyone on the internet can view the code
- Usually open-source projects

Example:

https://github.com/kubernetes/kubernetes

Pricing:

- GitHub Actions self-hosted usage charge: **$0**
- Only infrastructure cost applies


---

## Private Repository

A private repository means:

* Only invited users/team members can access code
* Used by most company/internal projects


Pricing:

* GitHub platform charge may apply for self-hosted runner usage depending on GitHub plan and pricing model
* Plus infrastructure cost

---

# Self-Hosted Runner Pricing

## Formula

```text
Total Cost =
GitHub Runner Usage Cost
+
Infrastructure Cost
```

Infrastructure includes:

* EC2 / VM
* Storage
* Kubernetes worker nodes
* Networking
* Monitoring

---

## Example Usage

Monthly usage: **10,000 minutes**

GitHub fee estimate:

```text
10,000 × $0.002
= $20
```

Infrastructure:

```text
EC2 instance
≈ $25/month
```

Total:

```text
$20 + $25
≈ $45/month
```

---

## More Examples

| Monthly Minutes | GitHub Fee | Infra (~$25) | Total |
| --------------- | ---------: | -----------: | ----: |
| 10,000          |        $20 |          $25 |   $45 |
| 50,000          |       $100 |          $25 |  $125 |
| 100,000         |       $200 |          $25 |  $225 |

> Note: Infrastructure cost varies depending on EC2 size, Kubernetes nodes, autoscaling, and cloud provider.

---

# GitHub Hosted Runner Pricing

GitHub manages infrastructure.

Pricing is based on:

* Runner OS
* Build minutes
* GitHub plan

Approximate Linux pricing:

```text
~$0.008/min
```

GitHub plans include free monthly minutes:

| Plan             | Included Minutes |
| ---------------- | ---------------- |
| Free             | 2,000            |
| Pro              | 3,000            |
| Enterprise Cloud | 50,000           |

---

## Example

Monthly build usage:

```text
4,500 minutes
```

With Pro plan:

```text
Paid Minutes:

4500 − 3000
=1500
```

Cost:

```text
1500 × $0.008
=$12/month
```

Without free minutes:

```text
4500 × $0.008
=$36/month
```

---

# Example Scenario

Assumptions:

* 5 microservices
* Average build time = 3 minutes
* Each service builds 10 times/day
* Lower environments only
* 30 days/month
* Linux runners

Daily usage:

```text
5 services × 10 builds × 3 minutes
=150 min/day
```

Monthly:

```text
150 × 30
=4,500 min/month
```

Estimated cost:

| Option        | Monthly Cost |
| ------------- | ------------ |
| GitHub Hosted | ~$12–36      |
| Self Hosted   | ~$45–70      |

---

# Pros and Cons

## GitHub Hosted

### Pros

* No infrastructure management
* Quick setup
* Auto-scaled
* Maintained by GitHub

### Cons

* Can become expensive at scale
* Limited customization
* Less control over build environment

---

## Self Hosted

### Pros

* Better for heavy Docker builds
* Full control over CPU/RAM
* Build caching support
* Can integrate with Kubernetes autoscaling

### Cons

* Requires infrastructure maintenance
* Monitoring responsibility
* Scaling management required

---

# Recommendation

Low usage (<10k minutes/month)

→ GitHub Hosted usually cheaper

High usage (>50k minutes/month)

→ Self-hosted often becomes more cost effective

Particularly useful for:

* Docker builds
* Kubernetes workloads
* EKS deployments
* Terraform pipelines
* CI systems with heavy build workloads

---

# References

## Official GitHub Pricing

GitHub Pricing:
[https://github.com/pricing](https://github.com/pricing)

GitHub Pricing Calculator:
[https://github.com/pricing/calculator](https://github.com/pricing/calculator)

GitHub Actions Billing:
[https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions)

GitHub Hosted Runner Pricing:
[https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions)

Self-hosted Runners:
[https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners](https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners)

GitHub Actions Changelog:
[https://github.blog/changelog/](https://github.blog/changelog/)

Northflank Analysis:
[https://northflank.com/blog/github-pricing-change-self-hosted-alternatives-github-actions](https://northflank.com/blog/github-pricing-change-self-hosted-alternatives-github-actions)

---
