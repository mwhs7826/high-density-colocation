# high density colocation: power, cooling, and what actually matters when choosing a provider for AI and GPU racks

If you typed "high density colocation" into a search box, you're probably not shopping for a $99 shared cabinet. You've got gear that drinks power — GPU trays, dense 2U compute, AI inference boxes, maybe a stack of H100s — and you've already figured out that the average colo facility will either refuse your rack or quietly throttle it the moment load spikes. The question isn't really "what is high density colocation." It's "which facility can actually handle my power draw without lying about it on the spec sheet, and what do I need to verify before I sign."

This article walks through what genuinely defines a high-density deployment, where the costs and risks hide, and how a carrier-neutral operator like DMIT — which runs colocation out of Los Angeles, Hong Kong, and Tokyo — fits into the picture if you're targeting AI, HPC, or latency-sensitive workloads with a China or APAC component.

## What "high density" actually means in 2026

Colocation density is measured in kilowatts per rack, and the baseline keeps shifting upward because of AI. The rough tiers that show up consistently across providers:

- **Standard colocation:** 3–5 kW per rack. This is what most legacy facilities were built for — a rack of 1U web servers, maybe some storage.
- **High-density baseline:** 10–15 kW per rack. Where mainstream "high-density" marketing starts.
- **AI / GPU density:** 30–50 kW per rack. Typical for a rack packed with current-gen GPU servers.
- **Extreme density:** 60–100+ kW per rack, generally liquid-cooled. Some operators report observed racks north of 140 kW, and next-generation designs are talking about 200–240 kW per rack for fully liquid-cooled GPU clusters.

The reason this matters is simple: a facility that lists "high-density support" on its homepage may mean 15 kW, and your rack may need 40. Those are not the same conversation. The first real question to ask any provider is the maximum sustained kW per cabinet they can deliver at the specific location you want — not the marketing number, the actual engineered limit on the floor you'd be placed on.

## Cooling is the real ceiling, not power

Power gets the headlines, but cooling is what actually caps density. You can often pull more amps if the facility upgrades a circuit, but getting heat *out* of a hot aisle at 40 kW/rack is a different engineering problem entirely.

Air cooling works up to a point — most operators put that point around 20 kW per rack, with some pushing 25–30 kW using hot/cold aisle containment and high-capacity CRAC units. Beyond that, air becomes inefficient and unreliable, and liquid cooling moves from "nice to have" to "the only thing that works."

The main liquid options you'll see:

- **Direct Liquid Cooling (DLC):** cold plates on the CPUs/GPUs, liquid in a closed loop. The most common approach for GPU racks today.
- **Air-Assisted Liquid Cooling (AALC):** a hybrid that extends the range of air infrastructure with rear-door or in-row liquid heat exchangers.
- **Immersion cooling:** whole servers (or components) submerged in dielectric fluid. Best PUE numbers (1.02–1.05 vs. 1.3–1.6 for air), but it's a bigger operational commitment — different server form factors, different maintenance procedures, harder to swap a failed DIMM.

If your deployment is heading past 30 kW/rack, treat liquid-cooling readiness as a hard filter when you're screening facilities. A provider that says "we can do 50 kW air-cooled" is either exceptional or optimistic; verify it against an actual engineered spec, not a sales deck.

## Power infrastructure: the things that actually bite you

Beyond raw kW per rack, the things that separate a facility that *can* take your load from one that *will* take your load without incident:

- **A/B dual feeds** — two independent power paths from separate PDUs, ideally from diverse utility entrances. Single-feed cabinets are fine for a web server, not for a $300k GPU rig.
- **Three-phase power** at higher amperage circuits. High-density racks almost always need 3-phase 30A/50A/60A rather than single-phase 15A/20A.
- **N+1 (or better) UPS and generator backup**, with enough fuel runtime to cover a real utility outage, not just a brownout.
- **Metered vs. fixed power billing.** Metered is honest — you pay for what you draw. Fixed can be cheaper if your load is steady, but watch for clauses that cap sustained draw below the rated circuit size.
- **Headroom on the floor.** Even if a cabinet is rated for 40 kW, you need to ask whether the *row* and *facility* can sustain multiple such racks simultaneously, or whether you're sharing a cooling loop with someone else's lower-density gear.

One subtlety people miss: a facility can be rated for high density in aggregate but have specific floors or pods that can't actually deliver it. Get the per-location number, not the portfolio number.

## What high density costs, roughly

Pricing in the US primary markets (Northern Virginia, Dallas, etc.) in 2026 sits roughly in the **$180–$400 per kW per month** range, with secondary markets around **$130–$250 per kW**. Per-rack pricing for a full cabinet at standard density averages around **$300–$1,000/month** for 3–5 kW, and high-density deployments at 10–20 kW typically land between **$1,000 and several thousand dollars monthly** depending on market, cooling method, and bandwidth inclusions.

The interesting thing about high density from a TCO standpoint is consolidation. A workload drawing ~7 kW split across two standard low-density racks (~$3,000/month at typical pricing) can often fit on a single high-density rack (~$1,500/month) — roughly half the cost for the same compute, plus fewer cross-connects, less cabling, and a smaller physical footprint to manage.

The catch is that high-density pricing is almost never list. It's quoted per-deployment based on your actual power draw, cooling method, port speed, bandwidth commitment, IP needs, and contract length. Any article giving you a fixed "high density costs $X" number without those variables is either oversimplifying or making it up.

## A practical checklist before you commit

If I were evaluating a facility for a GPU or AI deployment tomorrow, the questions I'd want answered in writing:

1. **Max sustained kW per rack** at the specific location/floor I'd be placed on — not the marketing number.
2. **Cooling method** for that density tier — air, DLC, AALC, immersion — and whether liquid is included or a paid add-on.
3. **Power redundancy** — A/B feeds, diverse utility entrances, N+1 or 2N UPS, generator runtime.
4. **Circuit type** — single-phase vs. three-phase, available amperage.
5. **Billing model** — metered vs. fixed, and whether sustained draw is capped below the rated circuit.
6. **Cross-connects and carrier neutrality** — can I bring my own carriers, reach IXes, get private interconnects to cloud on-ramps?
7. **Remote hands** — 24/7, what's included (reboots, swaps, media), what's billable, response SLA.
8. **Compliance certifications** — ISO 27001, SOC 2, PCI DSS — if your workload needs them.
9. **Physical security** — biometric access, CCTV, on-site guards, escort policy.
10. **Scalability** — can I add another high-density rack next quarter without relocating, or am I capped at one pod?

That list isn't exhaustive, but it covers the items that actually show up in post-mortems when a deployment goes sideways.

## Where DMIT fits if your workload has a China or APAC angle

DMIT is a carrier-neutral infrastructure operator running colocation out of three locations — Los Angeles (CoreSite LA campus plus Digital Realty), Hong Kong (Equinix HK2), and Tokyo (Equinix TY8). All three are Tier III-class or better facilities with N+1 power and cooling, 24/7 on-site staff, and ISO 27001 / SOC 2 / PCI DSS compliance coverage.

A few things that make DMIT worth looking at specifically for high-density-style workloads, even though their colocation is quote-based rather than list-priced:

**China-optimized routing is the actual differentiator.** This is the thing DMIT is known for. They hold direct peering with all three major Chinese carriers — China Telecom (AS4809), China Unicom (AS9929), and China Mobile International (AS58807) — and on the Premium Network they run China Telecom CN2 GIA. From Hong Kong, they reference ~15 ms average latency to China Mainland with packet loss under 0.1%. If your high-density rig is serving users or training pipelines that touch China, that routing is the part most generic colo providers can't match at any price.

**Three network tiers let you match cost to traffic profile.** DMIT splits its network into Premium (CN2 GIA, best quality, higher cost per GB), Eyeball (CMIN2/CMI, reasonable-effort China routing at a lower price), and Tier 1 (clean APAC + Americas routing, no China-specific optimization, most economical). For a GPU inference box that mostly serves US users with occasional China traffic, Tier 1 with an Eyeball fallback is a very different cost profile from running everything on Premium.

**Colocation is sold as a custom quote, not off-the-shelf SKUs.** You tell them your hardware, power draw, bandwidth, and location, and they put together a tailored plan. This is normal for high-density — list pricing doesn't survive a real power/cooling conversation — but it means you won't find a public price table. If you want to see what your specific deployment would cost, the entry point is 👉 [open a colocation quote request with DMIT](https://bit.ly/DmiT).

**The colocation footprint** supports 1U–4U per-unit deployments, half cabinets, and full cabinets, with private cages available on request. Bandwidth is offered on 95th percentile, committed + burst, or flat unmetered models, with 1G/10G/higher port options and cross-connects to carriers and IXes. IP resources include IPv4/IPv6 allocations, BYOIP with LOA, ASN application assistance, and RPKI/IRR/rDNS support. Always-on volumetric DDoS protection is included at the edge.

## DMIT colocation options at a glance

The table below covers the three deployment tiers DMIT publishes on their colocation page. Pricing is quote-based — final numbers depend on your actual power draw, cooling method, port speed, bandwidth commitment, and contract length, so the links go to the quote request rather than a checkout.

| Deployment tier | Footprint | Best for | Power / cooling | Pricing | Get a quote |
| --- | --- | --- | --- | --- | --- |
| **Rack Units (1U–4U)** | Per-unit in a shared secured cabinet | Single servers, edge nodes, small appliances getting started | Shared cabinet power; scales with your unit size | Quote-based, pay-as-you-grow | [Request a quote](https://bit.ly/DmiT) |
| **Half Cabinet** | Lockable half cabinet with dedicated power and bandwidth | Mid-size clusters, storage arrays, growing deployments needing isolation | Dedicated power feed; sized to your draw | Quote-based | [Request a quote](https://bit.ly/DmiT) |
| **Full Cabinet** | Full cabinet with committed power and bandwidth | Dense, high-power racks; private cages available on request | Committed power sized for high-density deployments | Quote-based | [Request a quote](https://bit.ly/DmiT) |

All three tiers include 24/7 remote hands, hardware install and rack-and-stack, cross-connects to carriers and IXes, and access to DMIT's Premium / Eyeball / Tier 1 network series. Final specifications, power density, and pricing vary by location and capacity, and the colocation page explicitly notes that the published footprints are reference-only — the signed order or contract is what governs.

> **A note on discounts:** DMIT runs periodic promotions on their cloud and VPS products (annual billing discounts, launch offers on specific network series like the LAX Eyeball line), but colocation is custom-quoted, so promo codes generally don't apply to colo deals. If a code is floating around on a third-party coupon site, verify it directly with DMIT sales before assuming it works on a colocation contract.

## If you don't want to own the hardware: DMIT's bare metal and cloud instances

High-density colocation assumes you're bringing your own servers. If you'd rather not ship a rack across the Pacific, DMIT also offers dedicated bare metal and self-service cloud instances in the same three locations, on the same three network tiers.

**Bare metal** is single-tenant physical servers built to spec — AMD EPYC up to 128 cores / 256 threads, DDR4/DDR5 ECC, all-NVMe storage with optional RAID, GPU and accelerator options on request, IPMI access, and custom bandwidth/IP plans. Like colocation, it's quote-based and tailored to your workload. The entry point is 👉 [request a bare metal configuration from DMIT](https://bit.ly/DmiT).

**Cloud instances** are self-service KVM VMs with published pricing. From the Los Angeles page, the Premium Network plans currently run:

| Plan | vCPU | RAM | Storage | Transfer | Port | Price (monthly) |
| --- | --- | --- | --- | --- | --- | --- |
| TINY | 1 | 2GB | 20GB SSD | 1000GB | 1Gbps | $10.90 |
| Pocket | 2 | 2GB | 40GB SSD | 1500GB | 4Gbps | $16.90 |
| STARTER | 2 | 2GB | 80GB SSD | 3000GB | 10Gbps | $34.90 |
| MINI | 4 | 4GB | 80GB SSD | 5000GB | 10Gbps | $62.90 |
| MICRO | 4 | 4GB | 160GB SSD | 7000GB | 10Gbps | $87.90 |
| MEDIUM | 6 | 8GB | 160GB SSD | 15000GB | 10Gbps | $199.90 |

Those are LAX Premium Network prices on their AMD EPYC platforms (AN5 / AN4 / AS3 series, depending on availability). Hong Kong and Tokyo have separate plan ranges — the Hong Kong Premium lineup, for instance, runs from MINI at $149.90/month up to GIANT at $759.90/month on the AN5 series — and the LAX AS3 platform is still being built out, so expect reduced disk performance and a lower SLA there until it matures. To see live plans for a specific location and network series, 👉 [check current cloud instance pricing on DMIT](https://bit.ly/DmiT).

The cloud tier is obviously not "high density" in the colocation sense — it's virtualized, shared hardware. But if your actual goal is "run AI inference near China users without buying GPUs and shipping them to Hong Kong," bare metal is the closer fit, and cloud instances are the budget option for lighter workloads that still want the routing quality.

## Choosing the right network tier for a high-density workload

This is the part where DMIT's setup is genuinely useful for AI/GPU deployments specifically, because the network choice changes your per-GB cost dramatically:

- **Premium Network (CN2 GIA + direct peering):** Best quality into China Mainland. ~15 ms latency from Hong Kong, under 0.1% packet loss. Use this for latency-sensitive China-facing services — real-time inference, financial APIs, live streaming, gaming. Highest cost per GB.
- **Eyeball Network (CMIN2 / CMI + Tier 1):** Reasonable-effort China routing at lower cost. Good for mixed China/global audiences, API backends, SaaS, download mirrors. A practical middle ground.
- **Tier 1 Network (multi-Tbps global backbone, no China optimization):** Most economical. Up to 7.6 Tbps aggregate capacity across Cogent, NTT, GTT, Arelion, Lumen, Tata and others. Use this for backup, archival, bulk transfer, internal tooling, CI/CD, or anything that doesn't need China-specific routing.

For a high-density GPU rig, the honest recommendation is: profile your traffic first. If 80% of your inference requests come from China Mainland, Premium is worth the premium. If you're training models and shipping results back to a US-based team, Tier 1 is dramatically cheaper and the China routing doesn't matter. Eyeball is the answer when you have meaningful but not critical China traffic and you don't want to pay CN2 GIA rates for every byte.

## The actual decision

High-density colocation isn't a commodity purchase. The facility that's right for a 15 kW rack of storage nodes is not the same facility that's right for a 45 kW liquid-cooled GPU cluster, and neither is necessarily the right answer if your real problem is "I need 200 ms inference into Shanghai and my current US-East provider can't get there."

DMIT's specific value is the intersection of carrier-neutral colocation in LA / HKG / TYO with genuine China-optimized routing — the part most general-purpose colo providers either can't do or charge a fortune for. The tradeoff is that pricing is quote-based, so you can't comparison-shop on a public price table the way you can with their cloud instances. If your workload has a China or APAC angle and you want the routing quality without hosting inside China itself, 👉 [start a colocation conversation with DMIT](https://bit.ly/DmiT) and see what a tailored plan looks like for your actual power draw and traffic profile.

If you're not ready to commit to owning hardware, the same network and locations are available through their bare metal and cloud tiers, and the cloud pricing at least is public — so you can validate the routing quality on a $10.90/month TINY plan before you ever sign a colo contract.
