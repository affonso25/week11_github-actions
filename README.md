# GitHub Actions CI/CD Project

## Project Description

This project demonstrates the implementation of CI/CD pipelines using GitHub Actions, Docker, Terraform, and AWS OIDC authentication.

The repository includes workflows for:

- Continuous Integration (CI)
- Docker image build and push
- Terraform infrastructure deployment
- AWS authentication with OIDC
- Matrix builds
- Reusable workflows
- Production deployment approvals
- Local workflow testing with act

---

# Repository Structure

```text
project-root/
├── .github/
│   └── workflows/
│       ├── hello.yml
│       ├── ci.yml
│       ├── image.yml
│       ├── aws-test.yml
│       ├── terraform.yml
│       ├── build-all.yml
│       ├── reusable-image.yml
│       ├── release.yml
│       └── deploy-prod.yml
├── services/
│   ├── user-service/
│   ├── product-service/
│   └── order-service/
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
└── README.md
```

---

# Workflow Explanations

## hello.yml

Simple workflow used to validate GitHub Actions setup.

## ci.yml

Runs Maven validation, compilation, and unit tests for the Java microservice.

## image.yml

Builds and pushes Docker images to Docker Hub.

## aws-test.yml

Tests AWS authentication using GitHub OIDC.

## terraform.yml

Runs Terraform format, validation, plan, and apply.

## build-all.yml

Uses matrix strategy to build multiple services in parallel.

## reusable-image.yml

Reusable workflow for Docker image builds.

## release.yml

Calls reusable workflows for multiple services.

## deploy-prod.yml

Production deployment workflow with manual approval and deployment summary.

---

# Required GitHub Secrets

The following GitHub Secrets are required:

| Secret Name | Description |
|---|---|
| DOCKERHUB_USERNAME | Docker Hub username |
| DOCKERHUB_TOKEN | Docker Hub access token |
| AWS_ROLE_TO_ASSUME | AWS IAM Role ARN for OIDC |
| SLACK_WEBHOOK | Slack webhook URL (optional) |

---

# How to Trigger Workflows

## Automatic Triggers

- Push to main branch
- Pull requests
- Terraform file changes

## Manual Triggers

Some workflows use:

```yaml
workflow_dispatch:
```

These workflows can be triggered manually from the GitHub Actions tab.

---

# Docker Hub Repository Information

Docker images are pushed to Docker Hub repositories:

- affonso25/product-service
- affonso25/user-service
- affonso25/order-service

Docker images are tagged using:

- latest
- github.sha

---

# Terraform Usage Instructions

Terraform files are stored inside:

```text
terraform/
```

Main commands used:

```bash
terraform init
terraform validate
terraform plan
terraform apply
```

Terraform workflows run automatically using GitHub Actions.

---

# AWS OIDC Setup Summary

AWS OIDC authentication was configured using:

- GitHub Actions OpenID Connect provider
- AWS IAM Role
- GitHub Actions configure-aws-credentials action

This removes the need to store AWS access keys in GitHub Secrets.

The following permissions were configured in AWS IAM:

- EC2 permissions
- VPC permissions
- Terraform deployment permissions

OIDC Provider URL:

```text
https://token.actions.githubusercontent.com
```

Audience:

```text
sts.amazonaws.com
```