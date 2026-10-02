# 🚨 Enterprise Production Observability & Incident Response Pipeline

[![AWS](https://img.shields.io/badge/AWS-CloudWatch%20%7C%20Alarms%20%7C%20SNS%20%7C%20SQS-orange?logo=amazon-aws)](https://aws.amazon.com/)
[![LocalStack](https://img.shields.io/badge/Emulation-LocalStack%203.8-blue?logo=docker)](https://localstack.cloud/)
[![Observability](https://img.shields.io/badge/SRE-Monitoring%20%26%20Incident%20Response-red)](https://aws.amazon.com/cloudwatch/)
[![Docker](https://img.shields.io/badge/Container-Docker%20Desktop-2496ED?logo=docker)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An enterprise-grade cloud telemetry, monitoring, and automated incident response architecture. Built using **Amazon CloudWatch Logs**, **Metric Filters**, **CloudWatch Alarms**, **Amazon SNS**, and **Amazon SQS** to detect production application failures in real-time and trigger automated incident escalation workflows.

---

## 🏛️ Architecture Topology

```mermaid
flowchart LR
    App["🖥️ Production Application"] -->|1. Stream Log Events| CW_Logs["📜 CloudWatch Logs<br><i>/production/core-banking-api</i>"]
    CW_Logs -->|2. Metric Filter: Count HTTP 500s| CW_Metric["📈 CloudWatch Metric<br><i>BankingApiErrorCount</i>"]
    CW_Metric -->|3. Error Threshold > 3 breached| CW_Alarm["🚨 CloudWatch Alarm<br><i>Critical-API-Failure-Alarm</i>"]
    CW_Alarm -->|4. Trigger Incident Notification| SNS["📢 Amazon SNS Topic<br><i>sre-incident-alerts</i>"]
    SNS -->|5. Queue Incident Ticket| SQS["📬 SQS Queue<br><i>oncall-incident-ticket-queue</i>"]
    SNS --> Email["📧 On-Call Engineer Pager"]
