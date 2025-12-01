SRE Fundamentals – Hands-On Labs

This repository contains my hands-on labs for SRE (Site Reliability Engineering) Fundamentals.
Each lab focuses on a core SRE skill such as observability, monitoring, alerting, automation, IaC, cloud infrastructure, and reliability metrics.

Note: Always run Lab 0 before doing anything else.

📘 Overview of Labs & Activities

Below is a detailed explanation of every lab and activity included in the SRE-Fundamentals-main folder.

## 🧪 Lab 0 – Setting Up

This introductory lab prepares the environment needed for the other labs.

What you do:

Install required CLI tools (AWS CLI, kubectl, Terraform, Docker, etc.)

Configure IAM roles / credentials

Set up your working environment

Validate access to cloud resources

Verify monitoring/observability prerequisites

This ensures all subsequent hands-on exercises run smoothly.

## 📊 Lab 1 – SLI and SLO with Prometheus

This lab introduces Service Level Indicators (SLIs) and Service Level Objectives (SLOs)—core reliability concepts in SRE.

You will:

Deploy Prometheus

Collect service metrics

Define SLIs (e.g., latency, error rate, throughput)

Calculate SLOs

Observe how reliability is measured in real time

## 📈 Lab 2 – Exploring Metric Types

This lab focuses on understanding how metrics are structured and used in monitoring systems.

You will learn:

Counter metrics

Gauge metrics

Histogram metrics

Summary metrics

How to interpret them in dashboards

When to use each type in production environments

## 📡 Lab 3 – Monitoring, Logging & Alerting

This lab covers the three pillars of observability:

Monitoring

Collecting performance and system metrics

Understanding data trends

Logging

Structured logs

Application + system logs

Log querying basics

Alerting

Defining alert rules

Detecting anomalies

Understanding alert thresholds

You learn how monitoring + logs + alerts combine to improve service reliability.

## 📊 Lab 4 – Setting Up a CloudWatch Alarm

This is an AWS-specific observability lab.

You will:

Create CloudWatch metrics

Configure CloudWatch alarms

Set thresholds

Trigger notifications

Validate that alarms fire correctly

You learn how cloud-native monitoring works.

## 📊 Lab 5 – Creating a Grafana Dashboard

This lab focuses on data visualization for SRE.

You will:

Deploy Grafana

Connect Prometheus as a data source

Build custom dashboards

Visualize latency, traffic, error rate, and saturation

Create panels, charts, and alerting rules

By the end, you have a production-style Grafana setup.

## ⚙️ Lab 7 – Autoscaling for Reliable Systems

This lab teaches scalability, one of the foundations of reliability.

You will:

Configure autoscaling rules

Understand scaling triggers

Use AWS Autoscaling Groups or Kubernetes Horizontal Pod Autoscaler

Simulate load

Watch the system scale dynamically

A realistic demonstration of how systems handle growing traffic.

## 🏗️ Lab 8 – Infrastructure as Code with AWS

This lab introduces automation using IaC tools like Terraform or CloudFormation.

You will:

Create AWS resources programmatically

Reproduce environments reliably

Use version-controlled IaC

Deploy infrastructure at scale

Destroy and rebuild environments with one command

This lab shows why IaC is essential for modern SRE.

## ⚠️ Extra Lab – Adding Alerts in Email & Slack

An additional drilled-down lab for alerting:

You will:

Integrate alert notifications with Slack

Configure email alerts

Test failures to generate notifications

Build escalation workflows

This lab focuses heavily on real-world incident handling.

## 🐳 Extra Lab – Playing with Docker

A foundational lab to ensure container fluency.

You will:

Build Docker images

Run, inspect, stop & remove containers

Use Docker Compose

Understand container logs and networking

Prepares you for Kubernetes and cloud-native orchestration.

## 📝 Activities (Case Studies & Guided Work)

These activities are more theoretical and conceptual, guiding you through SRE practices.

Activity 1 – SLI and SLO Case Study

A deep-dive case study on defining reliability metrics for real-world services.

You will:

Create SLIs

Define SLOs

Understand error budgets

Apply SRE thinking to business scenarios

Guided Activity 1 – Manual VPC Creation

A step-by-step introduction to building infrastructure manually before using IaC.

You will:

Create VPC

Subnets

Route tables

Gateways

Security groups

Helps you understand cloud networking fundamentals.

Guided Activity 2 – CloudFormation Setup

This activity teaches cloud-native IaC using AWS CloudFormation.

You will:

Write CloudFormation templates

Deploy them

Validate results

Understand declarative deployments

A core SRE automation skill.

📂 Repository Structure
SRE-Fundamentals/
│
├── Lab 0_ Setting Up.md
├── Lab 1_ SLI and SLO with Prometheus.md
├── Lab 2_ Exploring Metric Types.md
├── Lab 3_ Monitoring, Logging, and Alerting.md
├── Lab 4_ Setting Up a CloudWatch Alarm.md
├── Lab 5_ Creating a Grafana Dashboard.md
├── Lab 7_ Autoscaling for reliable sys....md
├── Lab 8_ Infrastructure as Code with AWS.md
│
├── Activity 1_ SLI and SLO Case Study.md
├── Guided Activity 1_ Manual VPC Creation.md
├── Guided Activity 2_ CloudFormation Setup.md
│
├── Extra Lab_ Adding alerts in email and slack.md
├── Extra Lab_ Playing with Docker.md
└── README.md

✔️ How to Use This Repository

Start with Lab 0

Follow labs in order

Use the images/ folder for screenshots

Push updates to keep your learning organized

