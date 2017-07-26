# Methodology

A well-rounded system testing strategy needs to focus on speed, stability, and reliability. 
![alt text](https://docs.google.com/drawings/d/e/2PACX-1vQZ_28zzRptA6iN6kCJoZsIrfvGqg89myTvVfXQrUC1sG4TnG-IvHuXYV3Ur9pQToXh9sMnZ-ryVn00/pub?w=480&h=360 "Full View Testing")

### Local Developer / CI Testing
![alt text](https://docs.google.com/drawings/d/e/2PACX-1vQjiEyQe_sBHLVM3nQiKHhbBqX241jJr_QuSK0E2_HehkKzeqMWOpLcW86sNkrxo-BGCFJ_3BPohIAR/pub?w=480&amp;h=360 "Local Developer Testing")
* Focus is on finding issues _before merging to the master codebase_, where they would infect other streams of development, and are much more expensive to resolve ($0.10 defect vs $10,000 defect).

* **Unit testing**: Smallest testable pieces of a system, developer owned.
    * Measured in milliseconds.
    * Spotlight on module specification, measured by code coverage.
    * Test assets live in application repository.
    * Mock external integrations.
    * Run local on the developer machine, as well as pre & post-merge in the Continuous Integration system.
    * Risks: Developer assumptions, known dataset.
    * Mitigations: Peer review on tests.
    * *Failure fails the build*.

* **Functional testing**: Demonstrable feature testing, via browser, api, etc. Owned by developer & qa/test.
    * Measured in seconds.
    * Spotlight on feature behaviors, measured by feature coverage.
    * Test assets live in application repository.
    * Mock/fake external integrations.
    * Run local on the developer machine, via the browser or other external interface, pre & post-merge in the Continuous Integration system.
    * Risks: developer/tester assumptions, known dataset, flakiness, slows build.
    * Mitigations: Cross-functional sign-off on tests, set alert thresholds on test reliability and build performance.
    * *Failure fails the build*.

* **Feature performance testing**: Measure performance of features via tests that send metrics to a stats collector to graph performance over time.
    * Show performance graphs on Big TVs around the office, weekly reports, etc.
    * Run tests in every build, next to unit/functional tests.
    * Run local on the developer machine, as well as pre & post-merge in the Continuous Integration system.
    * Risks: Slows build, tests not executed on production infrastructure.
    * Mitigations: Peer review, alert thresholds on relative change in performance, not absolute measurements.
    * *Failure... alerts.* We want to be careful about premature performance optimization. But the data is important to trend.


### Pre-production Testing
![alt text](https://docs.google.com/drawings/d/e/2PACX-1vQma-vBOPkOOYX48U3cQN2Lw7_GFbUOL86mzQuvcjEaWucQoKmZlykybGMqRlijoy8dw07QRdEIP3A4/pub?w=480&h=360 "Pre-production Testing")
* Focus is on finding issues _before release to production_.
  * This is where traditional QA spent/spends most of their resources.
  * Expensive, but valuable if used correctly.
  * Real integrations with external services.
  * Share with internal experts, business experts for feedback on new features.
  * Scrubbed production dataset copy, refreshed weekly.
  * *Critical functionality failure holds up a release.*

* **Manual, exploratory testing**: Behavorial user testing, with empathy for end users.
    * Measured in defects found.
    * Targeted to new features, NOT a full regression cycle.
    * Not scripted.
    * Risks: Slow, specialized skills needed.
    * Mitigations: Cross-functional team feature verification, education on testing skills.

* **Load testing**: Test system under load for software and/or infrastructure vulnerabilities.
    * Measured in end user load.
    * Targeted to most heavily used features in production.
    * Risks: Slow, expensive to build & monitor, specialized skills needed.
    * Mitigations: Cross-functional team test creation, education on testing skills (contract experts).

### Production Testing
![alt text](https://docs.google.com/drawings/d/e/2PACX-1vTnmNAmo0bWczGgfrsebD6KbODw8P3xuiPTN199ak8FIq4mGoSvpFLt8xdQHkUhp4pgYkn2JM5tHVbB/pub?w=480&h=360 "Production Testing")
* Focus is on watching real user behaviors closely.
  * All defects cannot be found pre-release, and it is expensive to try.
  * Don't be proud. Assume you missed something.

* **Application testing**: Script bots to run automated tests against production application.
    * Black-box tests, focus on end-to-end functionality.
    * Run frequently, every minute (if possible).
    * Filter bot traffic for metrics reporting.
    * Test assets live in application repository, unless a 3rd party is used (New Relic).
    * Risks: Using & creating test data in production, expensive to monitor/mitigate, developer/tester assumptions on user behavior.
    * Mitigations: Pre-emptive outreach to Business, Support, Data, etc.
    * *Failure alerts Support, Ops, and cross-functional teams to assess and resolve*.

* **Release validation**: Validate new features have made it to production successfully.
    * Cross-functional team, focus on new changes.
    * Check after every release.
    * Filter traffic for metrics reporting.
    * Risks: Using & creating test data in production.
    * Mitigations: Pre-emptive outreach to Business, Support, Data, etc.
