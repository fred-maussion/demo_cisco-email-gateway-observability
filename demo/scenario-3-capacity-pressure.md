# Scenario 3: Connect queue growth with gateway capacity

**Slide:** `scenario-3-capacity-pressure.html` · **Duration:** about 5 min · **Role:** resilience and planning. Use it when the audience cares about capacity.

## Goal

Show that a gateway can look available while queues and resource metrics reveal pressure building up, and that the same view supports capacity planning with operational evidence.

**One-sentence message:** traffic peaks can hide emerging capacity limits. Put queue trends next to CPU, RAM, disk I/O and utilization.

## Setup

- Dashboard: **Cisco Secure Email Gateway — Overview**.
- Time range: widen to **Last 1 hour** (or longer if data exists). Trends need a longer window than the other scenarios. **Gateway host** and **Destination domain** = Any.
- Start on **Resource trends & fleet status**.

## Walkthrough

| # | Action | Point at | Talk track |
|---|--------|----------|------------|
| 1 | Start from the green KPIs at the top. | **CPU load**, **RAM utilization %**, **Disk I/O %**, **Mail Queue Utilization** | "Right now everything is green. A point-in-time view says the gateways are fine. Capacity problems start before the tiles turn red." |
| 2 | Scroll to **Resource trends & fleet status**. | **Cisco Secure Email Gateway message queues over time** | "Here is the queue over time. Look at direction and slope, not the current value." |
| 3 | Put the queue next to resources. | **Average Overall CPU Load over Time by Host Name** | "CPU per host: is the load even across the fleet, or is one gateway doing more work?" |
| 4 | Continue. | **Average system utilization over time** | "Overall system utilization trend. Combined with the queue, this shows whether the fleet is approaching its ceiling." |
| 5 | Check connections. Scroll up or use the KPI row. | **Current incoming SMTP connections**, **Current Outgoing SMTP Connections**, **Messages Received Per Minute** | "Is the pressure driven by traffic volume (more connections, more mail) or by resource drift (same traffic, higher load)?" |
| 6 | Isolate by host. In **Gateway host**, pick one host, then another. | CPU, utilization and queue panels | "Compare gateways. If one host sits higher on CPU and queue than its peers, rebalance traffic. If all rise together, plan scaling." Reset to **Any**. |
| 7 | Check fleet inventory. Scroll to the bottom. | **Latest gateway status per host**: System Status, Up Since, Model, Operating System, RAID Status | "Same view tells us which hosts are online, how long they have been up, model and OS version, and RAID status. Useful before deciding to take one out of rotation." |
| 8 | Close the loop. | **Total Queue Utilized %** and **Total Active Recipients** | "Queue utilization as a percentage and active recipients give a simple headroom number for capacity conversations." |

## Key takeaway

"The team can explain *when* to investigate a gateway, rebalance traffic, or plan scaling, using evidence from the same view they use for daily monitoring. It turns capacity planning from a gut feeling into a data conversation."

## Questions to expect

- **What threshold means "too high"?** It depends on the environment. Use the POC data to establish a baseline, then set thresholds and alerts from it.
- **Can this predict when we run out of capacity?** Trend panels show direction today. Elastic machine learning (anomaly detection and forecasting) can be added on these same metrics as a follow-up.
- **Does this replace Cisco's own tooling?** No. It adds a cross-fleet operations view and correlation with the other signals shown here.

## Fallback

- **Trends are flat:** say "this is a healthy baseline". Describe what a rising queue would look like, and point out that the panels would show it side by side.
- **Only a few data points:** widen the time range. If the data still starts only minutes ago, state that the history is short and the pattern becomes clearer as the POC runs.
- **A host is missing from the fleet table:** note it as a data-collection gap and continue.

## Transition

"That is the full loop: detect earlier, isolate faster, and plan with data. Let me close on the value." (Go to the closing slide.)
