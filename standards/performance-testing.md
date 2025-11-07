# Performance Testing

A high-level approach for broad applicability across NYPL web services

## Table of Contents

- [Overview](#overview)
- [Goal](#goal)
- [Tools](#tools)
- [Key Performance Indicators (KPIs)](#key-performance-indicators-kpis)
    - [Load Testing](#load-testing)
    - [Web Vitals](#web-vitals)
- [KPI Thresholds](#kpi-thresholds)
- [Load Testing Process](#load-testing-process)
    1. [Test Planning](#1-test-planning)
    2. [Environment Setup](#2-environment-setup)
    3. [Test Design](#3-test-design)
    4. [Test Execution](#4-test-execution)
    5. [Analysis & Data Collection](#5-analysis--data-collection)
    6. [Reporting](#6-reporting)
- [Cadence & Continuous Testing](#cadence--continuous-testing)

---

### Overview
This guide outlines the QA team's strategy and approach to performance testing. It covers the end-to-end process, including planning, environment setup, test design, execution, data analysis, and reporting. It also defines key metrics and thresholds to evaluate system performance and provides recommendations for continuous monitoring and improvement.

### Goal
Ensure web services perform reliably and remain responsive under expected and peak usage conditions by identifying and addressing performance issues to support the delivery of consistent user satisfaction.

## Tools
| Tool                | Purpose & Usage |
|---------------------|-----------------------------------------------------------------------------------------|
| **Locust**       | Open source load test framework for simulating user behavior with Python code. |
| **LoadForge**       | Cloud-based load test service for running Locust tests for realistic simulation of live traffic. Offers detailed reports, test scheduling, CI/CD capabilities, live performance monitoring, and other useful features.
| **New Relic / AWS** | Monitor application performance and server-side metrics. Track resource utilization during tests, identify bottlenecks, and correlate real-time data with test results. |
| **PageSpeed Insights** | Measure Web Vitals metrics. Run on key pages, track over time, and obtain suggestions for improvement. |
| **Google Analytics**| Leverage user engagement data to identify core flows, high-traffic pages, and user concurrency thresholds. |

---

## Key Performance Indicators (KPIs)


### Load Testing
Locust measures typical performance metrics (see [LoadForge documentation](https://docs.loadforge.com/runs/run-results)).
- Response time
    - Median
    - Average
    - P95 (and other percentiles)
    - Max
    - Min
- Throughput
- Error rate
- Concurrent users

### Web Vitals
Higher-level metrics intended to measure UX of front-end applications (defined at [web.dev](https://web.dev/articles/vitals)).
- First Contentful Paint (FCP)
- Largest Contentful Paint (LCP)
- Total Blocking Time (TBT)
- Cumulative Layout Shift (CLS)
- Speed Index (SI)
- Time to First Byte (TTFB)

Web Vitals metrics for a particular web page can be accessed from the CrUX report using [pagespeed.web.dev](https://pagespeed.web.dev/), which provides realtime data aggregated over a 28 day period.

For obtaining specific measurements rather than aggregated field data, tests can be conducted using the [PageSpeed API](https://developers.google.com/speed/docs/insights/v5/get-started) to measure a page's Web Vitals at any given time. Measurements in that fashion are referred to as lab data, which is especially useful when evaluating performance in test environments prior to production (as the live users don't interact with our test environments, so realtime data from the CrUX report is either non-existent or unreliable.

> [!IMPORTANT]
>Traditional performance testing metrics and Web Vitals are entirely different sets of data. Metrics like response time, error rate and throughput can be measured for any web service with load testing while Web Vitals are for front-end applications only and not intended for evaluating performance at varying levels of traffic.

## KPI Thresholds

For untested systems, requesting input from stakeholders in order to define thresholds for KPIs such as response time and error rate is highly recommended, as these set the criteria for what is considered an acceptable performance level and provide a benchmark for evaluating whether a system meets the required standards under various conditions.

The thresholds defined below can be used as a starting point when lacking historical data but note that they can vary greatly depending on the type of system under test.

### Response Time
- **Definition:** Time for server to respond to a request.
- **Sample Thresholds:**
    - <ins>Baseline</ins>: ≤ 2s for 95% of requests
    - <ins>Peak</ins>: ≤ 3s for 95% of requests
    - <ins>Stress</ins>: Monitor for degradation as system approaches limits

### Error Rate
- **Definition:** Percentage of requests resulting in errors.
- **Thresholds:**
    - <ins>Baseline:</ins> 0%
    - <ins>Peak:</ins> < 1%
    - <ins>Stress:</ins> Identify max concurrency before error rate is unacceptable (e.g., 5%)

### Throughput
- **Definition:** Requests processed per second.
- **Thresholds:**
    - <ins>Baseline:</ins> ≥ 10 RPS
    - <ins>Peak:</ins> ≥ 250 RPS
    - <ins>Stress:</ins> Monitor decline as system reaches limits

## Load Testing Process

### 1. Test Planning
---

#### **Define Objectives**
Begin by explicitly defining the goals of the load testing. While stakeholders may present general requests, it is the tester’s responsibility to translate them into clear, actionable objectives that guide the testing process ensure alignment with project needs.

> [!TIP]
> For untested systems, it is strongly advised to set the following goals in addition to stakeholder requests:
>
> 🎯 <ins>Benchmarking</ins>: Establish baseline performance; a set metrics to target or improve upon.
>
> ⚙️ <ins>Process and infrastructure</ins>: Create a framework for sustainable performance testing of the system.
>
> 🤝 <ins>Knowledge sharing</ins>: Provide guidance that empowers team members to run future tests with confidence.
>
> 📝 <ins>Documentation</ins>: Document performance data, process, and other key information.
#### **Understand the System Under Test**
##### **System Architecture**
Communicate with developers familiar with the system to gain insights into its architecture. This understanding is essential for accurately modeling user behavior and writing test scripts properly.

Questions to consider include:
- What is the technology stack that this system is built on?
- Are there any external dependencies? If so, do they have their own test environments?
- What types of requests are involved with processing user interactions?
- Is it a single page application?
- Are there known performance issues or bottlenecks?
- Are there recent or upcoming changes that could affect performance?

##### **User Engagement**
Collaborate with the product team and stakeholders to identify the most important user flows, endpoints, and pages to target during testing. Prioritize these based on expected usage frequency to ensure test scenarios focus on areas most critical to user experience and system performance.

##### **Analytics Data**
Leverage existing analytics data (e.g from Google Analytics) to determine realistic user concurrencies to test against. This data helps with understanding typical usage patterns and page views to inform the design of test scenarios that accurately simulate live engagement, ensuring tests reflect real-world usage.

##### **Exploratory Testing**
If a web application, engage with it by performing common user actions and navigating to frequently accessed pages while the Network tab of the browser's developer tools is open. This allows the tester to see the web request(s) involved with particular actions, and scripting the tests requires accurate replication of those requests and any associated payloads (e.g. if a form submission involves a POST request).

#### **Consider a Written Test Plan**
Such a document provides a clear understanding of the testing approach for the team and facilitates effective communication with stakeholders. See [MODv2 load test plan](https://docs.google.com/document/d/1Soc2vDXuMx0Ikf9f7G88P_RFGpp3deSwrOG4tqvqR-Q/edit?usp=sharing) for an example.

---
### 2. Environment Setup
---

#### **Dedicated Performance Test Environment (Ideal)**
Conduct load tests in a dedicated performance test environment that mirrors the production configuration. This minimizes interference from other development or testing activities and ensures consistent, reliable results.

#### **Scaling QA Environments (Practical)**
If a dedicated environment isn't feasible or practical, scale up existing QA server(s) to mirror their production counterpart(s). This ensures that the test environment's capabilities are consistent with the live system, providing more accurate performance insights on actual user experience.

#### **Production Service Protection**
In some cases, a QA environment may be wired to a production dependency, so ensure performance test environments are configured in a way that guarantees a load test will not impact live production performance.

#### **Record Test Environment Configuration**
Clearly documenting the specifications of the performance test environment is essential.

Consistent environment configuration ensures that future tests are comparable and that observed performance changes can be attributed to code modifications rather than infrastructure differences. This minimizes variability across test iterations, enabling accurate assessment of the impact of code changes on system performance.

Examples:
- [Repo & Collections API Performance Testing](https://docs.google.com/document/d/1f2tndhxSpBz3wR7hWP6ZpI83_fg5NRE7U3vtAafAZxw/edit?usp=sharing)
- [FY25Q2: Digital Collections QA Infrastructure Updates for Performance Testing](https://docs.google.com/document/d/1XdF7tERouWCsPgkQOfCQdescNIC_HGZnMW9daGVQNXw/edit?usp=sharing)

#### **DevOps Coordination**
Maintain clear and constant communication with DevOps regarding environment consistency, external dependencies, testing timelines, etc. so that servers are properly configured and ready when needed.

All environment-related requests should be made via Jira tickets in the DOPS space _as early as possible_ to ensure proper planning, tracking, and accountability.

> [!WARNING]
> DOPS tickets require a target end date. When setting this field, keep their team's [sprint cadence](https://newyorkpubliclibrary.atlassian.net/jira/software/c/projects/DOPS/boards/14/backlog) in mind to avoid injecting sudden requests into their planned work.

For examples, see [DevOps requests for performance testing](https://newyorkpubliclibrary.atlassian.net/issues/?filter=12661).

---
### 3. Test Design
---
#### **Test Scenario Design**
Design test scenarios based on the identified core user flows and pages.

Ensure they're ranked in order of importance to ensure the most common actions are carried out more frequently to accurately reflect live traffic patterns. This ranking will inform proper weighing of test scenarios when scripting the test.

#### **Define Load Profiles**
Establish different load profiles to evaluate the system's response under varying traffic levels. Ramp-up periods (known as _spawn rates_ in Locust) and test run durations should also be included to ensure that test runs are carried out using the same parameters each time.

Load profiles to test should include the following parameters defined in the table below.

| Profile | Description | Concurrency | Duration | Spawn Rate |
| :--- | :--- | :---: | :---: | :---: |
| **Baseline** | User traffic during low or typical usage periods | 10 users | 10 min | 0.0333
| **Peak** | User traffic during known high-usage periods | 200 users | 15 min |
| **Stress (or max)** | Extreme level of user traffic to identify system capacity | 1000 users | 15 min |

> [!NOTE]
> The spawn rates listed above are set so that the first half of each test serves as a ramp-up period, gradually increasing concurrency, while the second half maintains a steady user load.
>
> This approach is standard practice, but ramp-up speed can be adjusted as needed—such as using a faster ramp-up for stress testing or a slower one for more gradual load increases.
>
> Calculation of the rate is determined dividing the number of users by the duration (in seconds).

#### **Test Script Creation**
Develop one or more test scripts (known as locustfiles) as needed, defining weighted tasks that each carry out the set of web requests associated with the actions for a given test scenario. Set appropriate wait times to mimic user pauses, handle necessary request headers, and manage request payloads if applicable (e.g. for POST requests).

Go to [locust.io](https://www.locust.io) for official documentation.

> [!TIP]
> LoadForge has a [browser recorder](https://docs.loadforge.com/test-scripts/record-your-browser that that may be used to capture the exact set of web requests involved in carrying out a set user actions.

---
### 4. Test Execution
---
#### **Local Testing**
Before running large-scale, paid tests with LoadForge, perform local testing to debug and refine test scripts.

This is done by installing the locust Python package then simply executing the command `locust` within a terminal while in a folder containing a file named locustfile.py. From there, navigating to [localhost:8089](http://localhost:8089) in a browser will provide a UI where a test can be run with the desired test parameters and results can be viewed along with the logging of any errors encountered.

#### **Environment Readiness**
Add the test environment as a host in LoadForge. Ensure proper connectivity and address any external domain requirements.

The host [nypl.org](https://www.nypl.org) is already validated, but if testing involves a domain outside of it (which is rare), validating will require a DevOps request similar to [DOPS-725](https://newyorkpubliclibrary.atlassian.net/browse/DOPS-725).

> [!CAUTION]
> If the test environment is behind the VPN and/or restricted to on-prem access only, then LoadForge tests cannot be run on it, as its load generators for simulating user traffic will be unable to reach the server. If this is the case, then the access restrictions in place must be lifted (at least temporarily) in order to run a test.
>
>For an example DevOps request in this case, see [DOPS-781](https://newyorkpubliclibrary.atlassian.net/browse/DOPS-781).

#### **Test Definition**
The recommended way to create a test in LoadForge is by utilizing the "Full Test Editor" to import a locustile and define the desired test parameters such as number of users, spawn rate, and location where traffic should originate from (New York is the most sensible option).

It is recommended to create one test per each load profile to avoid having to constantly edit a test in order to run against different user thresholds (e.g. baseline vs peak).

Optionally set scoring targets to automatically determine the success or failure of a test run, but this is recommended only if an adequate amount of historical performance data exists for setting reasonable targets.

> [!WARNING]
> LoadForge offers a features for quickly creating tests using a website crawler but it is not recommended for use because it bypass key steps earlier in the process necessary for accurately simulating live traffic to the system under test (particularly, the identification and proper weighting of core user actions and pages).
>
> If test scenarios are not designed or weighed properly to reflect expected usage of the live system, any obtained test results will not provide an accurate picture of its actual performance.
>
> On a short timeline, it is better to go with a simple test containing one task that simply requests the root of the site.

#### **Running Tests**
After confirming environment readiness, test script accuracy, and monitoring tools are active, the test is ready to run with LoadForge. The duration of the test run is set at the time of running a test in LoadForge, not in the test's definition itself.

Respective team members and DevOps should be notified of when a test run is to be taken place and ideally planned in advance. This can be done using the DevOps & Digital Release Calendar in our Google workspace calendar.

#### **Test Monitoring**
Actively monitor test runs using LoadForge's realtime reporting and any monitoring tools that have been set up to obtain real-time insights on system health. Note trends in KPIs and resource utilization as volume increases.

> [!WARNING]
> Be prepared to stop the test if critical issues arise (e.g. if an external production dependency was overlooked and performance degradation is raised)

#### **After Test Runs**
Communicate test completion, share any initial findings (e.g. high error rate), and continue coordination with DevOps for any required environment resets or troubleshooting that may be needed.

---
### 5. Analysis & Data Collection
---

#### **Interpret Reports**
After test completion, interpret charts and graphs within the LoadForge reports. Analyze KPIs like median and P95 response times (aggregate and per request) to understand application responsiveness under load. Note errors, if any, and identify the type of errors and which requests they occurred on.

Compare results to baseline metrics to determine how the system responds to higher traffic.

> [!TIP]
> The line chart that plots KPI measurements throughout a test run should be the starting point in determining how well the system performed during a test. Some key signs to look for when analyzing the test run chart from start to finish are given below.
>
> ✅ System performed well:
>    - Throughput and users maintain a 1-1 relationship
>    - Median response time flattens out and converges to a lower value
>
> 🔻 System performance degraded:
>    - Throughput flattens out or declines during or shortly after ramp-up period.
>    - Median response time and/or error rate increase and tail off to a higher value.

#### **Utilize Observability Tools**
Use observability tools to correlate realtime data with metrics collected from LoadForge test results. If errors or performance degredation are detected, use New Relic APM (if set up) to analyze logs for more information on errors and slow transaction traces to identify bottlenecks.

#### **Export Results (Recommended)**
Export test results and reports for historical tracking, long-term analysis, and sharing with stakeholders.

---
### 6. Reporting
---
#### **Create Report as Deliverable**
Create a report for documenting test results, recording KPIs and noting any deviations from baseline metrics or with prior results, if they exist. Ideally write in an analysis of the results, highlightng noteworthy findings and takeaways.

Select a reporting format that's appropriate to the test scope. Larger projects likely warrant a doc or sheet to track KPIs across multiple test iterations, while for smaller requests it's usually sufficient to report results by commenting on the associated Jira ticket.

Note the following examples:
- Long term project based reporting: [DC Facelift Performance Testing](https://docs.google.com/document/d/196-OdgspFEbvb5VXidIwc5Fa1lK-i9XkHdWhAEH4dKo/edit?usp=sharing)
- One-off request reporting: [DR-3289](https://newyorkpubliclibrary.atlassian.net/browse/DR-3289)

> [!CAUTION]
> LoadForge test run reports may be shared with anyone via public links but they expire after a week or so. They also contain a lot of information that may seem unclear and potentially mislead stakeholders if not supplemented with some guidance from the tester.

Thus only consider using a LoadForge report as a deliverable if on a very tight timeline.

#### **Communicate Test Results to Stakeholders**
Clearly communicate test results to stakeholders by delivering report(s) and ideally scheduling a meeting to review them.

The tester's role is to carry out the tests and present the findings effectively so that stakeholders can properly determine next steps (e.g. if a regression is detected for an upcoming release).

#### **Version Control**
Commit test script(s) and other relevant files to the GitHub repository for the system under test, ideally including a README for setup instructions and other information such as links to past test runs

Example: https://github.com/NYPL/de-visualization/tree/main/locust

---

## Cadence & Continuous Testing
Conducting performance testing on a regular schedule allows for effective monitoring and attribution of performance changes to specific code updates. This proactive approach enables early detection of regressions and helps maintain ongoing system reliability as a codebase evolves.

LoadForge provides a [scheduling feature](https://docs.loadforge.com/tests/scheduling#scheduling), enabling the automation of load testing at regular intervals. This enables consistent monitoring of system performance over time and helps quickly identify regressions or trends.

### CI/CD
Whether using Locust on its own or the [LoadForge API](https://docs.loadforge.com/api-reference/introduction), test runs can be triggered in CI/CD pipelines to support shift left initiatives.

To detect performance regressions during CI checks, a proven approach is to export key metrics from each test run as artifacts (such as a CSV) stored in the GitHub repository. Using tools like the [Google Sheet action](https://github.com/marketplace/actions/gsheet-action), a sheet can be automatically updated with the latest results, which enables comparison of current metrics against established benchmarks or previous test runs, helping to quickly identify regressions and track performance trends over time.
