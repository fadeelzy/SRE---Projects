## SRE Projects – Infrastructure Reliability, Observability & Automation

This project showcases real-world Site Reliability Engineering (SRE) practices by designing and operating production-grade systems with automated deployments, full observability, fault tolerance, and measurable performance improvements. It demonstrates how I apply reliability principles to achieve 99.9% uptime, reduce deployment risks, and build systems that are secure, scalable, and self-healing.

⭐ Key Achievements

Built fully automated cloud infrastructure using Terraform/Kubernetes, enabling repeatable, zero-downtime environment provisioning.

Implemented end-to-end observability with Prometheus, Grafana & Alertmanager — delivering real-time metrics, actionable alerts, and reduction of mean-time-to-detect (MTTD) by ~60%.

Designed a centralized logging pipeline (Loki + Promtail) to streamline debugging and reduce incident resolution time (MTTR under 10 minutes).

Created CI/CD pipelines (GitHub/GitLab) with automated testing, security scans, and rolling deployments, cutting deployment time by ~50%.

Developed automation scripts for backups, log rotation, and health checks, reducing manual operational load by ~70%.

Performed load testing (Locust/k6) to validate system scalability and ensure reliability under high traffic.

Deployed a sample microservice application with auto-scaling, monitoring dashboards, and recovery playbooks, simulating a real production environment. See the /docs folder for:- Architecture diagram- SLOs, SLIs & error budget- Runbooks- Incident response playbook.

sre-project/

│
├── infra/

│   ├── terraform/      

│   ├── kubernetes/     

│   └── ansible/     

│
├── monitoring/

│   ├── prometheus/

│   ├── grafana/

│   ├── alertmanager/

│   └── dashboards/       # JSON exported dashboards

│
├── logging/

│   ├── loki/

│   └── promtail/

│
├── ci-cd/

│   ├── github-actions.yml

│   └── gitlab-ci.yml

│
├── automation/

│   ├── backup.sh

│   ├── health-check.py

│   └── log-cleanup.sh

│
├── load-testing/

│   ├── locustfile.py

│   └── k6-script.js

│
├── src/

│   ├── app/

│   └── Dockerfile

│
├── docs/

│   ├── architecture.png

│   ├── sre-runbook.md

│   ├── incident-response.md

│   ├── uptime-slos.md

│   ├── dashboards.png

│   └── ci-cd-flow.png

│
└── README.md

