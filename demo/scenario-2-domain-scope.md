# Scenario 2: Identify whether the issue affects one destination domain

**Slide:** `scenario-2-domain-scope.html` · **Duration:** about 5 min · **Role:** scoping scenario.

## Goal

Show that when someone reports "mail to partner X is delayed", the email team can prove within a minute whether the problem is internal (the gateway fleet) or specific to a destination domain, and who should own the next action.

**One-sentence message:** faster ownership and cleaner communication.

## Setup

- Dashboard: **Cisco Secure Email Gateway — Overview**.
- Time range: Last 15 minutes (widen to 1 hour if the table is sparse). Both filters = Any.
- Start on **Mail flow & delivery**, with the **Destination Domain** table visible.

## Walkthrough

| # | Action | Point at | Talk track |
|---|--------|----------|------------|
| 1 | Set the scene from the slide: "A partner says our mail to them is delayed or rejected." | Table **Destination Domain** | "Where do we start? Without domain-level visibility the team spends the first hour proving whether it is us or them." |
| 2 | Read the table top to bottom. | Columns **Delivered Recipients**, **Hard Bounces**, **Soft Bounces**, **Latest Host Status** | "Every destination domain, side by side: volume delivered, permanent failures, temporary failures, and whether the gateway handling it is up." |
| 3 | Identify the outlier. | The partner domain row | Look for a domain whose bounce counts stand out relative to its delivered volume. In the generic example: `relay.partner.example` has 33 soft bounces on 77,861 delivered, while `mx1.northwind-example.com` shows 12,904 hard bounces on 1,882,440 delivered. Read the ratio, not only the count. |
| 4 | Distinguish the two bounce types. | **Hard Bounces** vs **Soft Bounces** | "Hard bounces are permanent: bad address or a policy rejection on their side. Soft bounces are temporary: their server is busy or deferring. The right owner and the right message to the partner differ." |
| 5 | Filter by domain. In **Destination domain**, select the partner domain. | All Mail flow panels update | "Now the whole dashboard is that domain only." |
| 6 | Check delivery and bounce panels. | **Delivered recipients per minute**, **Hard Bounced Recipients per Minute**, **Soft bounce events per minute**, **Average email bounce rates over time** | "Is delivery still flowing to them? Are bounces rising or flat?" |
| 7 | Prove the gateway is not the problem. Scroll to **Resource trends & fleet status**. | **Latest gateway status per host**, CPU and queue panels | "The gateways are online and their resources are normal, so this is not an internal capacity issue." (Only say this if it is true on screen.) |
| 8 | Compare with the rest. Reset **Destination domain** to **Any**. | Other rows in the table | "Other domains are delivering normally from the same gateways. Same fleet, different behaviour, so the scope is that domain." |

## Key takeaway

"In under a minute the admin can say: it is scoped to this domain, the gateways are healthy, and here is the bounce evidence to share with the partner. That separates internal operations from external delivery problems and puts the next action with the right owner."

## Questions to expect

- **Can we see *why* a domain is bouncing?** Not at message level in this POC, since it is metrics only. The hard versus soft split gives the direction (permanent versus temporary).
- **How many domains can it handle?** The table is sortable and filterable, so it works for many domains. Use the **Destination domain** control to jump to one.
- **Can we compare to yesterday?** Yes. Widen the time range, or add a time comparison. It is a natural follow-up.

## Fallback

- **No obvious outlier in live data:** pick the domain with the highest soft or hard bounces, or the highest delivered volume, and demonstrate the filter flow. The point is the method.
- **Table is sparse:** widen the time range to 1 hour or more.
- **Domain filter shows few values:** type the domain name directly in the control.

## Transition

"So far, mail was moving and the question was *where*. What about the case where mail still flows but the gateway itself is slowly running out of headroom? Last scenario."
