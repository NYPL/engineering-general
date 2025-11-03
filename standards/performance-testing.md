# Performance Testing

A high-level approach for broad applicability across NYPL web services


## Table of Contents

- [Overview](#overview)
- [Goal](#goal)
- [Tools](#tools-summary)
- [Process](#process)
    1. [Test Planning](#test-planning)
    2. [Environment Setup](#environment-setup)
    3. [Test Design](#test-design)
    4. [Test Execution](#test-execution)
    5. [Data Collection and Analysis](#data-collection-and-analysis)
    6. [Reporting](#reporting)
- [Key Performance Indicators (KPIs)](#key-performance-indicators-kpis)
    - [Load Testing](#load-testing-kpis)
    - [Core Web Vitals](#core-web-vitals-kpis)
- [KPI Thresholds](#kpi-thresholds)
    - [Response Time](#response-time)
    - [Error Rate](#error-rate)
    - [Throughput](#throughput)
    - [Concurrent Users](#concurrent-users)
- [Analysis & Reporting](#analysis--reporting)
- [Test Environment Details](#test-environment-details)
- [Cadence & Continuous Testing](#cadence--continuous-testing)

---

### Overview
This guide outlines the QA team's strategy and approach to performance testing. It covers the end-to-end process, including planning, environment setup, test design, execution, data analysis, and reporting. It also defines key metrics and thresholds to evaluate system performance and provides recommendations for continuous monitoring and improvement.

### Goal
Ensure web services perform reliably and remain responsive under expected and peak usage conditions by identifying and addressing performance issues to support the delivery of consistent user satisfaction.

## Tools
| Tool                | Purpose & Usage |
|---------------------|-----------------------------------------------------------------------------------------|
| **Locust.io**       | Python-based load test scripting. Identify key user flows, create locustfiles, parameterize data, use helper methods, and assign task weights for realistic scenarios. |
| **LoadForge**       | Cloud-based load execution and reporting. Import locustfiles, run baseline and peak tests, analyze results in UI, and monitor trends. |
| **New Relic / AWS** | Monitor application and server-side metrics. Track resource utilization, identify bottlenecks, and correlate real-time data with test results. |
| **PageSpeed Insights** | Measure Web Vitals metrics. Run on key pages, track over time, and provide suggestions for improvement. |
| **Google Analytics**| Analyze user behavior to inform test cases and concurrency levels. Identify core flows and high-traffic pages. |

---



## Process

### 1. Test Planning
---
**Define Objectives:** Start by clearly defining the goals of the load testing. Stakeholders often provide general requests, so it's crucial to translate these into specific objectives.

**Understand the Application and Core User Flows:** Gain an understanding of the application's architecture, including its dependencies (databases, external APIs, etc.). Work with stakeholders to identify the most critical user flows. These are the sequences of actions a typical user takes within the application and will form the basis of designing effective test scenarios.

**Utilize Analytics Data:** Leverage existing analytics data (e.g from Google Analytics) to determine realistic user concurrencies to test against. This data helps with understanding typical user behavior patterns and page views to inform the design of test scenarios that accurately simulate live engagement, ensuring tests reflect real-world usage.

**Consider a Written Test Plan:** Such a document provides a clear understanding of the testing approach for the team and facilitates effective communication with stakeholders. See [MODv2 load test plan](https://docs.google.com/document/d/1Soc2vDXuMx0Ikf9f7G88P_RFGpp3deSwrOG4tqvqR-Q/edit?usp=sharing) for an example.

### 2. Environment Setup
---
**Dedicated Performance Test Environment (Ideal):** Ideally, conduct load tests in a dedicated performance test environment. This minimizes interference from other development or testing activities and ensures consistent, reliable results.

**Scaling QA Environments (Practical):** In practice, if a dedicated environment isn't available, scale up existing QA environments to mirror production resources. This ensures that the test environment's capabilities are consistent with the live system, providing more accurate performance insights.

**DevOps Communication and Coordination:** Maintain clear and constant communication with DevOps regarding environment consistency and any external dependencies. This ensures that the test environment is properly configured and that external services are available and performing as expected during testing. All environment-related requests should be made via Jira tickets to ensure proper tracking and accountability.

**Production Service Protection:** Ensure that performance test environments are configured in a way that they do not impact live production services (e.g., due to external dependencies).

### 3. Test Design
---
**Scenario Design and Weighing:** Design test scenarios based on the identified core user flows and weigh them reasonably, assigning higher importance to frequently performed actions to accurately reflect realistic user behavior.

**Define Load Profiles:** Establish different load profiles to evaluate the system's response under varying traffic levels. These typically include:
- **Baseline:** Represents user traffic during low usage periods.
- **Peak:** Simulates expected high levels of user traffic.
- **Maximum (or Stress):** Pushes the system to its breaking point to identify its absolute capacity.

**Create Test Scripts:** Develop test scripts (known as locustfiles) by defining tasks that represent user actions, setting appropriate wait times to mimic user pauses, handling necessary request headers, and managing large request payloads if applicable.

### 4. Test Execution
---
**Local Testing:** Before running large-scale, paid tests, perform local testing to debug and refine test scripts.

**Environment Configuration:** Add your testing environment as a host in the chosen load testing service (e.g., LoadForge). Ensure proper connectivity and address any external domain requirements. Note that nypl.org has been validated; others may require DevOps requests like [DOPS-725](https://newyorkpubliclibrary.atlassian.net/browse/DOPS-725).

**Parameter Definition:** Utilize the test editor to define critical test parameters, including the number of users, spawn rates, and load generators. Set accurate scoring targets to automatically determine the success or failure of a test run, but only if prior benchmark data exists.

### 5. Data Collection and Analysis
---
**Utilize Observability Tools:** Use observability tools for comprehensive data collection, such as New Relic for application-level monitoring and AWS CloudWatch for server-level metrics.

**Monitor Test Progress:** Continuously monitor the load testing service's monitoring page during test runs for real-time insights.

**Interpret Reports:** After test completion, interpret charts and graphs within reports, looking for performance degradation.

**Analyze Key Performance Indicators:** Analyze KPIs like median and P95 response times to understand application responsiveness under load.

**Export Results:** Export all test results and reports for historical tracking, long-term analysis, and sharing with stakeholders.

### 6. Reporting
---
**Generate Detailed Reports:** Generate concise reports directly from reporting data, including metrics such as requests per second, average response times, and error rates.

**Communicate Test Results to Stakeholders:** Clearly communicate test results to stakeholders, creating documents or sheets with charts and aggregate metrics for each load profile.

**Version Control:** Commit test script(s) and other relevant files to the GitHub repository for the application under test, including a README for instructions and links to past test runs
- Example: https://github.com/NYPL/de-visualization/tree/main/locust

---

## Key Performance Indicators (KPIs)


### Load Testing

- Response Time
- Throughput
- Error Rate
- Concurrent Users


### Core Web Vitals

- First Contentful Paint (FCP)
- Largest Contentful Paint (LCP)
- Total Blocking Time (TBT)
- Cumulative Layout Shift (CLS)
- Speed Index (SI)
- Time to First Byte (TTFB)

*Note that traditional performance testing metrics (e.g. response time) and Core Web Vitals are entirely different sets of data that are used for different purposes. An API, for example, can be load tested, but an API typically has no UI and therefore cannot be measured using Core Web Vitals.*

---

## KPI Thresholds

To ensure consistent and reliable performance testing outcomes, it is essential to define clear thresholds for Key Performance Indicators (KPIs). These thresholds set the criteria for what is considered an acceptable performance level and provide a benchmark for evaluating whether a system meets the required standards under various conditions.

The thresholds defined below can be used as a starting point but can vary depending on the service being tested and whether there’s historical performance data to reference


### Response Time
- **Definition:** Time for server to respond to a request.
- **Thresholds:**
    - **Baseline:** ≤ 2s for 95% of requests
    - **Peak:** ≤ 3s for 95% of requests
    - **Stress:** Monitor for degradation as system approaches limits

### Error Rate
- **Definition:** Percentage of requests resulting in errors.
- **Thresholds:**
    - **Baseline:** 0%
    - **Peak:** < 1%
    - **Stress:** Identify max concurrency before error rate is unacceptable (e.g., 5%)

### Throughput
- **Definition:** Requests processed per second.
- **Thresholds:**
    - **Baseline:** ≥ 10 RPS
    - **Peak:** ≥ 250 RPS
    - **Stress:** Monitor decline as system reaches limits

### Concurrent Users
- **Definition:** Simultaneous users interacting with the system.
- **Thresholds:**
    - **Baseline:** Typical usage under normal conditions (10 users)
    - **Peak:** Expected high-usage periods (200 users)
    - **Stress:** Test volumes exceeding peak usage to find breaking point (1000 users)

---

## Analysis & Reporting

- Compare test results to benchmarks; pass if equal or better, fail if worse.
- Associate reports with Jira tickets; use docs for large scopes, comments for small tests.
- LoadForge retains reports for 2 years but it is recommended to export test results (e.g. to Google Drive or GitHub) for backup.
- Choose reporting format (structured or freeform) based on test scope.

---

## Test Environment Details

Record specs for the performance test environment (keep constant across tests or document per test run). For example, when load testing Collections API, info on both the API and its Solr datasource is documented:
  - **Collections API ECS Instances**
    - ECS Cluster: collections-api-qa; URL: https://qa-api-collections.nypl.org
    - Application: Python
    - Instance type: m5.large (2 CPU; 8G RAM; up to 10Gbps network bandwidth)
    - No. of instances: 6
    - Tasks: 24
  - **Solr 8 Instances**
    - EC2 Name: dev:DAM:SOLR8; URL: https://dev-solr8.nypl.org
    - Application: Java-based
    - Instance type: m6i.2xlarge (4 CPU; 32G RAM; up to 10Gbps network bandwidth)
    - No. of instances: 3
    - JVM Heap: 6G


---

## Cadence & Continuous Testing

- Run performance tests as part of regression testing releases.
- If regression detected, raise a bug and review with stakeholders.
- Schedule or trigger tests for frequent performance monitoring.
- Output test artifacts in GitHub (see [Google Sheet](https://github.com/marketplace/actions/gsheet-action)).
