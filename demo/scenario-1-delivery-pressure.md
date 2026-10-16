# Scenario 1: Detect delivery pressure before users complain

**Slide:** `scenario-1-delivery-pressure.html` · **Duration:** about 6 min · **Role:** lead story, always run it.

## Goal

Show that the email admin can see delivery pressure building from gateway signals, before helpdesk tickets arrive, and can narrow it to a gateway, a queue buildup, a destination domain, or an external dependency.

**One-sentence message:** tickets are a late signal. Elastic correlates mail flow, queue pressure, SMTP connections and gateway health so you start from the signal.

## Setup

- Dashboard: **Cisco Secure Email Gateway — Overview**.
- Time range: Last 15 minutes. **Gateway host** = Any, **Destination domain** = Any.
- Start scrolled to the top, on the title and the **Gateway health: KPIs** row.

## Walkthrough

| # | Action | Point at | Talk track |
|---|--------|----------|------------|
| 1 | Back from the slide. Show the top of the dashboard. | Section **Gateway health: KPIs (latest values)** | "This is the first thing the email admin sees: is the fleet healthy right now?" Name the green tiles: CPU load, RAM utilization %, Disk I/O %, Mail Queue Utilization. |
| 2 | Stay on the same row, move right. | **Messages in Work Queue**, **Messages in quarantine**, **Current incoming SMTP connections**, **Current Outgoing SMTP Connections** | "Green means the gateway itself looks fine. But a gateway can be up and still be struggling to deliver. Queue and connection counts show that." Example: 6 messages in the work queue, 32 incoming connections. |
| 3 | Scroll to **Mail flow & delivery**. | **Messages Received Per Minute** vs **Delivered recipients per minute** | "Pressure shows up when received and delivered stop moving together." Example: 2,412 received per minute and 3,655 delivered per minute. Explain that delivered is counted in recipients, so it can legitimately exceed messages received. |
| 4 | Point at the chart. | **Email gateway message rates over time** | "Look at the shape, not just the number. If received keeps rising while delivered flattens, a queue is about to form." |
| 5 | Point at the bounce chart. | **Average email bounce rates over time**, **Hard Bounced Recipients per Minute**, **Soft bounce events per minute** | "A spike in bounces tells us delivery quality is degrading, even though mail is still entering." |
| 6 | Scroll to **Resource trends & fleet status**. | **Cisco Secure Email Gateway message queues over time**, **Total Queue Utilized %** | "Now the queue trend. A rising line here is the earliest hint that downstream delivery is slowing." |
| 7 | Narrow the scope with a filter. In **Gateway host**, pick one host. | All panels update | "Is it one gateway or the whole fleet? One click answers that." Reset to **Any**. |
| 8 | Narrow again. In **Destination domain**, pick one domain. | Delivery and bounce panels update | "Or is it one destination? That is Scenario 2." Reset to **Any**. |

## Key takeaway

"By the time a user reports delayed or rejected email, the team is already reactive. Here the admin sees queue growth, rate divergence and bounces first, and can decide *where* to look: gateway, queue, domain or external dependency."

## Questions to expect

- **Can we alert on this?** Yes. Any of these metrics can drive an Elastic alerting rule, for example Mail Queue Utilization above a threshold for N minutes. This POC uses the dashboard, and alerting is a natural next step.
- **Can we see the actual delayed messages?** Not in this POC. The dataset is metrics only. Message-level data would be a separate data source.
- **What is the data source?** Cisco Secure Email Gateway metrics collected into Elastic. Keep the answer at this level unless asked for details.

## Fallback

- **Everything is flat or calm:** that is a valid result. Say "this is what healthy looks like" and show the same panels as the baseline. Widen the time range to 1 hour to find any variation.
- **A panel is empty:** skip it and use the neighbouring panel that carries the same message. Do not debug live.
- **No data at all:** use the generic screenshot on the cover slide and walk through the same steps verbally.

## Transition

"That showed the fleet-level view. But what if the complaint is about one specific destination? Next scenario."
