# Cisco Secure Email Gateway observability demo

A short Elastic demo for email administrators who run Cisco Secure Email Gateway (ESA). It shows how gateway **metrics** in Kibana give early warning of delivery problems, so the team doesn't start from a helpdesk ticket.

The demo is **metrics only**: it covers operational visibility and triage, not message-level forensics.

## What's in this repo

| Path | Contents |
|------|----------|
| `slides/` | The deck: six HTML slides for [fslides](https://fslides.dev) on a fixed 1280×720 canvas |
| `demo/` | Live demo scripts: a [README](demo/README.md) plus one script per scenario |
| `assets/` | Screenshot of the Kibana dashboard (synthetic data, no real hostnames or domains) |
| `notes.json` | Speaker notes per slide, each pointing to the matching demo script |
| `fslides.config.js` | Slide order and labels |
| `scenario-*.gif` | Animated previews of the three scenario slides |

## The three scenarios

1. **Delivery pressure:** detect rising queues and diverging received/delivered rates before users complain. This is the lead story. Script: [demo/scenario-1-delivery-pressure.md](demo/scenario-1-delivery-pressure.md)
2. **Domain scope:** show whether a delivery problem affects one destination domain or the whole fleet. Script: [demo/scenario-2-domain-scope.md](demo/scenario-2-domain-scope.md)
3. **Capacity pressure:** link queue growth to CPU, RAM, disk I/O and SMTP connections for capacity planning. Script: [demo/scenario-3-capacity-pressure.md](demo/scenario-3-capacity-pressure.md)

The demo runs on the **Cisco Secure Email Gateway — Overview** dashboard. The panels it relies on are listed in [demo/README.md](demo/README.md).

## Run the deck

Requires Node.js and the `fslides` CLI.

```bash
npm install            # installs the slide tooling
npm run serve          # open the deck in the browser player
```

## Export

```bash
npm run pdf            # PDF of all slides
npm run export         # single self-contained HTML file
npm run gif -- <slide> # animated GIF of one slide
```

If the PDF export fails because Puppeteer has no bundled Chrome, point it at an installed one:

```bash
PUPPETEER_EXECUTABLE_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" npm run pdf
```

Speaker notes (`notes.json`) are shown in the `serve` player. They are **not** included in the PDF or the single-file HTML, so share the `demo/` folder alongside those exports.

## Using this with real data

The screenshot in `assets/` is a mock-up with invented domains, hostnames and figures. When you run the demo for real, use a dashboard backed by your own gateway metrics, and treat any screenshot of it as sensitive before adding it to this repo.
