# Cisco Secure Email Gateway POC: demo guide

Live demo scripts that go with the slide deck (`slides/`). Each scenario has the same structure: goal, setup, walkthrough, expected questions, fallback, transition.

| # | Scenario | Script | Slide |
|---|----------|--------|-------|
| 1 | Detect delivery pressure before users complain (lead story) | [scenario-1-delivery-pressure.md](scenario-1-delivery-pressure.md) | `scenario-1-delivery-pressure.html` |
| 2 | Identify whether the issue affects one destination domain | [scenario-2-domain-scope.md](scenario-2-domain-scope.md) | `scenario-2-domain-scope.html` |
| 3 | Connect queue growth with gateway capacity | [scenario-3-capacity-pressure.md](scenario-3-capacity-pressure.md) | `scenario-3-capacity-pressure.html` |

## Persona and scope

- **Persona:** email administrator running Cisco Secure Email Gateway (ESA) hosts.
- **Data:** **metrics only**. There is no message tracking or per-message content. Never promise message forensics. Every claim in the demo must rest on a panel on the dashboard.
- **Message:** Elastic moves the starting point from "a user opened a ticket" to "the signals told us first".

## Prerequisites

- Dashboard **Cisco Secure Email Gateway — Overview** (Observability > Dashboards) opened in Kibana, with data flowing.
- Time range **Last 15 minutes** and auto-refresh on. Widen the range to 1 hour if a trend looks too flat.
- Both control filters set to **Any**: **Gateway host** and **Destination domain**.
- Browser zoom at 80–90% so the three dashboard sections fit on screen.
- Sensible data check before presenting: the gateway KPIs are populated and the destination-domain table has rows. If not, see each script's Fallback section.

## Dashboard map

Use the same section names the audience sees on screen.

| Section | Panels |
|---------|--------|
| Gateway health: KPIs (latest values) | CPU load, RAM utilization %, Disk I/O %, Mail Queue Utilization, Messages in Work Queue, Messages in quarantine, Current incoming SMTP connections, Current Outgoing SMTP Connections |
| Mail flow & delivery | Messages Received Per Minute, Delivered recipients per minute, Hard Bounced Recipients per Minute, Soft bounce events per minute, and since-boot counters (received, delivered, dropped, rejected). Charts: *Email gateway message rates over time*, *Average email bounce rates over time*. Table: Destination Domain with Delivered Recipients, Hard Bounces, Soft Bounces, Latest Host Status |
| Resource trends & fleet status | *Average Overall CPU Load over Time by Host Name*, *Average system utilization over time*, *Cisco Secure Email Gateway message queues over time*, *Total Queue Utilized %*, *Total Active Recipients*, *Latest gateway status per host* (host name, system status, up since, model, operating system, RAID status) |

## Suggested flow

1. Cover and POC framing slides (about 2 min).
2. **Scenario 1** slide, then live dashboard (about 6 min). This is the lead story, so always run it.
3. **Scenario 2** slide, then live dashboard (about 5 min).
4. **Scenario 3** slide, then live dashboard (about 5 min). Use it when the audience cares about resilience and planning.
5. Closing slide (about 2 min).

If time is short, run Scenario 1 and the scenario that best matches the audience's stated pain, then go to the closing slide.

## Notes on the numbers

Example figures in these scripts match the generic dashboard image used in the deck. Live values will differ. Always read the real numbers off the screen and adapt the talk track. Do not quote the examples as facts.
