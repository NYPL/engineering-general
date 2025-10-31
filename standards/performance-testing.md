# Performance Testing

**_High-level Approach_**
<br>
<span style="color: #888; font-style: italic;">For broad applicability across NYPL web services</span>


## Table of Contents

- [Overview](#overview)
- [Goal](#goal)
- [Tools](#tools-summary)
- [Process](#process)
    - [Test Planning](#test-planning)
    - [Environment Setup](#environment-setup)
    - [Test Design](#test-design)
    - [Test Execution](#test-execution)
    - [Data Collection and Analysis](#data-collection-and-analysis)
    - [Reporting](#reporting)
- [Key Performance Indicators (KPIs)](#key-performance-indicators-kpis)
    - [Load Testing KPIs](#load-testing-kpis)
    - [Core Web Vitals KPIs](#core-web-vitals-kpis)
- [KPI Thresholds](#kpi-thresholds)
    - [Response Time](#response-time)
    - [Error Rate](#error-rate)
    - [Throughput](#throughput)
    - [Concurrent Users](#concurrent-users)
- [Monitoring & Reporting](#monitoring--reporting)
    - [Analysis & Reporting Details](#analysis--reporting-details)
- [Test Environment Details](#test-environment-details)
- [Cadence & Continuous Testing](#cadence--continuous-testing)

---

### Overview
This document outlines the QA team's approach to performance testing for web projects. The strategy is intentionally generic for broad applicability.

### Goal
Ensure web applications meet performance criteria under expected load and stress, supporting user satisfaction.

---

## Tools

| Tool                | Purpose & Usage Highlights                                                                 |
|---------------------|-----------------------------------------------------------------------------------------|
| **Locust.io**       | Python-based load test scripting. Identify key user flows, create locustfiles, parameterize data, use helper methods, and assign task weights for realistic scenarios. |
| **LoadForge**       | Cloud-based load execution and reporting. Import locustfiles, run baseline and peak tests, analyze results in UI, and monitor trends. |
| **New Relic / AWS** | Server-side and Core Web Vitals monitoring. Integrate with app, track CPU/memory/db, use CloudWatch, and correlate with load results. |
| **PageSpeed Insights** | Measure Core Web Vitals (FCP, LCP, TBT, CLS). Run on key pages, track over time, and create Jira tickets for improvements. |
| **Google Analytics**| Analyze user behavior to inform test cases and concurrency levels. Identify core flows and high-traffic pages. |

---



## Process

### Test Planning
**Define Objectives:** Start by clearly defining the goals of the load testing. Stakeholders often provide general requests, so it's crucial to translate these into specific objectives.

**Understand the Application and Core User Flows:** Gain an understanding of the application's architecture, including its dependencies (databases, external APIs, etc.). Work with stakeholders to identify the most critical user flows. These are the sequences of actions a typical user takes within the application and will form the basis of designing effective test scenarios.

**Utilize Analytics Data:** Leverage existing analytics data (e.g., from Adobe Analytics or Google Analytics) to determine realistic user concurrencies. This data helps with understanding typical user behavior patterns and page views to inform the design of test scenarios that accurately simulate live engagement, ensuring tests reflect real-world usage.

**Consider a Written Test Plan:** Such a document provides a clear understanding of the testing approach for the team and facilitates effective communication with stakeholders. See MODv2 load test plan for an example.

### Environment Setup
**Dedicated Performance Test Environment (Ideal):** Ideally, conduct load tests in a dedicated performance test environment. This minimizes interference from other development or testing activities and ensures consistent, reliable results.

**Scaling QA Environments (Practical):** In practice, if a dedicated environment isn't available, scale up existing QA environments to mirror production resources. This ensures that the test environment's capabilities are consistent with the live system, providing more accurate performance insights.

**DevOps Communication and Coordination:** Maintain clear and constant communication with DevOps regarding environment consistency and any external dependencies. This ensures that the test environment is properly configured and that external services are available and performing as expected during testing. All environment-related requests should be made via Jira tickets to ensure proper tracking and accountability.

### Test Design
**Scenario Design and Weighing:** Design test scenarios based on the identified core user flows and weigh them reasonably, assigning higher importance to frequently performed actions to accurately reflect realistic user behavior.

**Define Load Profiles:** Establish different load profiles to evaluate the system's response under varying traffic levels. These typically include:
- **Baseline:** Represents user traffic during low usage periods.
- **Peak:** Simulates expected high levels of user traffic.
- **Maximum (or Stress):** Pushes the system to its breaking point to identify its absolute capacity.

**Create Test Scripts:** Develop test scripts (e.g., locustfiles) by defining user actions, setting appropriate wait times to mimic user pauses, handling necessary request headers, and managing large request payloads if applicable.

### Test Execution
**Local Testing:** Before running large-scale, paid tests, perform local testing to debug and refine test scripts.

**Environment Configuration:** Add your testing environment as a host in the chosen load testing service (e.g., LoadForge). Ensure proper connectivity and address any external domain requirements (e.g., nypl.org has been validated; others may require DevOps requests like DOPS-725).

**Parameter Definition:** Utilize the test editor to define critical test parameters, including the number of users, spawn rates, and load generators. Set accurate scoring targets to automatically determine the success or failure of a test run.

**Production Service Protection:** Ensure that performance test environments are configured in a way that they do not impact live production services (e.g., due to external dependencies).

### Data Collection and Analysis
**Utilize Observability Tools:** Use observability tools for comprehensive data collection, such as New Relic for application-level monitoring and AWS CloudWatch for server-level metrics.

**Monitor Test Progress:** Continuously monitor the load testing service's monitoring page during test runs for real-time insights.

**Interpret Reports:** After test completion, interpret charts and graphs within reports, looking for performance degradation.

**Analyze Key Performance Indicators:** Analyze KPIs like median and P95 response times to understand application responsiveness under load.

**Export Results:** Export all test results and reports for historical tracking, long-term analysis, and sharing with stakeholders.

### Reporting
**Generate Detailed Reports:** Generate concise reports directly from reporting data, including metrics such as requests per second, average response times, and error rates.

**Communicate Test Results to Stakeholders:** Clearly communicate test results to stakeholders, creating documents or sheets with charts and aggregate metrics for each load profile.

**Version Control:** Commit test script(s) and other relevant files to the GitHub repository for the application under test, including a README for instructions and links to past test runs.

Example: https://github.com/NYPL/de-visualization/tree/main/locust

---

## Key Performance Indicators (KPIs)


### Load Testing KPIs

- **Response Time**
- **Throughput** (transactions per second)
- **Error Rate**
- **Concurrent Users**


### Core Web Vitals KPIs

- **First Contentful Paint (FCP)**
- **Largest Contentful Paint (LCP)**
- **Total Blocking Time (TBT)**
- **Cumulative Layout Shift (CLS)**
- **Speed Index (SI)**
- **Time to First Byte (TTFB)**

*PageSpeed Insights provides suggestions for improvement, which can be mapped to Jira tickets. Note: Core Web Vitals are for UI; APIs are measured only by load testing metrics.*

---

## KPI Thresholds

To ensure consistent and reliable performance testing outcomes, it is essential to define clear thresholds for Key Performance Indicators (KPIs). These thresholds set the criteria for what is considered an acceptable performance level and provide a benchmark for evaluating whether a system meets the required standards under various conditions.

The thresholds defined below can be used as a starting point but can vary depending on the type of service being tested and whether there’s historical performance data to reference


### Response Time
- **Definition:** Time for server to respond to a request.
- **Thresholds:**
    - **Standard Load:** ≤ 2s for 95% of requests (≤ 500 users)
    - **High Load:** ≤ 3s for 95% of requests (≤ 1000 users)
    - **Stress:** Monitor for degradation as system approaches limits

### Error Rate
- **Definition:** Percentage of requests resulting in errors.
- **Thresholds:**
    - **Standard Load:** < 0.5% (≤ 500 users)
    - **High Load:** < 1% (≤ 1000 users)
    - **Stress:** Identify max concurrency before error rate is unacceptable (e.g., 5%)

### Throughput
- **Definition:** Requests processed per second.
- **Thresholds:**
    - **Standard Load:** ≥ 50 TPS (≤ 500 users)
    - **High Load:** ≥ 30 TPS (≤ 1000 users)
    - **Stress:** Monitor decline as system reaches limits

### Concurrent Users
- **Definition:** Simultaneous users interacting with the system.
- **Thresholds:**
    - **Baseline:** Acceptable performance at 500 users
    - **Peak:** Up to 1000 users while meeting other thresholds
    - **Stress:** Test up to 5000 users to find degradation point

---

## Monitoring & Reporting

- **Regular Monitoring:** Ensure performance does not degrade over time or after releases.
- **Reporting:** Document and share results, highlight metric deviations, and propose remediation actions.

### Analysis & Reporting Details

- Compare test results to benchmarks; pass if equal or better, fail if worse.
- Associate reports with Jira tickets; use docs for large scopes, comments for small tests.
- Record server specs for test environment (keep constant across tests):
    - Name: nyplorg-data-archives-production
    - Tasks: 2 (1 per EC2 instance)
    - EC2 Type: t3.medium (2 CPU, 4GB RAM, 5G Network)
    - Soft Memory Limit: 512MB
- Retain reports for at least 2 years; export to Google Drive or GitHub for backup.
- Choose report format (structured or freeform) based on test scope.

---

## Test Environment Details

- Use servers mirroring production resources and data for accurate results.
- Prefer dedicated QA or new environments to avoid blocking functional testing.
- Coordinate with DevOps to spin up or upscale environments as needed.
- Avoid impacting production by stress testing environments with production integrations (e.g., image server, database).

---

## Cadence & Continuous Testing

- Run performance tests as part of regression (not minor) releases.
- If regression detected, raise a bug and review with stakeholders.
- Schedule or trigger tests for frequent performance monitoring (e.g., via GitHub Actions, JMeter, or PageSpeed API scripts).
- Output test artifacts to GitHub or [Google Sheet](https://github.com/marketplace/actions/gsheet-action) for analysis and reporting.
