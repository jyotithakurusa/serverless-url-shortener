# Serverless URL Shortener

> A production-style URL shortener built entirely on AWS serverless primitives, with infrastructure defined as code in Terraform and a fully automated CI/CD pipeline.

**Status:** 🚧 Work in progress
**Tech stack:** AWS (API Gateway · Lambda · DynamoDB · CloudFront) · Terraform · GitHub Actions

---

## What it does

Takes a long URL, generates a short slug, stores the mapping in DynamoDB, and redirects clicks via API Gateway + Lambda. CloudFront sits in front for low-latency redirects. The point of the project isn't the app itself — it's demonstrating clean AWS architecture, IaC, and CI/CD.

## Planned features

- [x] Project scaffolding
- [ ] DynamoDB table with partition-key design
- [ ] Lambda functions (create / redirect / analytics)
- [ ] API Gateway routing
- [ ] CloudFront distribution with custom domain
- [ ] Click analytics + per-URL stats
- [ ] Terraform modules for every resource
- [ ] Remote state on S3 + DynamoDB lock table
- [ ] GitHub Actions: `terraform plan` on PR, `terraform apply` on merge to main
- [ ] Multi-environment (dev / prod) via Terraform workspaces

## Architecture

```
Client → CloudFront → API Gateway → Lambda → DynamoDB
```

All resources defined in Terraform — `terraform apply` provisions the entire stack from scratch.

## Tech stack rationale

- **API Gateway + Lambda** — pay-per-request, auto-scaling, zero ops overhead
- **DynamoDB** — single-digit-millisecond reads at scale, no schema migrations
- **CloudFront** — edge caching for low-latency redirects globally
- **Terraform** — provider-agnostic IaC; the standard at most enterprises
- **GitHub Actions** — keeps CI/CD inside the same repo as the code

## How to deploy

```bash
git clone https://github.com/jyotithakurusa/serverless-url-shortener.git
cd serverless-url-shortener/infra
terraform init
terraform plan
terraform apply
```

## Roadmap

- v0.1 — Single-Lambda URL create + redirect
- v0.2 — Terraform-managed deploy
- v0.3 — CloudFront + custom domain
- v0.4 — Click analytics
- v0.5 — CI/CD pipeline
- v1.0 — Multi-env (dev/prod) with workspaces

---

**Author:** Jyoti Thakur · [GitHub](https://github.com/jyotithakurusa) · jyotithakurusa@gmail.com
