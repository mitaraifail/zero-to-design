# Product Definition · Pulse

## Product Name
Pulse

## One-sentence Definition
It is a tool that rolls an indie developer's revenue, user, and event data into one clear homepage, so you can tell whether anything is off in 30 seconds every morning.

## Target User
- **Age**: 25–40
- **Background**: Full-stack / backend engineers, indie developers, one-person company founders
- **Revenue Sources**: SaaS subscriptions, paid apps, small tools, digital products
- **How they currently look at data**:
  - Stripe Dashboard for revenue, but only daily/weekly views with no event linkage
  - Google Analytics for traffic, but funnels are complex and they rarely drill down
  - Self-written SQL/scripts to query the database, which is tedious to maintain
  - Key numbers occasionally jotted into Notion or Excel and updated manually

## User Mindset
They open it first thing in the morning with a slight anxiety of *"is my product okay today?"* and want to confirm within 30 seconds:
- Did revenue drop?
- Are active users abnormal?
- Did yesterday's shipped feature make any difference?

They are not here for deep analysis; they are here to rule out bad news and maybe spot a small win.

## Atmosphere Keywords
**Calm + Speed**

Professionalism is the baseline, not something to emphasize separately:
- **Calm**: reduces anxiety; anomalies do not glare
- **Speed**: a glance is enough; no time wasted

## Core Differentiator
"It proactively tells you today's status every morning, instead of waiting for you to go look."

Stripe / GA / self-built dashboards make you dig. Pulse prepares the daily status for you so you only need to look. This difference directly shapes the homepage architecture: the top should be a "today summary," not a wall of drill-down charts.

## Conversion Goal
**Default state**: scanning key numbers within 30 seconds and leaving is a normal and successful path.  
**Anomaly state**: when a metric needs attention, the homepage must make it visible at a glance and let the user drill down in one click.

## Design Constraints
- **Platform**: Web
- **Audience Age**: 16–40
- **Accessibility**: no special requirements
- **Existing Brand Assets**: none
