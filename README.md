# dedicated server for gaming: the specs that matter, what it really costs, and how to pick a host for Minecraft, Rust, and CS2

Shared game hosting has a ceiling. Your Minecraft network fills up on Friday night and the panel starts throttling CPU. Your Rust server eats a 5Gbps flood and goes dark for an hour. Or you simply want root on the box, your own firewall rules, and no permission gymnastics every time you install a mod. That's usually the moment people start searching for a dedicated server for gaming.

This guide covers what hardware actually matters when you're hosting game servers — single-core clock speed beats raw core count for most titles — realistic RAM and storage targets per game, why DDoS protection decides whether your server stays online, and a concrete pricing comparison using Sharktech, a DDoS-focused host whose current bare-metal lineup runs from **$259 to $699 a month with free setup**.

## What you're actually buying: dedicated vs VPS vs game panel hosting

Game hosting comes in three tiers, and the differences matter more than the marketing suggests.

**Game server providers (GSPs)** sell pre-configured slots: one click, your ARK or CS2 server exists. You get a panel, automatic mod updates, and zero sysadmin work. Price range is roughly **$2–$30/month**. The trade-off is that you're on shared hardware with slot caps, and heavy modpacks frequently overload those plans.

**VPS hosting** gives you a virtual machine with root access on shared physical hardware, typically **$10–$70/month**. Fine for a friends-only Valheim world or a small modded Minecraft server. The catch is oversubscription: if your neighbors on the host machine spike, your tick rates spike with them.

**A dedicated server** is the entire physical machine, leased to you alone. No noisy neighbors, no slot limits, no resource arbitration. You install the OS, you run as many game instances as the hardware can carry, and performance is predictable. Cost lands roughly in the **$80–$400+/month** range depending on specs and bandwidth.

The rule of thumb that holds up across most buyer guides and community discussions:

- Under ~50 concurrent players, casual group → VPS or GSP is enough
- 50–100 players or heavy mods → high-slot GSP plans or a big VPS
- 100+ concurrent players, esports uptime requirements, repeated DDoS attacks, or multi-server networks → dedicated

If you're hosting one private world for five friends on a $259/month box, you're burning money. If you're running a public Rust server that gets attacked weekly and needs to stay online, dedicated pays for itself the first time an attack doesn't take you down.

## The specs that actually matter for a gaming dedicated server

Game engines are weird workloads. Most of them — Minecraft, Rust, ARK, Valheim — run a main game loop ("tick") that executes largely on a single CPU thread. That produces a counterintuitive buying rule: **a fast 8-core processor beats a slow 32-core one for a single busy world**. A 36-core Xeon running at 2.1GHz will stutter on a packed Minecraft server where an 8-core at 5GHz stays smooth.

Core count still matters — when you're running *many* server instances on one box, or pinning separate instances to separate cores. Match the CPU shape to your project, not to the spec sheet.

RAM and storage requirements depend heavily on the title and mod load:

| Game | Typical players | RAM target | Storage notes |
| --- | --- | --- | --- |
| Minecraft (vanilla/light) | up to ~20 | 4–8 GB | NVMe, fast single-thread CPU |
| Minecraft (modded) | 20–100+ | 12–32 GB | NVMe, trim view/simulation distance |
| Rust | 60–200 | 8–24 GB by map size | NVMe for entity churn, automate wipe backups |
| ARK: Survival | single world | 16–32 GB | NVMe for long saves; clusters want more |
| Valheim | up to 20 | 4–16 GB | NVMe reduces world hitching |
| CS2 (multi-instance) | per instance | 8–32 GB total | Pin cores per server for stable tick |

Two storage rules save people pain: put world saves on NVMe (large ARK and Rust saves can take minutes on SATA), and keep backups on separate storage — a RAID1 array that also holds your only backup copy isn't a backup strategy.

**Network and location.** For bandwidth, 1Gbps handles most game servers comfortably; 10Gbps matters when you're serving map downloads, running SteamCMD updates for multiple instances, or hosting events. Location is the bigger latency lever: pick a data center near your players, then verify with actual ping and route checks (mtr) before committing. Evening congestion on the last-mile ISPs your players use affects real-world lag more than raw distance does.

## DDoS protection is not an optional feature for public servers

If your server is publicly listed, it *will* get attacked at some point. It's cheap to do, bots do it for fun, and competitors in the game-server space do it to each other. Generic web-oriented DDoS filtering often handles TCP floods poorly against UDP game traffic — you need filtering that understands game protocols and keeps tick rates stable while scrubbing is underway.

This is the area where hosting choices genuinely diverge. Some providers charge extra for meaningful protection; some include network-level filtering on every service.

Sharktech, for example, builds its whole identity around DDoS protection — every service includes their proprietary network-level mitigation, and they offer a 100Gbps protection tier for customers expecting attacks beyond the standard limit, spread across their data centers using anycast BGP. A testimonial published on their own site from game-server operator Dingdian Network describes attacks "ranging from 3Gbit to 8Gbit" against their game servers with the servers never skipping a beat. Treat vendor-site testimonials with appropriate skepticism, but it's a signal of who their customer base is: game-server providers themselves.

## Sharktech's dedicated server lineup: all current plans and prices

Sharktech has been in the hosting business for about 20 years, operating from five data centers — Los Angeles (near One Wilshire, a major US–Asia traffic hub), Las Vegas, Denver, Chicago, and Amsterdam. Every dedicated server ships with DDoS protection, a bare-metal management panel, 24/7 support, a **99.99% uptime guarantee**, and free setup. Hardware is upgradeable at any time: RAM scales up to 1TB, and network ports scale from 10Gbps to 40Gbps or 100Gbps.

Here is their full current dedicated server lineup as displayed on their site:

| Plan | CPU (cores × clock) | RAM | Storage | Network | Monthly price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| Dual Xeon E5-2695v4 (2.5" bays) | 36 × 2.1 GHz | 64 GB DDR4 | 2TB M.2 NVMe + 6× 2.5" SATA/SAS bays | 10 Gbps, 300TB/mo | **$259/mo** | [ Configure this server](https://portal.sharktech.net/aff.php?aff=1611&pid=741) |
| Dual Xeon E5-2695v4 (3.5" bays) | 36 × 2.1 GHz | 64 GB DDR4 | 2TB M.2 NVMe + 6× 3.5" SATA/SAS bays | 10 Gbps, 300TB/mo | **$269/mo** | [ Ask Sharktech sales about this build](https://bit.ly/SharKTech) |
| Dual Xeon Gold 6248 (3.5" bays) | 40 × 2.5 GHz | 128 GB DDR4 | 2TB M.2 NVMe + 3× 3.5" bays | 10 Gbps, 300TB/mo | **$299/mo** | [ Configure this server](https://portal.sharktech.net/aff.php?aff=1611&pid=660) |
| Dual Xeon Gold 6248 (2.5" bays) | 40 × 2.5 GHz | 128 GB DDR4 | 2TB M.2 NVMe + 6× 2.5" bays | 10 Gbps, 300TB/mo | **$309/mo** | [ Configure this server](https://portal.sharktech.net/aff.php?aff=1611&pid=636) |
| Dual Xeon Gold 6246 | 24 × 3.3 GHz | 128 GB DDR4 | 2TB M.2 NVMe + 3× 3.5" bays | 10 Gbps, 300TB/mo | **$309/mo** | [ Configure this server](https://portal.sharktech.net/aff.php?aff=1611&pid=814) |
| Dual Xeon Gold 6248 (U.2 NVMe) | 40 × 2.5 GHz | 128 GB DDR4 | 2TB M.2 NVMe + 6× U.2 NVMe bays | 10 Gbps, 300TB/mo | **$329/mo** | [ Configure this server](https://portal.sharktech.net/aff.php?aff=1611&pid=766) |
| AMD EPYC 7702P | 64 × 2.0 GHz | 128 GB DDR4 | 2TB M.2 NVMe + 10× U.2 NVMe bays | 10 Gbps, 300TB/mo | **$499/mo** | [ Configure this server](https://portal.sharktech.net/aff.php?aff=1611&pid=729) |
| Dual AMD EPYC 7702 | 128 × 2.0 GHz | 128 GB DDR4 | 2TB M.2 NVMe + 10× U.2 NVMe bays | 10 Gbps, 300TB/mo | **$699/mo** | [ Ask Sharktech sales about this build](https://bit.ly/SharKTech) |

A few things worth knowing before you order:

- **Setup is free on every plan**, and billing defaults to monthly with no lock-in. Longer commitments cut the price — on the $259/mo plan, paying annually works out to about **$220/mo equivalent** (roughly 15% off). Similar discounts apply across the lineup.
- All plans include a /29 IPv4 allocation option and free IPv6 — you select these on the order form.
- The order form includes the OS choice, control panel options, RAID configuration, and the DDoS protection tier (basic included, 100Gbps as an add-on).
- **Delivery is not instant.** Sharktech states plainly that due to hardware shortages they can't guarantee delivery in under 24 hours, especially for customized bare-metal. Expect a wait measured in days, not minutes, and plan your launch date around it.
- Prices are USD, current as of this writing, and subject to inventory availability. If a configuration isn't listed, their sales team builds custom servers on request — [👉 reach them through the order page](https://bit.ly/SharKTech) and they typically respond within hours.

## Which plan fits which gaming project

The honest caveat first: these are enterprise Xeon and EPYC builds, not consumer Ryzen boxes. Base clocks run 2.0–2.5GHz (3.3GHz on the Gold 6246). If your entire project is *one* heavily modded Minecraft world and nothing else, a gaming-focused provider selling a high-clock consumer CPU may give you smoother ticks for similar money. Buy the CPU shape your workload needs.

Where this lineup makes sense:

**Multi-server networks.** The $259 Dual E5-2695v4 with 36 threads and 64GB is built for this — a BungeeCord-style Minecraft network with a hub plus several game modes, or a cluster of smaller servers, each pinned to its own cores. Per-instance clocks are modest, so don't point all 36 cores at one busy PvP world.

**Tick-hungry single worlds.** The Dual Gold 6246 at **24 × 3.3GHz** is the best per-core option in this lineup. For one busy Rust or ARK server where single-thread speed drives your tick rate, it's the pick — and the 128GB default RAM covers heavy modpacks with room to spare.

**Hosting multiple communities or game studios.** The 40-core Gold 6248 ($299–$329) and the EPYC boxes ($499/$699) are for people running many instances simultaneously — game-server resellers, community clusters across several maps, studios running test and staging environments next to production. The EPYC's 10 U.2 NVMe bays also give you a genuine storage expansion path (3.84TB to 15.36TB drives), which SATA-bay plans don't offer.

**Location-driven choices.** Players split between the US and Asia benefit from the Los Angeles data center near One Wilshire; European communities should look at Amsterdam; central-US player bases are well served by Denver or Chicago.

## Budget reality check

Dedicated gaming hosting across the market runs roughly **$80–$400+ per month** — that's the band most buyer guides converge on for capable hardware. Sharktech's floor of $259/mo sits in the middle-upper part of that band, and what you're paying for is the included DDoS protection, 10Gbps standard ports, and 300TB of monthly transfer on every plan. Comparable providers often charge extra for either the protection tier or the port speed.

If $259 is more than your project can carry, the alternatives within the same company are cheaper: their game-server hosting page advertises plans starting around **$7.95/month** for panel-style hosting, and their VPS line includes configurations sized for games (their own promo copy describes a 32GB/4-core VPS as suited for game hosting, with 60Gbps DDoS protection included). Sharktech also has a history of running promotional pricing with recurring discounts on dedicated boxes — those promos come and go, so if you're price-sensitive, [👉 ask their sales team what's currently on offer](https://bit.ly/SharKTech) before committing at list price.

One more balanced data point: Sharktech holds a 3.5-out-of-5 TrustScore on Trustpilot, but across a very small number of reviews — too few to treat as a strong signal either way. Their longevity, their game-provider customer base, and their DDoS engineering track record are better indicators than that sample.

## Day-one checklist once your server arrives

Bare-metal gives you power, and responsibility. The first hours decide whether your community's first impression is smooth or chaotic:

1. **Harden the OS.** Default-deny firewall; open only the ports each game needs — 25565/TCP for Minecraft, 28015–28016 for Rust (UDP game, TCP RCON), 7777/7778 and 27015 for ARK, 27015–27036 for CS2, 2456–2458 for Valheim. Restrict RCON to specific IPs if you use it at all.
2. **Set your DDoS posture.** Confirm the included protection is active on your IP range, and decide whether your threat level justifies the 100Gbps add-on before launch night, not after.
3. **Storage layout.** World saves on NVMe, logs on a separate path, backups written off-box on a schedule. Test an actual restore once — an untested backup is a hope, not a plan.
4. **Monitor.** Track single-core utilization at peak, memory growth after wipes and updates, and run periodic route checks to the ISPs your players actually use.
5. **Load-test before inviting anyone.** Simulate peak player counts (or invite a small test group) so the first real Friday night isn't your first stress test.

Linux keeps overhead lower and automation cleaner; Windows Server makes sense mainly when your tooling or specific game server software requires it, and adds licensing cost.

## Quick FAQ

**Is a dedicated server better than GSP panel hosting for gaming?**
It depends on what "better" means for you. Dedicated wins on consistent tick rates, player counts above ~100, heavy modpacks, DDoS resilience, and running multiple game instances. GSPs win on setup time, managed mods, and price for small groups. Be honest about how much sysadmin work you want to do.

**How many players can one of these boxes handle?**
Rule-of-thumb figures from hosting guides: a well-configured Minecraft server on strong single-thread hardware handles 150–200 players; Rust runs 150–200 on mid-size maps with 16–32GB; ARK clusters run 2–3 maps at 50–70 players each with 32GB+. Mods and plugins move these numbers a lot — treat them as ceilings to test toward, not guarantees.

**Windows or Linux for game servers?**
Linux for lower overhead, cheaper licensing, and cleaner automation, unless your game's server software or admin tooling is Windows-only. Most major titles — Minecraft, Rust, ARK, CS2, Valheim — run fine on Linux.

**How long until the server is live?**
Not instantly. Bare-metal provisioning at Sharktech can take up to a few business days depending on hardware availability and customization. Order before your planned launch, not the night before.

**Can I upgrade the hardware later?**
Yes — Sharktech allows CPU, RAM, storage, and network upgrades at any time, though delivery timelines and hardware availability still apply to upgrades.

## The short version

A dedicated server for gaming is worth it when shared hosting's limits are actively hurting you: player counts that overflow slot plans, mods that crash panels, DDoS attacks that take you offline, or a network of servers that needs one predictable machine underneath it all. Below that threshold, a VPS or a GSP saves you money and weekend hours.

When you shop, buy in this order: single-core CPU speed for your main world, enough RAM for your mod load, NVMe for saves, a data center near your players, and DDoS protection that understands game traffic. Sharktech's lineup checks the protection, network, and location boxes on every plan — the $309 Gold 6246 is the strongest pick here for a single busy server, the $259 E5-2695v4 for a multi-instance network, and the EPYC boxes for serious multi-community operations. Just go in with open eyes about the enterprise CPU clocks and the non-instant provisioning.

If that trade lines up with your project, [👉 check Sharktech's current dedicated server lineup and configure a box](https://bit.ly/SharKTech) — and if your budget or timeline is tighter, their sales team will tell you straight whether a VPS tier or a current promo fits better.
