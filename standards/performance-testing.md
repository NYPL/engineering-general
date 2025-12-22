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
| **[Locust](https://locust.io/)**       | Open source load test framework for simulating user behavior with Python code. |
| **[LoadForge](https://loadforge.com/)**       | Cloud-based load test service for running Locust tests with realistic and reliable simulation of live traffic. Offers detailed reports, test scheduling, CI/CD capabilities, live performance monitoring, and other useful features.
| **[New Relic](https://newrelic.com/)** / **[AWS](https://aws.amazon.com/)** | Monitor application performance and server-side metrics. Track resource utilization during tests, identify bottlenecks, and correlate real-time data with test results. |
| **[PageSpeed Insights](https://pagespeed.web.dev/)** | Measure Web Vitals metrics. Run on key pages, track over time, and obtain suggestions for improvement. |
| **[Google Analytics](https://marketingplatform.google.com/about/analytics/)**| Leverage user engagement data to identify core flows, high-traffic pages, and user concurrency thresholds. |

---

## Key Performance Indicators (KPIs)

### Load Testing
Locust measures typical performance metrics (see [LoadForge documentation](https://docs.loadforge.com/runs/run-results)).

⏱️&nbsp;&nbsp;**Response time**: Captured using multiple stats
  - Median
  - Average
  - P95 and other percentiles
  - Max
  - Min

🚀&nbsp;&nbsp;**Throughput**: Rate of incoming requests (measured in RPS)

🚫&nbsp;&nbsp;**Error rate**: Percentage of unsuccessful requests

👥&nbsp;&nbsp;**Concurrent users**: Number of simultaneous users engaging with the system

> [!TIP]
> Median response time is the most reliable single metric for comparing performance trends across multiple test runs, as it is less affected by outliers than averages or maximum values.

### Web Vitals
High-level Metrics developed by Google that quantify front-end application UX (defined at [web.dev](https://web.dev/articles/vitals)).

**Core Web Vitals**: The primary metrics for evaluating page experience, focusing specifically on how users perceive the speed and stability of a page.
  - Largest Contentful Paint (LCP)
  - Interaction to Next Paint (INP)
  - Cumulative Layout Shift (CLS)

**Other Web Vitals**: While the three metrics above are the primary indicators of a web app’s UX, they are backed by a broader set of supporting metrics that help diagnose why one or more Core Web Vitals may be underperforming.
  - First Contentful Paint (FCP)
  - Time to First Byte (TTFB)
  - Total Blocking Time (TBT)
  - Speed Index (SI)
  - Time to Interactive (TTI)

Note this latter set of metrics is ordered by role in the page load lifecycle.

#### Relationships
Because Web Vitals share many of the same underlying signals and scoring inputs with each other, changes to one metric often affect others. Improvements or regressions in a single metric can cascade across others.

Some relationships between the core set and the underlying ones include:
- A poor FCP score almost always leads to poor LCP.
- If TTFB is slow, FCP will be delayed by the same amount, thereby impacting LCP.
- TBT is the "lab"  equivalent of INP (see [lab data vs field data](https://web.dev/articles/lab-and-field-data-differences#lab_data_versus_field_data)). Improving TBT in a controlled lab environment is the most effective way to improve INP in the field.
- SI provides a holistic view of the "perceived" loading speed, whereas LCP only focuses on a single element.
- TTI has been deprioritized in favor of TBT and INP but it still remains a useful metric for understanding when a page is fully "settled" and usable.

#### Measuring Web Vitals
 A number of services offer access to Core Web Vitals for measurements of real-time (i.e. field) data:
- **PageSpeed Insights**: Provides [CrUX report](https://developer.chrome.com/docs/crux) data, aggregated over the last 28 days
- **LoadForge**: Performance monitoring features that include Core Web Vitals scores
- **New Relic Browser**: Collects data from actual users over the last 7 day period

PageSpeed Insights is the preferred tool for measuring Web Vitals. It is free to use, has an [API](https://developers.google.com/speed/docs/insights/v5/get-started) that can be used for automating lab measurements, and provides actionable suggestions for improving low scores. Tests can be run on demand against any URL, which is especially valuable in pre-production environments since they have little or no real user traffic (and thus limited field data), making lab measurements from PageSpeed Insights the primary way to evaluate and tune performance before release.

📜&nbsp;&nbsp;The script [runpagespeed.py](https://drive.google.com/file/d/152Qi3SOqvTgIgz5niuahPtyX9pADNVa1/view?usp=sharing) leverages the PageSpeed API and was used prior to major releases for Digital Collections.

> [!IMPORTANT]
> Traditional performance testing metrics and Web Vitals are entirely different sets of data. Metrics like response time, error rate and throughput can be measured for any web service with load testing while Web Vitals are for front-end applications only and not intended for evaluating performance at varying levels of traffic.

> [!NOTE]
> The following sections focus exclusively on load testing. Web Vitals and other front-end performance metrics are not covered in detail beyond this point.

## KPI Thresholds

For untested systems, requesting input from stakeholders in order to define thresholds for KPIs such as response time and error rate is highly recommended, as these set the criteria for what is considered an acceptable performance level and provide a benchmark for evaluating whether a system meets the required standards under various conditions.

The thresholds defined below can be used as a starting point when lacking historical data but note that they can vary greatly depending on the type of system under test.

### Response Time
- **Definition:** Time for server to respond to a request.
- **Example Thresholds:**
    - <ins>Baseline</ins>: ≤ 2s for 95% of requests
    - <ins>Peak</ins>: ≤ 3s for 95% of requests
    - <ins>Stress</ins>: Monitor for degradation as system approaches limits

### Error Rate
- **Definition:** Percentage of requests resulting in errors.
- **Example Thresholds:**
    - <ins>Baseline:</ins> 0%
    - <ins>Peak:</ins> < 1%
    - <ins>Stress:</ins> Identify max concurrency before error rate is unacceptable (e.g., 5%)

### Throughput
- **Definition:** Requests processed per second.
- **Example Thresholds:**
    - <ins>Baseline:</ins> ≥ 10 RPS
    - <ins>Peak:</ins> ≥ 250 RPS
    - <ins>Stress:</ins> Monitor decline as system reaches limits

## Load Testing Process

### 1. Test Planning
---

#### **Define Objectives**
Begin by explicitly defining the goals of the load testing. While stakeholders may present general requests, it is the tester’s responsibility to translate them into clear, actionable objectives that guide the testing process and ensure alignment with project needs.

> [!NOTE]
> For untested systems, it is strongly advised to set the following goals in addition to stakeholder requests:
>
> 🎯&nbsp;&nbsp;**Benchmarking**: Establish baseline performance; a set of metrics to target or improve upon.
>
> ⚙️&nbsp;&nbsp;**Process and infrastructure**: Create a framework for sustainable performance testing of the system.
>
> 🤝&nbsp;&nbsp;**Knowledge sharing**: Provide guidance that empowers team members to run future tests with confidence.
>
> 📝&nbsp;&nbsp;**Documentation**: Document performance data, process, and other key information.
#### **Understand the System Under Test**
##### **System Architecture**
Communicate with developers familiar with the system to gain insights into its design. This understanding is essential for accurately modeling user behavior and writing test scripts properly.

Questions to consider include:
- What is the technology stack that this system is built on?
- Are there any external dependencies? If so, do they have their own test environments?
- What types of requests are involved with processing user interactions?
- Is it a single page application?
- Are there known performance issues or bottlenecks?
- Are there recent or upcoming changes that could affect performance?
- Is authentication required to access the service? If so, what type?

##### **User Engagement**
Collaborate with the product team and stakeholders to identify the most important user flows, endpoints, and pages to target during testing. Prioritize these based on expected usage frequency to ensure test scenarios focus on areas most critical to user experience and system performance.

##### **Analytics Data**
Leverage existing analytics data (e.g from Google Analytics) to determine realistic user concurrencies to test against. This data helps with understanding typical usage patterns and page views to inform the design of test scenarios that accurately simulate live engagement, ensuring tests reflect real-world usage.

##### **Exploratory Testing**
If a web application, engage with it by performing common user actions and navigating to frequently accessed pages while the Network tab of the browser's developer tools is open. This allows the tester to see the web request(s) involved with particular actions; scripting test scenarios requires precise replication of those requests and any associated payloads (e.g. if a form submission involves a POST request).

#### **Consider a Written Test Plan**
Such a document provides a clear understanding of the testing approach for the team and facilitates effective communication with stakeholders. See [MODv2 load test plan](https://docs.google.com/document/d/1Soc2vDXuMx0Ikf9f7G88P_RFGpp3deSwrOG4tqvqR-Q/edit?usp=sharing) for an example.

---
### 2. Environment Setup
---

#### **Dedicated Performance Test Environment (Ideal)**
Conduct load tests in a dedicated performance test environment that mirrors the production configuration. This minimizes interference from other development or testing activities and ensures consistent, reliable results.

#### **Scaling QA Environments (Practical)**
If a dedicated environment isn't feasible or practical, scale up existing QA server(s) to mirror their production counterpart(s). This ensures that the test environment's capabilities are consistent with the live system, providing more accurate performance insights on actual user experience.

> [!IMPORTANT]
> Scaling up infrastructure results in increased costs. Unless continuous testing is planned, the test environment should be scaled back down and returned to its original configuration upon completion of testing.

> [!WARNING]
> In some cases, a QA environment may be wired to a production dependency, so ensure performance test environments are configured in a way that guarantees a load test will not impact live production performance.

#### **Record Test Environment Configuration**
Clearly documenting the specifications of the performance test environment is highly recommended.

Consistent environment configuration ensures that future tests are comparable and that observed performance changes can be attributed to code modifications rather than infrastructure differences. This minimizes variability across test iterations, enabling accurate assessment of the impact of code changes on system performance.

Examples:
- [Repo & Collections API Performance Testing](https://docs.google.com/document/d/1f2tndhxSpBz3wR7hWP6ZpI83_fg5NRE7U3vtAafAZxw/edit?usp=sharing)
- [FY25Q2: Digital Collections QA Infrastructure Updates for Performance Testing](https://docs.google.com/document/d/1XdF7tERouWCsPgkQOfCQdescNIC_HGZnMW9daGVQNXw/edit?usp=sharing)

#### **DevOps Coordination**
Maintain clear and constant communication with DevOps regarding environment consistency, external dependencies, testing timelines, etc. so that servers are properly configured and ready when needed.

All environment-related requests should be made via Jira tickets in the DOPS space _as early as possible_ to ensure proper planning, tracking, and accountability.

> [!NOTE]
> DOPS tickets require a target end date. When setting this field, keep their team's [sprint cadence](https://newyorkpubliclibrary.atlassian.net/jira/software/c/projects/DOPS/boards/14/backlog) in mind to avoid injecting sudden requests into their planned work.

For examples, see [DevOps requests for performance testing](https://newyorkpubliclibrary.atlassian.net/issues/?filter=12661).

---
### 3. Test Design
---
#### **Test Scenario Design**
Design test scenarios based on the identified core user flows and pages.

Ensure they're ranked in order of importance so the most common actions are carried out more frequently to accurately reflect live traffic patterns. This ranking will inform proper weighing of test scenarios when scripting the test.

#### **Define Load Profiles**
Establish different load profiles to evaluate the system's response under varying traffic levels. Ramp-up periods (known as _spawn rates_ in Locust) and test run durations should also be included to ensure that test runs are carried out using the same parameters each time.

Load profiles to test should include the following parameters defined in the table below. Note the concurrencies given below are examples; adjust according to available analytics data.

| Profile | Description | Concurrency | Duration | Spawn Rate |
| :--- | :--- | :---: | :---: | :---: |
| **Baseline** | User traffic during low or typical usage periods | 10 users | 10 min | 0.033 |
| **Peak** | User traffic during known high-usage periods | 200 users | 15 min | 0.444 |
| **Stress (or max)** | Extreme level of user traffic to identify system capacity | 1000 users | 30 min | 1.111 |

> [!NOTE]
> The spawn rates listed above are set so that the first half of each test serves as the ramp-up period, gradually increasing concurrency, while the second half maintains a steady user load.
>
> This approach is standard practice, but ramp-up speed can be adjusted as needed—such as using a faster ramp-up for stress testing or a slower one for more gradual load increases.
>
> Calculation of spawn rates for achieving halfway ramp-up is determined by dividing the number of users by half the duration (in seconds).

#### **Test Script Creation**
Develop one or more test scripts (known as locustfiles) as needed, defining weighted tasks that each carry out the set of web requests associated with the actions for a given test scenario. Set appropriate wait times to mimic user pauses, handle necessary request headers, and manage request payloads if applicable (e.g. for POST requests). See [Locust documentation](https://docs.locust.io/en/stable/) for syntax and other key information.

> [!TIP]
> LoadForge has a [browser recorder](https://docs.loadforge.com/test-scripts/record-your-browser) that may be used to capture the exact set of web requests involved in carrying out a set of actions.

---
### 4. Test Execution
---
#### **Local Testing**
Before running large-scale, paid tests with LoadForge, perform local testing to debug and refine test scripts.

This is done by installing the locust Python package then simply executing the command `locust` within a terminal while in a folder containing a file named locustfile.py. From there, navigating to [localhost:8089](http://localhost:8089) in a browser will provide a UI where a test can be run with the desired test parameters and results can be viewed along with the logging of any errors encountered.

#### **Environment Readiness**
Add the test environment as a host in LoadForge. Ensure proper connectivity and address any external domain requirements.

The domain [nypl.org](https://www.nypl.org) is already validated, permitting LoadForge access to any subdomain as well, but if testing involves a different domain (which is rare), host validation will require a DevOps request similar to [DOPS-725](https://newyorkpubliclibrary.atlassian.net/browse/DOPS-725).

> [!CAUTION]
> If the test environment is behind the VPN and/or restricted to on-prem access only, then LoadForge tests cannot be run on it, as its load generators for simulating user traffic will be unable to reach the server. If this is the case, then the access restrictions in place must be lifted (at least temporarily) in order to run a test.
>
> For an example DevOps request in this case, see [DOPS-781](https://newyorkpubliclibrary.atlassian.net/browse/DOPS-781).

#### **Test Definition**
The recommended way to create a test in LoadForge is by utilizing the Full Test Editor to import a locustfile and set the desired test parameters such as number of users, spawn rate, and location where traffic should originate from (New York is the most sensible option).

It is recommended to create one test per each load profile to avoid having to constantly edit a test in order to run against different user thresholds (e.g. baseline vs peak).

Optionally set scoring targets for KPIs to automatically determine the success or failure of a test run, but this is recommended only if an adequate amount of historical performance data exists for setting reasonable thresholds.

> [!WARNING]
> LoadForge offers a feature for quickly creating tests using a website crawler but it is not recommended for use because it bypasses key steps earlier in the process necessary for accurately simulating live traffic to the system under test (particularly, the identification and proper weighting of core user flows and pages).
>
> If test scenarios are not designed or weighed properly to reflect expected usage of the live system, any obtained test results would be ineffective in providing an accurate depiction of actual performance.

> [!TIP]
> On a short timeline, it is better to go with a simple test containing one task that just requests the root of the site.

#### **Running Tests**
After confirming environment readiness, test script accuracy, and monitoring tools are active, the test is ready to run with LoadForge. The duration of the test run is set at the time of running a test in LoadForge, not in the test definition itself.

Respective team members and DevOps should be notified of when a test run is to take place and ideally planned in advance. This can be done using the DevOps & Digital Release Calendar in our Google workspace calendar.

#### **Test Monitoring**
Actively monitor test runs using LoadForge's real-time reporting and any monitoring tools that have been set up to obtain real-time insights on system health. Note trends in KPIs and resource utilization as volume increases.

> [!IMPORTANT]
> Be prepared to stop the test if critical issues arise (e.g. if an external production dependency was overlooked and performance degradation is noticed in a live environment).

#### **After Test Runs**
Communicate test completion, share any initial findings (e.g. high error rate), and continue coordination with DevOps for any required environment resets or troubleshooting that may be needed.

> [!TIP]
> Do not request the test environment to be scaled down at this time. Wait until the remainder of the process detailed below is finished and it's confirmed that no more load testing will be needed for the current effort or until further notice.

---
### 5. Analysis & Data Collection
---

#### **Interpret Reports**
After test completion, interpret charts and graphs within the LoadForge reports. Analyze KPIs like median and P95 response times (aggregate and per request) to understand application responsiveness under load. Note errors, if any, identifying their response codes and which requests they occurred on.

Compare results to baseline metrics to determine how the system responds to higher traffic.

> [!NOTE]
> The line chart in a report that plots KPI measurements throughout a test is the ideal starting point for determining how well the system performed. Some key signs to look for when analyzing the chart from the test's start to its finish are given below.
>
> ✅&nbsp;&nbsp;<ins>System performed well</ins>:
>    - Throughput and users maintain a 1-1 relationship.
>    - Median response time begins to flatten and converges to a lower value.
>
> 🔻&nbsp;&nbsp;<ins>System performance degraded</ins>:
>    - Throughput flattens out or drops during ramp-up.
>    - Median response time and/or error rate continually increase and tail off to a higher value.
>    - Several large spikes occur for any KPI.
>      - If only this is observed without the above two, it indicates system instability but also shows an ability for it to recover quickly.

> [!WARNING]
> If local testing of the test script was not carried out, error spikes could be due to issues with the script itself. LoadForge produces logs that may provide debugging information for script issues.

#### **Utilize Observability Tools**
Use observability tools to correlate real-time data with metrics collected from LoadForge test results. If errors or performance degradation are detected, use New Relic APM (if set up); analyze logs to seek more information on errors and slow transaction traces to identify bottlenecks.

#### **Export Results (Recommended)**
Export test results and reports for historical tracking, long-term analysis, and sharing with stakeholders.

LoadForge retains our reports for up to 2 years, but it's better to own our performance data on our storage.

---
### 6. Reporting
---
#### **Create Report as Deliverable**
Create a report for documenting test results, recording KPIs and noting any deviations from baseline metrics or with prior results, if they exist. Ideally include an analysis of the results, highlighting noteworthy findings and takeaways.

Select a reporting format that's appropriate to the test scope. Larger projects likely warrant a doc or sheet to track KPIs across multiple test iterations, while for smaller requests it's usually sufficient to report results by commenting on the associated Jira ticket.

Note the following examples:
- Long term, project-based reporting: [DC Facelift Performance Testing](https://docs.google.com/document/d/196-OdgspFEbvb5VXidIwc5Fa1lK-i9XkHdWhAEH4dKo/edit?usp=sharing)
- One-off request reporting: [DR-3289](https://newyorkpubliclibrary.atlassian.net/browse/DR-3289)

> [!CAUTION]
> LoadForge test run reports may be shared with any team member via public links but the links expire after a short time. They also contain a lot of information that may seem unclear and potentially mislead stakeholders if not supplemented with guidance from the tester.
>
> Only consider using a LoadForge report as a deliverable when on a tight timeline.

#### **Communicate Test Results to Stakeholders**
Clearly communicate test results to stakeholders by delivering report(s) and ideally scheduling a meeting to review them.

The tester's role is to carry out the tests and present the findings effectively so that stakeholders can properly determine next steps (e.g. if a regression is detected for an upcoming release). Any insights gained from monitoring tools should also be shared, as they can point developers in the right direction for performance improvement.

#### **Version Control**
Commit test scripts and other relevant files to the GitHub repository for the system under test, ideally including a README with setup instructions and other information, such as links to past test runs.

Example: https://github.com/NYPL/de-visualization/tree/main/locust

---

## Cadence & Continuous Testing
Conducting performance testing on a regular schedule allows for effective monitoring and attribution of performance changes to specific code updates. This proactive approach enables early detection of regressions and helps maintain ongoing system reliability as a codebase evolves.

LoadForge provides a [scheduling feature](https://docs.loadforge.com/tests/scheduling#scheduling), enabling the automation of load testing at regular intervals. This enables consistent monitoring of system performance over time and helps quickly identify regressions or trends.

### CI/CD
Whether using Locust on its own or the [LoadForge API](https://docs.loadforge.com/api-reference/introduction), test runs can be triggered in CI/CD pipelines to support shift left initiatives.

To detect performance regressions during CI checks, a proven approach is to export key metrics from each test run as artifacts (such as a CSV) stored in the GitHub repository. Using tools like the [Google Sheet action](https://github.com/marketplace/actions/gsheet-action), a sheet can be automatically updated with the latest results, which enables comparison of current metrics against established benchmarks or previous test runs, helping to quickly identify regressions before merging code, track performance trends over time, and link performance changes to specific updates.
