# AWS Engineering Lab

**A hands-on journey into AWS Cloud Engineering, Infrastructure as Code, Python automation, DevOps and SRE.**

## About

This repository documents my practical learning journey and engineering experiments across the AWS ecosystem.

The goal is to build, automate, test, document and operate cloud environments using modern DevOps practices.

All labs are designed to be reproducible, version-controlled and progressively more complex.

## Learning Objectives

- **AWS:** Cloud architecture, networking, IAM, storage, compute, databases and serverless.
- **Terraform:** Infrastructure as Code, reusable modules, remote state and automation.
- **Python:** AWS SDK (boto3), scripting, API integrations and automated testing.
- **DevOps:** Docker, CI/CD, GitHub Actions and infrastructure automation.
- **SRE:** Observability, reliability, incident management and operational excellence.

## Technology Stack

| Technology | Purpose |
|---|---|
| AWS | Cloud infrastructure |
| Floci | Local AWS service emulation |
| Terraform | Infrastructure as Code |
| Python | Automation and AWS integrations |
| boto3 | AWS SDK for Python |
| Docker | Containerization and local environments |
| GitHub Actions | CI/CD and automated validation |
| Kubernetes | Container orchestration |

## Repository Structure

```text
aws-engineering-lab/
├── docs/
├── labs/
├── terraform/
├── python/
├── applications/
├── docker/
└── .github/
    └── workflows/
```

## Learning Roadmap

- [ ] Environment setup and local AWS emulation
- [ ] AWS fundamentals and cloud architecture
- [ ] Terraform fundamentals and advanced concepts
- [ ] AWS networking and security
- [ ] Python and boto3 automation
- [ ] AWS compute, storage and databases
- [ ] Serverless and event-driven architectures
- [ ] Docker and CI/CD
- [ ] Kubernetes and container orchestration
- [ ] Monitoring, observability and SRE
- [ ] End-to-end cloud engineering projects

## Engineering Principles

Every lab should include:

1. Problem statement and learning objectives.
2. Architecture and technical decisions.
3. Infrastructure and application code.
4. Deployment and validation instructions.
5. Troubleshooting scenarios.
6. Cleanup instructions.
7. Key learnings and limitations.

## Local Development

The initial environment uses Docker and Floci to emulate selected AWS services locally.

**Important:** Local emulation does not guarantee identical behavior to real AWS services. Critical architectures, permissions, networking and integrations must also be validated in an AWS sandbox account.

## Progress

This repository evolves continuously as new concepts, labs and engineering challenges are completed.

**Status:** Learning in progress.

---

*Built through hands-on experimentation, continuous learning and engineering best practices.*