# What Is the Purdue Model and Why Should You Care About Network Segmentation
A practical breakdown of the Purdue Enterprise Reference Architecture, why it still matters in 2026, and what happens when it's ignored.

**L; DR**

The Purdue Model is a layered framework for organizing industrial networks from physical equipment on a factory floor up to enterprise IT systems so that critical control systems stay isolated from the internet-facing world. It was designed in the 1990s, long before "IT/OT convergence" was a phrase anyone used, but it's still the reference architecture most industrial network segmentation strategies are built on today. If you work anywhere near OT, ICS, or SCADA environments, understanding this model isn't optional — it's the mental map that makes network segmentation make sense.

Why this matters now

Most engineers coming from a traditional IT background think about networks in fairly flat terms: users, servers, a firewall at the edge, maybe a DMZ. Industrial networks don't work like that, and for good reason  they weren't built to serve web traffic, they were built to run physical processes safely, reliably, and continuously.

The problem is that industrial and enterprise networks have been merging for years. Sensors report to cloud dashboards. Engineers remote into control systems. Vendors push firmware updates over the internet. All of that convenience comes at a cost: it collapses the boundary that used to exist between "the internet" and "the machinery that runs a power plant, a water treatment facility, or a production line."

The Purdue Model exists to put that boundary back deliberately, in layers, instead of as an afterthought.

The Purdue Model, level by level

The framework organizes an industrial environment into a set of numbered levels, typically visualized as a stack:

Level 5 — Enterprise Network        (corporate IT, ERP, email, internet access)
Level 4 — Business Logistics       (business planning, scheduling, IT services)
────────────────────────────────── DMZ (Level 3.5) ──────────────────────────
Level 3 — Operations Management     (MES, historians, plant-wide monitoring)
Level 2 — Supervisory Control       (SCADA, HMI, control room systems)
Level 1 — Basic Control             (PLCs, RTUs, control logic)
Level 0 — Physical Process          (sensors, actuators, valves, motors)

A quick walk-through of what actually lives at each layer:

Level 0 : Physical Process: The actual equipment. Sensors, valves, motors, actuators — the stuff that physically does something in the real world.
Level 1: Basic Control: Programmable Logic Controllers (PLCs) and Remote Terminal Units (RTUs) that read from and command Level 0 devices in real time.
Level 2: Supervisory Control: This is where SCADA systems and Human-Machine Interfaces (HMIs) live  the tools operators actually use to monitor and control processes.
Level 3: Operations Management: Plant-wide systems like Manufacturing Execution Systems (MES) and data historians that aggregate information across the whole facility.
Level 3.5: The DMZ: Not part of the original model but added in later revisions because it's essential in practice. This buffer zone is where IT and OT are allowed to talk to each other carefully, through controlled, monitored pathways without OT ever being directly exposed to Level 4/5 traffic.
Level 4: Business Logistics: Corporate-facing systems like ERP, scheduling, and business planning tools.
Level 5: Enterprise Network: Standard corporate IT  email, internet access, general business applications.

The core idea is simple even if the diagram looks complex: traffic shouldn't jump straight from Level 5 down to Level 0. Every hop between layers should be deliberate, monitored, and restricted.

Why segmentation is the whole point

The Purdue Model is really a segmentation strategy wearing an architecture diagram's clothes. Here's what breaks down without it:

1. Flat networks turn a small breach into a catastrophic one

If a phishing email compromises a laptop on the corporate network, and that network has an unrestricted path down to Level 1 control systems, an attacker doesn't need to be sophisticated they just need to move laterally. Segmentation forces them to fight for every layer instead of walking straight through.

2. OT systems can't be patched like IT systems

A lot of Level 0-2 equipment runs on legacy firmware that can't be updated without risking downtime sometimes it can't be updated at all. You can't always fix the vulnerability, so instead you contain the blast radius. That's what proper network segmentation buys you.

3. Visibility gets exponentially harder without it

When everything's flat, "normal" traffic and "suspicious" traffic look identical because there's no structural expectation for what should be talking to what. With clear layers, unexpected traffic between, say, Level 5 and Level 1, is an immediate red flag instead of noise.

4. Compliance frameworks assume this structure exists

Standards like ISA/IEC 62443 one of the most widely referenced frameworks in industrial control system security are explicitly built around zone-and-conduit concepts that map almost directly onto Purdue's layers. Trying to demonstrate compliance without some form of this segmentation in place is an uphill battle.

What this looks like in practice

A few patterns that show up repeatedly in real-world implementations:

✔ Level 5 has internet access; Level 0-3 generally do not, directly.
✔ All IT↔OT traffic routes through the DMZ (3.5), never bypasses it.
✔ Each level has its own firewall/access control rules, not a shared perimeter.
✔ Remote vendor access terminates in the DMZ with logging/monitoring — never
  directly into Level 1/2 systems.
✔ Historian and MES data replicate outward (Level 3 → DMZ → Level 4), rather
  than allowing enterprise systems to query Level 1/2 directly.

None of this is about being paranoid for its own sake. It's about making sure that a compromise at one layer requires real, deliberate effort to become a compromise at the next layer down instead of being one hop away by default.

A modern caveat: the model is still relevant, but rarely followed strictly

Worth being honest here: pure Purdue implementations are increasingly rare. Cloud-connected sensors, remote monitoring platforms, and Industrial IoT devices don't always fit neatly into a five-level hierarchy  a lot of modern architectures use Purdue as a reference point rather than a rulebook, adapting it into more flexible zone-based models (which is part of why the ISA/IEC 62443 "zones and conduits" approach has become the more commonly cited standard in newer designs).

That said, the underlying principle hasn't gone anywhere: critical control systems should never be directly reachable from the internet or the corporate network, full stop. However, an organization draws its zones, that rule is non-negotiable.

Where this fits into a broader security strategy

Understanding the Purdue Model is really step one. In practice, applying it well tends to involve:

An OT risk assessment to map what actually exists in each layer before drawing any boundaries
Industrial network security work to enforce segmentation with real technical controls, not just a diagram
SCADA security measures specific to Level 2 supervisory systems, which are frequent attacker targets
Ongoing monitoring across DMZ traffic, since that's where IT/OT interaction and risk concentrates
Alignment with frameworks like ISA/IEC 62443 to formalize zones, conduits, and access policies

This is usually where organizations bring in dedicated OT/IoT security consulting not because the Purdue Model itself is complicated to explain, but because implementing real segmentation across legacy equipment, live production environments, and modern IT systems is a genuinely hard engineering problem, not a one-time diagram exercise.

Closing thought

The Purdue Model is over 25 years old, and it still holds up not because industrial networks haven't changed, but because the core problem it solves hasn't gone away: critical systems need distance from everything that touches the open internet. Segmentation isn't a nice-to-have layered on top of security. In OT environments, it more or less is the security strategy.

Found this useful? Feel free to fork, star, or open an issue if you think a section needs updating this is a living reference, not a one-time snapshot.
