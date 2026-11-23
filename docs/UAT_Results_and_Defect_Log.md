# UAT Results and Defect Log: Service Request Approval Analysis

Tester: Shital Parab
Date: 2026-11-23
Data: service_requests.csv, 200 synthetic requests (practice data only)
Tool under test: Power BI report (web)

## UAT results

| ID | Requirement | Test | Expected | Actual | Result |
|---|---|---|---|---|---|
| UAT-01 | BR-01 | Total Requests | 200 | 200 | Pass |
| UAT-02 | BR-01 | Approved count | 155 | 155 | Pass |
| UAT-03 | BR-01 | Rejected count | 25 | 25 | Pass |
| UAT-04 | BR-01 | Pending count | 20 | 20 | Pass |
| UAT-05 | BR-02 | Avg Approval Days (decided requests) | 2.81 | 2.81 | Pass |
| UAT-06 | BR-03 | SLA breached requests (count) | 43 | Not tested (no count visual built) | Not tested |
| UAT-07 | BR-03 | SLA Breach % (decided requests) | 23.9% | 0.24 displayed (shown to 2 decimals, equals 23.9%) | Pass (display format note) |
| UAT-08 | BR-04 | Avg approval days, Procurement (bar chart) | 5.07 | Not tested | Not tested |
| UAT-09 | BR-04 | Sum of requests by type equals total | 200 | Not tested | Not tested |
| UAT-10 | BR-05 | Filter Status = Pending | 20 | Not tested (no filter or slicer built) | Not tested |

Notes: values come from the Power BI report screenshot taken on 2026-11-23. Tests marked Not tested were not run.

## Defect log

| ID | Description | Impact | Workaround | Status |
|---|---|---|---|---|
| D-01 | Dataverse has a system Status column next to the imported status column, which broke the first formula | Medium | Used the lowercase imported status column | Closed |
| D-02 | File upload in Power Query was blocked by a missing OneDrive license | Medium | Loaded the data by another supported route | Closed |
| D-03 | Approvals connector blocked by the tenant data policy (error 442) | Medium | Built the flow without the Approvals connector | Open (tenant policy) |
| D-04 | Dataverse connector is Premium in Power Automate | Medium | Built an instant cloud flow with standard connectors (manual trigger, Compose action) and ran it successfully; the Dataverse-triggered version was not run | Closed (workaround) |
| D-05 | Power Apps Vibe is retiring, and Copilot Studio app builder had no credit pool | Medium | Built the canvas app by hand | Closed |

## Limits

All data is synthetic. Built in a developer environment, not for production. Slicer and cross-filter tests were not built.
