# HELIos Telemetry Dashboard Specification

## Objective

Provide low-friction observability for reliability, resilience, and automation quality with actionable alerts.

## Dashboard Surfaces

1. **KPI Strip**
   - processing success rate
   - duplicate side-effect rate
   - dedupe precision/recall
   - retry exhausted count
   - reconciliation max age
2. **Exploratory Timeline**
   - event throughput
   - failure classes over time
   - failover/degrade mode transitions
   - alert firing and acknowledgement events

## Data Model

- source tables: event logs, attempts, reconciliation outcomes, alert events
- aggregate views: hourly and daily SLO snapshots
- retention:
  - raw telemetry: 30-90 days
  - aggregated SLO views: 12 months

## API Endpoints (Template)

- `GET /api/telemetry/kpis`
- `GET /api/telemetry/timeline?from=&to=&domain=`
- `GET /api/telemetry/incidents`
- `POST /api/telemetry/alerts/test`

## Security and Privacy

- enforce RLS for tenant/workspace isolation
- expose aggregated views by default
- restrict raw payload access to authorized operators

## Alerting Pipeline

1. scheduled evaluation job computes threshold breaches
2. dedupe alerts by breach key and cooldown
3. route alert to collaboration channel and incident store
4. require acknowledgement and resolution metadata

## Shipping Checklist

- synthetic data run validates every widget
- alert test event reaches destination channel
- dashboard load p95 under target threshold
- role-based access paths verified
