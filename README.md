# dedicated server rental: How to Compare Real Prices, Skip Hidden Setup Fees, and Pick the Right Bare Metal for Your Workload

Renting a dedicated server is one of those purchases where the sticker price lies by omission. The headline number is usually real. The total cost — setup fees, prepay discounts you didn't notice, DDoS protection that turns out to be a paid add-on — only surfaces after you've read three pages of fine print or already handed over a card.

This guide does the boring part. We pulled the current listings from five hosts that rank for this exact search, checked what their prices actually include, and put them next to Vultr's Bare Metal line, which attacks the same problem from a different angle: physical, single-tenant servers you can deploy and destroy from a cloud console, with no contract and no sales call.

> **Quick picks**
>
> - **Most readers:** [👉 See Vultr's current Bare Metal plans and prices](https://www.vultr.com/products/bare-metal/?ref=7268283) — single-tenant physical servers starting at **$120/month**, deployed like a cloud instance, billed monthly with no lock-in.
> - **Lowest entry price:** BeeHosting's Intel Atom box in Paris or Amsterdam at €32.49/month — fine for lightweight self-hosted projects, underpowered for anything serious.
> - **Most hardware per dollar:** Rabisu's M1007 ECO at $44/month — an older Xeon, but 64 GB of ECC RAM and a 10 Gbps port at that price is hard to argue with.

## What you're actually renting

A rented dedicated server is a complete physical machine in a data center, reserved for you alone for the length of the lease. Every core, every gigabyte of RAM, every disk, and the network port work only for your workloads. You get root access, and on most traditional hosts you also get IPMI or KVM access — a remote console wired directly to the motherboard, useful when an OS install goes sideways.

When does renting physical hardware actually pay off? A few cases come up again and again:

- **Compliance.** Frameworks like PCI-DSS, HIPAA, and ISO 27001 can require bare-metal isolation that a shared hypervisor can't give you. LikeVPS markets its dedicated line specifically for this.
- **High-load web and databases.** With no neighbors on the hardware, performance stays predictable during traffic spikes — no "noisy neighbor" problem.
- **Game and voice servers.** KernelHost positions its lineup around exactly this, which is why its plans lean on high-clock desktop CPUs.
- **Big data clusters.** Hadoop, Spark, and Elasticsearch nodes want full disks and full memory without virtualization overhead.

When does it *not* pay off? For most small sites and side projects, never. A VPS at single-digit monthly prices — LikeVPS's own VPS line starts at $9.60 — covers the majority of workloads people bring to dedicated hardware. Renting a full machine for a blog is paying for an empty office building to house one desk.

## Vultr's Bare Metal plans and prices

Vultr rents its dedicated hardware under the **Bare Metal** name, and the current entry point is an Intel E3-1270v6 (4 cores / 8 threads at 3.8 GHz, 32 GB RAM) at **$120/month**. The lineup above that scales through Xeon and EPYC configurations:

| Plan | CPU | RAM | Storage | Monthly |  |
| --- | --- | --- | --- | --- | --- |
| E3-1270v6 | 4c/8t @ 3.8 GHz | 32 GB | 2× 240 GB SSD | $120 | [ Order E3-1270v6](https://www.vultr.com/products/bare-metal/?ref=7268283) |
| E5-2650v4 | 12c/24t @ 2.2 GHz | 64 GB | 2× 480 GB SSD | $245 | [ Order E5-2650v4](https://www.vultr.com/products/bare-metal/?ref=7268283) |
| 2× E5-2680v4 | 28c/56t @ 2.4 GHz | 128 GB | 2× 960 GB SSD | $340 | [ Order 2× E5-2680v4](https://www.vultr.com/products/bare-metal/?ref=7268283) |
| EPYC 7402P | 24c/48t @ 2.8 GHz | 128 GB | 2× 1.92 TB NVMe | $495 | [ Order EPYC 7402P](https://www.vultr.com/products/bare-metal/?ref=7268283) |

Dual-socket EPYC configurations sit above these on the same page. One caveat worth repeating: Vultr refreshes this lineup as new CPU generations arrive, so treat the table as a snapshot and verify specs on the live page before ordering — [👉 here's Vultr's live Bare Metal pricing page](https://www.vultr.com/pricing/?ref=7268283).

What makes Vultr's approach different from the five traditional hosts compared below is operational, not financial. You order from the same console, API, CLI, or Terraform setup you'd use for a cloud VM. Standard Linux images install automatically, the machine appears in your account when provisioning finishes, and when you're done you destroy it and stop paying — no contract, no email thread with a sales team. If you run ephemeral or multi-region infrastructure, that workflow alone justifies the premium over a $44 legacy-Xeon box elsewhere.

The honest limitation: Vultr sells fixed SKUs. There's no configurator for custom disk layouts, no GPU options on this line, and you don't get raw IPMI handover the way traditional dedicated hosts provide. If you need 1 TB of RAM, a specific GPU, or hands-on out-of-band control, a custom-build host fits better than Vultr. If you need a clean physical server in a known configuration, deployed in minutes, it's the smoother path.

## How five other hosts compare

Entry pricing across the five hosts ranking for this search ranges from €32.49 to $318 a month, and the differences are mostly about hardware generation and terms, not quality. Here's what the cheapest usable plan at each host actually gets you:

| Host | Entry plan | What you get | Entry price | Terms worth knowing |
| --- | --- | --- | --- | --- |
| BeeHosting | Intel Atom C2350 | 2c/2t @ 1.7 GHz, 4 GB DDR3, 1× 128 GB SSD, 1 Gbit/s, Paris or Amsterdam | €32.49/mo | IPMI/IPKVM included; −10% on 3-month, −15% on 12-month prepay |
| Rabisu | M1007 ECO | Xeon E5-2650v2, 64 GB DDR3 ECC, 2× 250 GB SSD (hardware RAID), 10 Gbps | $44/mo | Stock configs deploy in 1–4 h; free DDoS mitigation |
| KernelHost | Prof-VDS-1 | 10 EPYC cores, 48 GB DDR4 ECC, 200 GB NVMe (RAID-1/10), 2× 1 Gbps, Frankfurt | €59.99/mo | KVM-based virtual dedicated — see the note below |
| IHC | Dedic-e8 | Xeon E3-1230, 8 GB RAM, disks of your choice, Moscow | ≈ $93.75/mo | Moscow stock servers activate in minutes; EU delivery carries extra fees |
| LikeVPS | Entry stock config | 32 vCore, 64 GB RAM, 2× 960 GB NVMe, Netherlands or USA | from $318/mo | No identity verification, crypto accepted, 14-day refund |

Three details in that table deserve unpacking, because the listings themselves blur them.

KernelHost's €59.99 tier is a **virtual** dedicated server — a KVM slice of an EPYC host, not a whole machine. Its first true bare metal plan starts at €134.99 (Ryzen 7 5700X, 64 GB DDR4, 2× 512 GB NVMe). That's not a knock on the product; it's a well-specced line with 3.2 Tbps Arbor DDoS protection in a TÜV Tier3+ certified Frankfurt data center. But if you search for a dedicated server and stop reading at the price, you'll think you found bare metal at a price that doesn't exist.

LikeVPS's own page quotes two different entry prices — the header says from $318/month while a comparison block lower down says from $270/month. Assume the higher figure until you reach checkout. Its stock configs (up to 32 vCore / 384 GB RAM / 4× 960 GB NVMe) deploy in 1–4 hours; custom builds, which can include GPUs and up to 1 TB of RAM, take 3–14 days.

IHC's cheapest Moscow plans are genuinely cheap for what they are, and its E-2236 config (64 GB, 2× 480 GB SSD, ≈$368.63) is a sensible mid-range option — but read the location asterisk before ordering.

## The fine print that changes the math

Three of the five listings bury terms that directly change what you'll pay or wait.

**IHC's EU location costs extra, in both money and time.** The Amsterdam option carries a one-off installation fee of 5,250 ₽ on top of the monthly price, and approximate installation time after payment is ten days. Moscow stock servers, by contrast, activate within minutes. If you're comparing IHC's EU pricing against Rabisu's 1–4 hour deployment or Vultr's console-based provisioning, the wait is part of the price. IHC does soften the annual bill: pay for one year and you get twelve months for the price of ten.

**BeeHosting's prepay ladder is the cheapest effective rate on this list.** The Atom box lists at €34.20, drops to €32.49 with the standard discount, and the 12-month prepay total of €348.84 works out to an effective **€29.07/month**. Nothing else we checked comes close at that floor — just make sure a 2-core Atom at 1.7 GHz can actually run what you plan to put on it. For context, the same host's Xeon E3-1220 (4c/4t @ 3.1 GHz, 8 GB, 2× 1 TB HDD) sits at €36.99 and is a more realistic machine for self-hosting several services.

**Rabisu's DDoS numbers don't match its own pages.** The marketing banner advertises mitigation "up to 10 Tbps+," while the FAQ states 3.8 Tbps at no additional cost. When a vendor's own materials disagree, plan around the smaller number. The same page also quotes both 99.99% and 99.95% uptime — the SLA figure to hold them to is 99.95%.

KernelHost is the cleanest of the bunch on this front: no setup fee, DDoS protection specified at 3.2 Tbps Arbor, and unlimited traffic on a fair-use basis stated plainly on each plan.

## Which server to rent, by workload

Match the hardware to the job and most of this comparison resolves itself:

- **Side projects and light self-hosting.** Don't rent dedicated hardware at all — take a VPS and pocket the difference.
- **Game servers, voice servers, anything latency-sensitive that loves clock speed.** Go Ryzen. KernelHost's 7700X plan (5.4 GHz boost, 64 GB DDR5) runs €139.99, its 7950X3D flagship €169.99; Rabisu's 5700X config is $119 and its 5950X tier $159.70.
- **Compliance-driven workloads.** True bare-metal isolation is the requirement, so the KVM-based tiers are out. LikeVPS builds its dedicated line around this exact use case; KernelHost's certified Frankfurt facility suits audit-heavy European buyers.
- **Bulk RAM and disk on a budget** — analytics nodes, media archives, backup targets. Rabisu's ECO line is the value play: $105/month buys 512 GB of RAM and 2× 2 TB SSD with hardware RAID.
- **Infrastructure you treat as cattle, not pets.** Spinning servers up and down through an API across a 32-location cloud network is the whole point of Vultr Bare Metal — [👉 compare Vultr's Bare Metal plans against its cheaper cloud instances](https://www.vultr.com/products/bare-metal/?ref=7268283) and see where your workload lands.

## FAQ

**How fast is a rented dedicated server actually delivered?**
Minutes to two weeks, depending on who you pick. IHC's Moscow stock servers activate within minutes of payment; Rabisu and LikeVPS provision stock configs in 1–4 hours; Vultr hands you the machine through its console the way a VPS arrives. The slow lanes are custom builds (3–14 days at LikeVPS) and IHC's EU location (about ten days plus a setup fee).

**Is DDoS protection included in the rental price?**
Often, but the capacity varies wildly and isn't always honestly advertised. KernelHost includes 3.2 Tbps Arbor protection on every plan; LikeVPS enables multi-layer L3/L4 protection plus basic L7 filtering by default; Rabisu includes mitigation free per its FAQ (3.8 Tbps — not the 10 Tbps+ in its banner). Ask for the mitigation capacity in writing before you order from anyone.

**What operating systems can I run?**
Nearly anything. IHC lets you mount your own ISO image; LikeVPS permits any OS including hypervisors like Proxmox and ESXi; Rabisu covers Windows Server 2019/2022 plus the usual Linux distributions and custom ISOs; Vultr installs standard Linux images automatically and supports bringing your own ISO across its platform.

**Do any of these hosts offer a refund window?**
LikeVPS does, and it's unusually clean: a full refund within 14 days of payment, no questions asked. IHC's annual billing (12 months for the price of 10) changes the calculus differently — you save money but commit upfront. For the others, assume prepaid months are spent months unless support tells you otherwise.

## Before you click order

One last pass through the decision, mapped to what you actually need:

- Want a known-spec physical server, deployed and deleted through an API, with monthly billing and no contract? That's the Vultr Bare Metal workflow, and the $120 E3-1270v6 is the plan to start with — [👉 start with Vultr's E3-1270v6 Bare Metal plan](https://www.vultr.com/products/bare-metal/?ref=7268283).
- Want maximum hardware per euro and don't mind older CPUs? Rabisu's ECO line or BeeHosting's annual prepay rate.
- Need high clock speeds for game servers? KernelHost's Ryzen plans, from €134.99 for true bare metal.
- Need custom configs, GPUs, or anonymity-friendly payment? LikeVPS — just budget for the 3–14 day custom-build wait.

And one concrete pre-order checklist, regardless of host: confirm whether your chosen location carries a setup fee, confirm the DDoS mitigation capacity in the FAQ rather than the banner, and confirm the delivery estimate for your specific configuration. Five minutes of checking beats ten days of waiting for a server you needed yesterday.
