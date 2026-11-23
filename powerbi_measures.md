# Power BI measures

Table: `service_requests` (loaded from `service_requests.csv`, 200 synthetic rows)

```dax
Total Requests = COUNTROWS(service_requests)

Approved = CALCULATE(COUNTROWS(service_requests), service_requests[status] = "Approved")

Rejected = CALCULATE(COUNTROWS(service_requests), service_requests[status] = "Rejected")

Pending = CALCULATE(COUNTROWS(service_requests), service_requests[status] = "Pending")

Avg Approval Days =
AVERAGEX(
    FILTER(service_requests, NOT ISBLANK(service_requests[decision_date])),
    DATEDIFF(service_requests[submitted_date], service_requests[decision_date], DAY)
)

SLA Breach % =
DIVIDE(
    COUNTROWS(
        FILTER(
            service_requests,
            NOT ISBLANK(service_requests[decision_date])
                && DATEDIFF(service_requests[submitted_date], service_requests[decision_date], DAY) > service_requests[sla_days]
        )
    ),
    COUNTROWS(FILTER(service_requests, NOT ISBLANK(service_requests[decision_date])))
)
```

## Definitions
- Approval days = decision date minus submitted date, in calendar days.
- Average approval days and SLA breach % use decided requests only (Approved and Rejected). Pending requests are excluded.
- SLA breach = approval days greater than the SLA days set for the request type (IT Access 2, Leave 3, Procurement 5, Expense 4).
- Without a percentage format, SLA Breach % displays as 0.24 (23.9% rounded to two decimals).
