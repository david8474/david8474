🚀 ENGINEERING PROJECT PORTFOLIO
# David Joseph 

### Secure Architecture • Cloud • Automation • Networking • IaC

Building secure, scalable, and production-ready cloud infrastructure and backend solutions.

This portfolio highlights representative engineering projects. Sensitive files and production implementations remain private for security.

📌 PROJECTS COVERED IN THIS PORTFOLIO

The following engineering projects are presented in detail below:

# 🚀 PROJECT 1

# Global Banking P95/P99 Latency Optimization Platform

Live Demo https://global-banking-latency-dashboard.vercel.app

(SLA-Driven Performance Engineering, Observability, Automation)

## 🚀 Project 2 — Enterprise Payment Platform

### 📂 Source Code

👉 https://github.com/david8474/enterprise-payment-platform

Production-ready payment platform built with **FastAPI** and **Go** using **Clean Architecture** and **SOLID** principles.

**⚙️ Stack:** FastAPI • Go • PostgreSQL • Redis • JWT • OAuth2 • RBAC • Docker • Kubernetes • Helm • GitHub Actions • Prometheus • Grafana • OpenTelemetry

# 🚀 PROJECT 3
## Real-Time Financial Risk & Customer Friction Optimization Platform

🔗 Live Demo (Production):
https://santander-financial-risk-dashboard-sigma.vercel.app

PROJECT 4 - Federal Multi-Enclave Insider-Threat & Anomaly Detection System

PROJECT 5 - CSfC Network Operations Platform (Tier 2/3, PKI, STIG, IaC)

PROJECT 6 - Secure Healthcare Cloud Data Platform (IaC, Airflow, IAM, Data Governance)

Each project demonstrates production-oriented design, security-first architecture, and disciplined automation practices.

PROJECT 1 – Global Banking P95/P99 Latency Optimization Platform
(SLA-Driven Performance Engineering, Observability, Automation)

📄 README.md
# Bank Global Latency & Stability Platform

Enterprise-grade platform for monitoring, analyzing, and automatically
remediating global service latency and stability issues.

## Key Capabilities
- Distributed latency probes
- SLA and percentile analysis (P95 / P99)
- Automated detection and remediation workflows
- Infrastructure as Code (Terraform)
- Orchestrated pipelines (Airflow)
- Local reproducible environments (Docker)

This repository contains sanitized, representative samples suitable for
public review. Full production implementations remain private.

📄 PROJECT_SUMMARY.txt
Project: Global Latency & Stability Platform

Purpose:
Detect, analyze, and respond to latency degradation across distributed systems.

Core Components:
- Terraform for infrastructure provisioning
- Airflow for scheduled data pipelines
- CI/CD workflows for validation
- Shell scripts for operational control

Design Principles:
- Modularity
- Automation-first
- Reproducibility
- Production-aligned architecture

📄 QUICKSTART.md
## Quick Start

1. Validate environment
   ./scripts/preflight.sh

2. Start local platform
   ./scripts/local_up.sh

3. Access services
   - Airflow UI: http://localhost:8080

4. Run smoke tests
   ./scripts/smoke_test.sh

5. Stop platform
   ./scripts/local_down.sh

📂 terraform/main.tf
terraform {
  required_version = ">= 1.5.0"
}

provider "aws" {
  region = var.aws_region
}

locals {
  common_tags = {
    Project = "Latency-Stability-Platform"
    Managed = "Terraform"
  }
}

module "network" {
  source = "./modules/network"
  vpc_id = var.vpc_id
}

📂 airflow/dags/latency_pipeline.py
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

def compute_percentiles(**context):
    pass

def detect_sla_breach(**context):
    pass

def submit_change_request(**context):
    pass

with DAG(
    dag_id="latency_pipeline",
    schedule_interval="*/5 * * * *",
    start_date=datetime(2024, 1, 1),
    catchup=False,
) as dag:

    compute_task = PythonOperator(
        task_id="compute_percentiles",
        python_callable=compute_percentiles,
        provide_context=True,
    )

    detect_task = PythonOperator(
        task_id="detect_sla_breach",
        python_callable=detect_sla_breach,
        provide_context=True,
    )

    change_request_task = PythonOperator(
        task_id="submit_change_request",
        python_callable=submit_change_request,
        provide_context=True,
    )

    compute_task >> detect_task >> change_request_task

📄 docker-compose.yml
version: "3.9"

services:
  postgres:
    image: postgres:14
    environment:
      POSTGRES_USER: airflow
      POSTGRES_PASSWORD: airflow
      POSTGRES_DB: airflow

  airflow:
    image: apache/airflow:2.7
    depends_on:
      - postgres
    ports:
      - "8080:8080"

📂 .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run smoke tests
        run: ./scripts/smoke_test.sh

📂 scripts/preflight.sh
#!/usr/bin/env bash
set -e

command -v docker >/dev/null 2>&1 || exit 1
command -v docker-compose >/dev/null 2>&1 || exit 1

echo "✓ Environment validated"

📂 scripts/smoke_test.sh
#!/usr/bin/env bash
set -e

docker ps >/dev/null 2>&1

echo "✓ Smoke tests passed"

📂 scripts/local_up.sh
#!/usr/bin/env bash
set -e

docker-compose up -d

echo "✓ Platform started"

📂 scripts/local_down.sh
#!/usr/bin/env bash
set -e

docker-compose down

echo "✓ Platform stopped"
📂 ansible/inventory/dev.yml
all:
  hosts:
    router1:
      ansible_host: 192.0.2.10
    router2:
      ansible_host: 192.0.2.11

📂 ansible/group_vars/dev.yml
env: dev
latency_threshold: 120
qos_profile: gold

network_segments:
  - name: core
    cidr: 10.0.0.0/16
  - name: edge
    cidr: 10.1.0.0/16
📂 ansible/templates/deploy_report.json.j2
{
  "deployment": {
    "environment": "{{ env }}",
    "timestamp": "{{ ansible_date_time.iso8601 }}",
    "status": "{{ deployment_status }}"
  },
  "network": {
    "segments": {{ network_segments | to_json }},
    "latency_threshold_ms": {{ latency_threshold }},
    "qos_profile": "{{ qos_profile }}"
  }
}

📂 ansible/roles/network_render/tasks/main.yml
- name: Render network deployment report
  template:
    src: deploy_report.json.j2
    dest: /tmp/deploy_report_{{ env }}.json

📂 ansible/roles/network_deploy_mock/tasks/main.yml
- name: Simulate network configuration deployment
  debug:
    msg: "Deploying network configuration to {{ inventory_hostname }}"

- name: Apply latency threshold
  debug:
    msg: "Latency threshold set to {{ latency_threshold }} ms"

📂 ansible/roles/validate/tasks/main.yml
- name: Validate latency threshold
  assert:
    that:
      - latency_threshold > 0
      - latency_threshold < 500

📂 ansible/inventory/dev.yml
all:
  hosts:
    router1:
      ansible_host: 192.0.2.10
    router2:
      ansible_host: 192.0.2.11

📂 ansible/group_vars/dev.yml
env: dev
latency_threshold: 120
qos_profile: gold

network_segments:
  - name: core
    cidr: 10.0.0.0/16
  - name: edge
    cidr: 10.1.0.0/16

📂 catalog/NETWORK_SEGMENT.md
# Network Segmentation Catalog

Segments:
- Core: Internal routing and backbone traffic
- Edge: Ingress, probes, and external-facing services

Segmentation enforces isolation and latency observability boundaries.

📂 catalog/QOS_ROLLOUT.md
# QoS Rollout Strategy

Profiles:
- bronze: best-effort
- silver: business-critical
- gold: latency-sensitive services

QoS profiles are applied per segment and validated post-deployment.

📂 catalog/LATENCY_PROBES.md
# Latency Probes

Probes are deployed at strategic ingress and egress points.
Measurements feed percentile-based SLA evaluation pipelines.



PROJECT 3
🚀 Real-Time Financial Risk & Customer Friction Optimization Platform

🔗 Live Demo (Production):
https://santander-financial-risk-dashboard-sigma.vercel.app

📊 Overview

This project simulates a real-time banking risk intelligence platform designed to detect fraud, automate security decisions, and optimize customer experience simultaneously.

Unlike traditional systems that prioritize either security or usability, this platform demonstrates a balanced, adaptive approach:

⚖️ Maximize Low-Friction Transactions while preserving strong fraud protection

🧠 Core Capabilities
🔹 Customer Friction Score Breakdown
Low Friction: 67 (56%)
Medium Friction: 38 (32%)
High Friction: 15 (13%)

📌 Friction score measures the interruption experienced by customers during verification.
The system dynamically minimizes friction without weakening risk controls.

🔹 Adaptive Authentication Engine

Risk-based decision system that automatically selects the optimal response:

✅ Allow (No Friction) → Seamless approval
🔄 Soft Verify → Lightweight confirmation
⚠️ Step-Up MFA → Additional validation
🚫 Hold / Block → High-risk containment
🔹 Live Attack Simulation (SOC Scenario)

Simulates a full fraud lifecycle:

Suspicious Login
Account Takeover Pattern
Fraudulent Transaction Attempt
Automated Secure Response
Compliance Audit Trail

📊 Live Risk Score: 87 / 100 (Critical)
⚠️ Customer Friction Spike: 75 / 100

🔹 Real-Time Observability Metrics
False Positive Rate: 9%
Secure Approvals: 72
Friction Avoided: 89 events
Avg Verification Time: 36s

📌 Designed to reflect SRE-style monitoring (SLIs/SLOs mindset)

🔹 Compliance & Audit Layer
📜 PCI-DSS style logging
🔐 GDPR-aligned privacy-safe evidence
🧾 Immutable audit trail for security events
🏗️ Architecture (Conceptual)
User Transaction
      ↓
Risk Engine (Scoring + Anomaly Detection)
      ↓
Adaptive Auth Decision Layer
      ↓
[Allow | Verify | Step-Up | Block]
      ↓
Audit + Monitoring + Dashboard
⚙️ Tech Stack
Frontend: React + TypeScript (Vite)
Deployment: Vercel (Global Edge Delivery)
Backend (Simulated APIs): Node.js
Concepts Applied:
Risk scoring models
Event-driven security decisions
Observability metrics (P95/P99 mindset)
DevSecOps principles
🎯 Engineering Impact

This project demonstrates:

🔐 Security-first design with UX awareness
⚡ Real-time decision systems under risk conditions
📊 SRE-style monitoring and incident simulation
🧠 Ability to model complex financial systems
☁️ Cloud-ready, scalable frontend deployment
💡 Key Insight

Modern financial systems must reduce friction for legitimate users while escalating security only when necessary.
This platform models how to achieve that balance at scale.

🔭 Future Enhancements
Integrate real ML anomaly detection models
Deploy backend on AWS (Lambda / API Gateway)
Add Kafka-style event streaming
Implement real IAM + OAuth flows
Introduce Terraform/CDK infrastructure
👨‍💻 Author

David Joseph
🔗 GitHub: https://github.com/david8474

⭐ Final Note

This project reflects real-world banking scenarios, combining:

Fraud detection
Customer experience optimization
Cloud-native thinking
DevSecOps + SRE principles


🔐 PROJECT 4 – FEDERAL MULTI-ENCLAVE INSIDER-THREAT & ANOMALY DETECTION SYSTEM
Overview

Enterprise-grade insider threat and anomaly detection platform designed for federal-style multi-enclave environments.
The system detects abnormal behavior from network telemetry and enforces automated containment and remediation.

Key Capabilities

Multi-enclave segmentation (Unclassified, Controlled, Restricted)

NetFlow-based anomaly detection

Automated quarantine and remediation

Zero Trust and least-privilege enforcement

CI/CD-validated infrastructure and security controls

Architecture Highlights

Network Segmentation: VRF-based enclave isolation

Detection: ML-driven anomaly analysis

Response: Ansible + NSO automated enforcement

Identity & Access: Cisco ISE TrustSec segmentation

Cloud: AWS & Azure (government-style configurations)

Automation & Security

Dynamic quarantine workflows

Infrastructure as Code (Terraform, Bicep)

Continuous security scanning (Trivy, Snyk)

Compliance aligned with NIST 800-53, FISMA, FedRAMP

📁 Repository Structure & Files (All Files Opened)
📄 README.md

Federal Multi-Enclave Insider-Threat & Anomaly Detection System

System Overview

This is a production-ready, enterprise-grade insider threat and anomaly detection system with automated remediation capabilities.

Architecture
High-Level System Architecture
graph TB
subgraph "Multi-Enclave Network"
VRF_GREEN[VRF-Green<br/>Unclassified]
VRF_YELLOW[VRF-Yellow<br/>Secret]
VRF_RED[VRF-Red<br/>Top Secret]

├── api/
├── soc/
├── compliance/
└── docs/

Automated Response Flow

Anomaly detected in NetFlow telemetry

Policy engine evaluates threat severity

Network controls updated dynamically

Quarantine service invoked via NSO

Remediation playbooks executed

Incident logged and reported

VRF-Green: Unclassified / Low Trust

VRF-Yellow: Controlled / Mission Systems

VRF-Red: High-Sensitivity / Restricted

📄 FINAL_AUDIT_REPORT.md

FINAL AUDIT & VERIFICATION REPORT

Federal Multi-Enclave Insider Threat Detection System

Audit Status: PASSED – READY FOR DEPLOYMENT

The system meets federal security requirements including NIST 800-53, FISMA, and FedRAMP standards.

Component Verification Matrix
Component	Status	Verification Method	Result
README.md	Confirmed	Comprehensive review	PASS
Zero Trust Design	Confirmed	NIST SP 800-207	PASS
CI/CD Workflow	Confirmed	GitHub Actions	PASS
Security Scanning	Confirmed	Trivy + Snyk	PASS
Audit Methodology

Static analysis of infrastructure definitions

Validation of network automation models

CI/CD workflow execution review

Security control mapping and verification

Risk Evaluation Summary

No critical architectural risks identified.
Medium risks addressed through sequencing controls and validation gates.

📄 DEPLOYMENT_GUIDE.md

Federal Insider Threat Detection System

Classification: UNCLASSIFIED
Version: 1.0.0

Technology Stack

Node.js 18+ (SOC Dashboard)

Python 3.9+ (ML Pipeline)

Ansible 2.10+ (Automation)

Logic Apps for SOAR

Network Security Configuration (Cisco ISE)

GUEST (10)

CONTRACTOR (20)

EMPLOYEE (30)

ADMIN (40)

QUARANTINE (99)

Environments

Development

Staging

Production

Change Control

All changes are validated through CI/CD prior to deployment.
Rollback paths exist for each deployment phase.

🏗️ infra/aws/main.tf
terraform {
  required_version = ">= 1.0"
}

backend "s3" {
  bucket = "federal-insider-threat-tfstate"
  encrypt = true
  kms_key_id = "alias/terraform-state"
}

resource "aws_s3_bucket_public_access_block" "netflow_raw" {
  block_public_acls = true
  block_public_policy = true
}

versioning {
  enabled = true
}

server_side_encryption_configuration {
  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "aws:kms"
    }
  }
}

cidr_block = "10.0.0.0/16"
enable_dns_hostnames = true

🏗️ infra/azure/main.bicep
@description('Azure Government deployment for Federal Insider Threat Detection System')

var commonTags = {
  Classification: 'UNCLASSIFIED'
  'NIST-800-53': 'AC-3,AU-2,SC-7,IR-4'
}

tags: {
  Classification: 'UNCLASSIFIED'
  Environment: 'Federal-Simulated'
}

publicNetworkAccess: 'Disabled'
kafkaEnabled: true

🌐 network/nso/packages/quarantine-service/src/yang/quarantine-service.yang
module quarantine-service {
  namespace "http://example.com/quarantine";
  prefix qs;

  container quarantine {
    description "Policy-driven quarantine service for isolating compromised assets.";

    leaf target-ip {
      type string;
    }

    leaf action {
      type enumeration {
        enum isolate;
        enum restore;
      }
    }
  }
}

📊 ml/scripts/generate_netflow_dataset.py
{
 'src_ip', 'dst_ip', 'src_port', 'dst_port', 'protocol',
 'bytes', 'packets', 'duration',
 'enclave', 'sgt', 'user_id', 'device_type',
 'is_anomaly', 'anomaly_type'
}

'anomaly_type': 'lateral_movement'
'enclave': random.choice(['GREEN', 'YELLOW', 'RED'])
'is_anomaly': True
'anomaly_type': 'privilege_escalation'

🔁 ml/pipeline/
pipeline/
├── ingest/
├── normalize/
├── enrich/
├── analyze/
├── alert/

🔐 .github/workflows/ci-cd.yml
name: Federal Insider Threat Detection - CI/CD Pipeline

- Ansible Lint
- Trivy vulnerability scanning
- SARIF upload
- Terraform Validate
- Bicep Build
- Trivy FS Scan
- Upload SARIF Results

📄 Cisco_ISE_REPRESENTATIVE.md

Cisco ISE Configuration (Representative Excerpt)

Security Group Tags (SGTs)

SGT 10 GUEST
SGT 20 CONTRACTOR
SGT 30 EMPLOYEE
SGT 40 ADMIN
SGT 99 QUARANTINE


Authorization Profiles

PERMIT_STANDARD_ACCESS
ADMIN_PRIVILEGED_ACCESS
QUARANTINE_ACCESS


TrustSec Matrix

EMPLOYEE → EMPLOYEE : ALLOW
EMPLOYEE → ADMIN : DENY
EMPLOYEE → QUARANTINE : DENY
ADMIN → ALL : ALLOW
QUARANTINE → ANY : DENY


Authorization Policy Logic

IF Device_Trust_State == "Compromised"
THEN Apply QUARANTINE_ACCESS


Compliance Mapping

AC-3 AC-6 AU-2 IR-4 SC-7


🛡️ PROJECT 5 – CSfC NETWORK OPERATIONS (TIER 2/3, PKI, STIG, IaC)
CSfC Network Operations Portfolio

This public repository contains sanitized, representative samples of a CSfC-aligned Network Operations & Engineering Support Platform.

Scope

CSfC / NIAP / DISA STIG-aligned operations

Tier 2 / Tier 3 incident response

PKI issuance, validation, revocation, compromise handling

Infrastructure as Code (Terraform / AWS CDK)

Compliance automation and audit readiness

What This Repository Is

A safe-to-share subset of a private platform

What This Repository Is Not

A production deployment

A complete implementation

A source of real credentials or IPs

Key Capabilities Demonstrated

Secure device baselines (Cisco IOS-XE, ASA)

Centralized logging and AAA

PKI failure response

Major outage response discipline

Audit scoring and RCA methodology

SECURITY NOTE – REDACTION & DISCLOSURE PHILOSOPHY

Removed or sanitized:

IPs, hostnames, domains

VPN peers, trustpoints

Certificates, private keys

Credentials and shared secrets

Internal runbook contacts

All sensitive fields replaced with REPLACE_ME_*.

📄 CSfC Network O&M Platform – Security Audit Report

Audit Date: [YYYY-MM-DD]
Auditor: [Name / Organization]
Audit Scope: Full platform security assessment
Report Version: 1.0

Executive Summary

This audit report provides a comprehensive security assessment of the CSfC Network O&M Platform, including verification of critical components, validation of security controls, identification of vulnerabilities, application of fixes, and recommendations for improvement.

Overall System Integrity Score: [XX/100]
Status: [PASS / PASS WITH CONDITIONS / FAIL]

Component Verification Matrix
Component	Purpose	Verified	Compliant	STIG Applied	Certificate Valid	Notes
Core Router 01	Routing	✅	✅	✅ V2R7	✅	
Core Switch 01	L3 Switching	✅	✅	✅	✅	
Firewall 01	Perimeter Control	✅	✅	✅	✅	
Final System Integrity Score

The System Integrity Score is calculated based on:

Component Verification (30%)

Security Controls (30%)

Compliance (20%)

Operational Readiness (20%)

📄 Cisco IOS-XE STIG Baseline (Representative Sample)
!
! Cisco IOS-XE STIG Baseline (Representative Sample)
!
crypto key generate rsa modulus 4096 label SSH-KEY

ip ssh version 2
ip ssh server algorithm encryption aes256-ctr aes192-ctr aes128-ctr
ip ssh server algorithm mac hmac-sha2-512 hmac-sha2-256
ip ssh server algorithm kex ecdh-sha2-nistp521 ecdh-sha2-nistp384 ecdh-sha2-nistp256
ip ssh server algorithm hostkey ecdsa-sha2-nistp521 ecdsa-sha2-nistp384 ecdsa-sha2-nistp256
no ip ssh server algorithm kex diffie-hellman-group1-sha1
ip ssh time-out 60
ip ssh authentication-retries 3
ip ssh logging events
!
logging buffered 64000 informational
logging console critical
logging monitor warnings
logging host REPLACE_ME_SYSLOG_SERVER transport tcp port 6514
logging host REPLACE_ME_SYSLOG_SERVER_BACKUP transport tcp port 6514
logging source-interface Loopback0
!
aaa new-model
tacacs server TACACS-SERVER-1
 address ipv4 REPLACE_ME_TACACS_SERVER_1
 key 7 REPLACE_ME_TACACS_KEY
tacacs server TACACS-SERVER-2
 address ipv4 REPLACE_ME_TACACS_SERVER_2
 key 7 REPLACE_ME_TACACS_KEY
aaa group server tacacs+ TACACS-GROUP
 server name TACACS-SERVER-1
 server name TACACS-SERVER-2
!
snmp-server group SECURE-GROUP v3 priv
snmp-server user SECURE-USER SECURE-GROUP v3 auth sha REPLACE_ME_AUTH priv aes 256 REPLACE_ME_PRIV
snmp-server host REPLACE_ME_SNMP_MANAGER version 3 priv SECURE-USER
!
line vty 0 4
 transport input ssh
 exec-timeout 10 0
 login authentication default
!

📄 Cisco ASA STIG Baseline (Representative Sample)
!
! Cisco ASA STIG Baseline (Representative Sample)
!
aaa-server TACACS-GROUP protocol tacacs+
aaa-server TACACS-GROUP (management) host REPLACE_ME_TACACS_SERVER_1
 key REPLACE_ME_TACACS_KEY
aaa-server TACACS-GROUP (management) host REPLACE_ME_TACACS_SERVER_2
 key REPLACE_ME_TACACS_KEY

aaa authentication ssh console TACACS-GROUP LOCAL
!
ssh version 2
ssh timeout 10
ssh REPLACE_ME_MGMT_NETWORK REPLACE_ME_MGMT_MASK management
ssh cipher encryption aes256-ctr aes192-ctr aes128-ctr
ssh cipher integrity hmac-sha2-512 hmac-sha2-256
ssh cipher kex ecdh-sha2-nistp521 ecdh-sha2-nistp384 ecdh-sha2-nistp256
!
logging enable
logging timestamp
logging buffer-size 65536
logging buffered informational
logging trap informational
logging host management REPLACE_ME_SYSLOG_SERVER tcp/6514
logging host management REPLACE_ME_SYSLOG_SERVER_BACKUP tcp/6514
!
policy-map global_policy
 class inspection_default
  inspect dns preset_dns_map
  inspect ftp
  inspect icmp
!
threat-detection basic-threat
threat-detection statistics access-list
threat-detection statistics tcp-intercept rate-interval 30 burst-rate 400 average-rate 200
!

📘 Runbook: Major Network Outage Response

Severity: CRITICAL
Response Time: 5 minutes

Overview

Response procedures for outages affecting more than 50% of users or critical infrastructure.

Indicators

Multiple simultaneous alerts

Loss of connectivity to critical segments

SIEM correlation events

Multiple user reports

Investigation Phase

Confirm scope and impact

Identify last-known-good state

Collect logs from core devices, firewalls, VPN gateways

Determine configuration vs hardware vs security root cause

Initial Notification

Subject: CRITICAL: Major Network Outage – Incident #[ID]
Impact: [Description]
Start Time: [UTC]
Status: INVESTIGATING

📘 Runbook: PKI Infrastructure Failure

Severity: HIGH to CRITICAL
Response Time: 15 minutes

Covered Scenarios

CA service failure

Expired certificates

CRL / OCSP outages

Validation failures

Compromise events

Compromise Response

Isolate CA infrastructure

Preserve logs and evidence

Revoke affected certificates

Publish emergency CRL

Activate backup CA per policy

📘 Post-Incident Root Cause Analysis (RCA)

Incident ID: [YYYY-MM-DD-NNN]
Author: [Name]

Executive Summary

What Happened:

Impact:

Resolution:

Five Whys

Why did the outage occur?

Why did that happen?

Why did that happen?

Why did that happen?

Root Cause:

Corrective Actions
Action	Owner	Due Date	Verification	Status


🏥 PROJECT 6 – SECURE HEALTHCARE CLOUD DATA PLATFORM (IaC, AIRFLOW, IAM, DATA GOVERNANCE)

This repository contains sanitized, representative examples of a secure cloud-native data platform. It demonstrates: - Infrastructure as Code (Terraform) - Production-grade Airflow pipelines with SLA handling - Least-privilege IAM design - Data masking and governance patterns - Containerized local development workflows ⚠️ No real credentials, datasets, or customer information are included. ## Architecture Overview - AWS-based infrastructure provisioned via Terraform - Apache Airflow orchestrating data pipelines - Security controls aligned with healthcare / regulated environments - Local development via Docker Compose ## Key Skills Demonstrated - Terraform (modular IaC) - Airflow DAG design & operations - Cloud security & compliance - DevOps best practices

📂 terraform/
📄 terraform/README.md

md Copy code

Terraform Infrastructure (Example) This folder contains representative Terraform configuration for a secure data platform. ## Components - VPC and networking (abstracted) - Managed database resources - IAM roles following least-privilege - Outputs suitable for downstream automation All identifiers, ARNs, and account details are placeholders.
1️⃣ Terraform – Infrastructure (IAM first)
📄 terraform/versions.tf
terraform {
  required_version = ">= 1.5.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

📄 terraform/variables.tf
variable "region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "environment" {
  description = "Deployment environment"
  type        = string
  default     = "dev"
}

📄 terraform/main.tf
provider "aws" {
  region = var.region
}

resource "aws_iam_role" "airflow_execution_role" {
  name = "airflow-execution-${var.environment}"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect = "Allow"
      Principal = {
        Service = "ecs-tasks.amazonaws.com"
      }
      Action = "sts:AssumeRole"
    }]
  })
}

📄 terraform/outputs.tf
output "airflow_execution_role_name" {
  description = "IAM role used by Airflow tasks"
  value       = aws_iam_role.airflow_execution_role.name
}

2️⃣ Docker Compose – Local Runtime (Airflow)
📄 docker-compose.example.yml
version: "3.9"

services:
  airflow:
    image: apache/airflow:2.8.0
    environment:
      AIRFLOW__CORE__LOAD_EXAMPLES: "false"
    ports:
      - "8080:8080"

3️⃣ Airflow – Core DAG Execution Logic
📄 airflow/dags/ehr_pipeline.example.py
from airflow import DAG
from airflow.operators.python import PythonOperator
from airflow.utils.dates import days_ago
from datetime import timedelta

def extract():
    print("Extracting example EHR data")

def transform():
    print("Transforming data")

def load():
    print("Loading data to analytics store")

default_args = {
    "owner": "data-platform",
    "retries": 2,
    "retry_delay": timedelta(minutes=5),
    "sla": timedelta(minutes=30),
}

with DAG(
    dag_id="ehr_pipeline_example",
    start_date=days_ago(1),
    schedule_interval="@daily",
    default_args=default_args,
    catchup=False,
) as dag:

    extract_task = PythonOperator(
        task_id="extract",
        python_callable=extract,
    )

    transform_task = PythonOperator(
        task_id="transform",
        python_callable=transform,
    )

    load_task = PythonOperator(
        task_id="load",
        python_callable=load,
    )

    extract_task >> transform_task >> load_task

📄 airflow/plugins/sla_callbacks.py
def sla_miss_callback(dag, task_list, blocking_task_list, slas, *args, **kwargs):
    """
    Called when an SLA is missed.
    In production, this would integrate with alerting systems.
    """
    print(f"SLA missed for DAG {dag.dag_id}")
    print(f"Tasks affected: {task_list}")

4️⃣ Security – IAM & Data Governance
📄 security/iam_policy_least_privilege.json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::example-data-bucket/*"
    }
  ]
}

📄 security/masking_policy.example.sql
CREATE MASKING POLICY mask_sensitive_string
AS (val STRING)
RETURNS STRING ->
CASE
  WHEN CURRENT_ROLE() IN ('SECURITY_ADMIN') THEN val
  ELSE '***MASKED***'
END;

Final Note 

This portfolio contains representative samples of my engineering work across networking, cloud, automation, and Kubernetes environments.
All sensitive files and full production implementations are kept private in bolt.new / windsurf / Codex for security reasons.
