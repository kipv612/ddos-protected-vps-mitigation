# DDoS Protected VPS: What "Free Mitigation" Actually Covers, How Much Attack Volume You Get, and Which Plan Fits

A DDoS-protected VPS scrubs attack traffic upstream, before it reaches your server, and on most entry-level plans the scrubbing stops at Layers 3 and 4. Volumetric floods get dropped. HTTP floods that look like ordinary visitors do not, and those you handle on the box with rate limiting or a WAF. SpinServers' smallest KVM VPS is $12.00/month for 2 vCPU, 2 GB RAM and 40 GB SSD, which is where most single-site buyers should start.

What separates one "included" protection from another is capacity and scope, and neither shows up in the marketing line. Below: the three things "DDoS protected" can mean in a plan description, the work that stays on your side of the network, the full SpinServers VPS lineup with published prices, and how four hosts that do publish mitigation figures compare.

> **Short answer:** for one site, a small API or a VPN endpoint, the KVM 2 vCPU / 2 GB plan at $12.00/month is the sensible starting point. Before ordering, get the mitigation capacity in Gbps from sales in writing, because that number, not the core count, decides whether the plan holds.
>
> 👉 [See the SpinServers KVM VPS lineup and live pricing](https://bit.ly/Spinservers)

## The SpinServers VPS lineup, plan by plan

| Plan | vCPU / RAM / storage | Bandwidth and port | Published price | Order |
| --- | --- | --- | --- | --- |
| KVM 2 vCPU / 2 GB | 2 vCPU, 2 GB DDR4, 40 GB SSD | 1 Gbps port | $12.00/mo | [Order the 2 vCPU plan](https://bit.ly/Spinservers) |
| App Server 4 vCPU / 4 GB | 4 vCPU, 4 GB DDR4, 80 GB RAID-10 SSD | 8 TB, 1 Gbps | On the order form | [Check the 4 vCPU price](https://bit.ly/Spinservers) |
| App Server 6 vCPU / 8 GB | 6 vCPU, 8 GB DDR4, 120 GB RAID-10 SSD | 8 TB, 1 Gbps | On the order form | [Check the 6 vCPU price](https://bit.ly/Spinservers) |
| App Server 8 vCPU / 8 GB | 8 vCPU, 8 GB DDR4, 160 GB RAID-10 SSD | 10 TB, 1 Gbps | On the order form | [Check the 8 vCPU price](https://bit.ly/Spinservers) |
| KVM 12 vCPU / 12 GB | 12 vCPU, 12 GB DDR4, 160 GB RAID-10 SSD | 10 TB, 1 Gbps | $62.00/mo | [Order the 12 vCPU plan](https://bit.ly/Spinservers) |
| Advanced App Server 32 vCPU / 32 GB | 32 vCPU, 32 GB RAM, 500 GB SSD | 20 TB, 1 Gbps | On the order form | [Check the 32 vCPU price](https://bit.ly/Spinservers) |

Two configurations publish a starting monthly figure, $12.00 and $62.00. The rest are priced on the order form, so confirm the live number there before you commit rather than relying on a table anywhere.

One detail that matters more than it looks: **port 25 is closed by default on every SpinServers VPS**, and opening it requires a ticket with a justification, which the company reserves the right to refuse. If you are planning a mail server as part of this deployment, budget for that step and do not assume the ticket will be approved.

## What "DDoS protected" actually covers

The filtering happens upstream of your server, in the provider's network, and it is aimed at traffic volume. Cloudzy spells out the vectors its included mitigation handles: UDP floods, SYN floods, ICMP floods, DNS amplification and NTP reflection, all Layer 3/4 attacks. Then it says the quiet part out loud: application-layer attacks need separate tooling, meaning rate limiting or a WAF you configure on your own server.

That line is the difference between a plan that survives an attack and one that goes down anyway while reporting that mitigation is active. An HTTP flood from a few thousand IPs sends requests that are, individually, perfectly valid. Nothing at Layer 3 looks wrong. The connection counts, the CPU and the database connection pool are what break.

Rad Web Hosting shows how wide the gap gets inside a single product line. Its Standard DDoS Protection tops out at **up to 5 Gbps**, covers Layers 3 and 4, has no Layer 7 protection, basic log-only visibility and no custom traffic rules. Premium goes to **up to 1+ Tbps** and adds an advanced WAF, AI-assisted pattern detection, zero-delay priority handling, real-time attack analytics and priority SLA response. Standard is marketed for small and medium websites, Premium for gaming, VoIP, APIs and e-commerce. Same phrase on the tin, two very different products underneath.

## Is the protection really free?

"Included" is a pricing statement, not a capacity statement, and hosts use it in at least three different ways.

OVHcloud is the most expansive: mitigation is always on, **unmetered**, on every VPS, and the page states it applies no matter the size or duration of the attack, at no extra cost. Cloudzy takes the second route, promising mitigation on every plan "from the $2.48/mo tier to the 64 GB tier" with no add-on and no premium tier, which tells you everyone gets the same volumetric filtering regardless of spend. InMotion Hosting takes a third, positioning protection on every plan so customers do not have to buy extra security tools or configure a platform themselves.

Rad's split tier is the fourth pattern, and the useful one to keep in mind when you read any other host's page. If a provider says "DDoS protected" and stops there, you do not yet know whether you are getting 5 Gbps with no Layer 7 or 1 Tbps with a WAF. Ask, in writing, for the Gbps figure and a yes or no on application-layer filtering. SpinServers does not publish a mitigation capacity figure on its VPS pages, so that is a pre-sales question, not something to infer from the plan specs.

👉 [Compare the SpinServers VPS configurations side by side](https://bit.ly/Spinservers)

## Upstream scrubbing does not replace the firewall on your server

These are two different jobs and the marketing tends to blur them. OVHcloud draws the line cleanly: firewalls and intrusion detection systems focus on preventing unauthorised access, while DDoS protection addresses the problem of overwhelming your server with traffic so it stays available. Cloudzy's version is that upstream mitigation absorbs volumetric floods while the on-server firewall handles application-level filtering.

Practically, that means the protection you are buying keeps the pipe clear. It does not stop a credential-stuffing run against your login form, a scraper hammering a search endpoint, or a badly written plugin eating every PHP worker. With root access, the tools for those live on your side: iptables, nftables, ufw, fail2ban, or a reverse proxy with request limits. Rad goes further and ships its VPS with **no pre-configured port blocks at all**, leaving every TCP and UDP rule to you and recommending the CSF plugin for firewall management.

If you want a clean division of labour: the host filters the flood, you filter the requests.

## Which plan fits your workload

**One site, a small API, a VPN or proxy endpoint.** The 2 vCPU / 2 GB plan at $12.00/month. WireGuard or a single WordPress install with a cache in front does not need more, and paying for cores that sit idle buys nothing against an attack.

**Anything with logins, checkout or a JSON API that accepts POSTs.** Layer 7 is your exposure, and mitigation capacity is secondary to what you put in front of the app. Start at the 4 or 8 vCPU configurations so rate limiting, a WAF and the app itself are not fighting over the same two cores, and budget time for configuring request limits rather than assuming the plan covers it.

**Game servers, DNS and VoIP.** These get hit with volumetric traffic, so the Gbps number matters more than the core count. Rad's own positioning puts gaming and VoIP in the premium tier for exactly this reason.

**Mail.** Remember the port 25 default. A VPS for SMTP needs the ticket approved before you plan around it.

The 32 vCPU / 32 GB / 500 GB configuration with 20 TB of transfer is for build servers, busy application backends or a stack of containers. It is not a DDoS upgrade. Buying more CPU does not increase scrubbing capacity, and if a single site is pushing past 8 vCPU under normal load, the problem is the site.

## What you still have to do on the server

Upstream filtering handles volume. Everything below is yours, on every host:

1. Patch the OS, the web app, its plugins and any third-party tool you installed. Most compromised VPSs were not broken into by a flood.
2. Put a WAF in front of the application and let it watch for abnormal request patterns.
3. Turn on rate limiting per IP per time window, and run Fail2Ban. Neither survives a large attack, but both buy time and cut noise.
4. Close every port you do not serve. HTTP, HTTPS, SSH and nothing else, unless you have a documented reason.
5. Watch traffic graphs and logs. A site that slows to a crawl, mail that stops flowing and a control panel that will not load are the usual first signs that something is incoming. Repeat requests from the same block of IPs are the other.
6. Keep automated off-site backups of files and databases. This is the only control that still works after a bad day.
7. Write the two-line incident plan now: who you contact at the host, and which service you isolate first.

## How SpinServers compares on verified numbers

Prices below are what each provider displayed when checked, including any discount running at the time. Cloudzy's figures reflect a 50% promotion off list prices that may end without notice.

| Provider | Entry price | Mitigation scope | What to watch |
| --- | --- | --- | --- |
| SpinServers | $12.00/mo (2 vCPU, 2 GB, 40 GB SSD) | Not published for the VPS line | Confirm Gbps and Layer 7 in writing |
| Cloudzy | $2.48/mo at 50% off ($4.95 list) | Volumetric L3/L4 on every plan | No L7 included; 14-day money-back; 99.95% SLA |
| Rad Web Hosting | From $15.96/mo | Standard up to 5 Gbps, Premium up to 1+ Tbps | Standard has no L7; the page also claims 1 Tbps per server elsewhere, which conflicts with its own table |
| OVHcloud | Not published in the material reviewed | Unmetered mitigation on every VPS | Capacity described qualitatively, not numerically |
| InMotion Hosting | Not published in the material reviewed | Protection on every plan | No published capacity figure |
| BlockDOS | Plan prices not published in the material reviewed | Claims coverage of UDP, HTTP and SYN floods | No capacity figure; $10/mo security add-on for admin VPN |

Read the table as a lesson in what to ask rather than a ranking. Cloudzy is cheapest by a wide margin and includes filtering on every plan, but it is the same L3/L4 filtering everyone else sells. Rad's entry price is the highest and its Standard tier is the one most buyers would land on, which means 5 Gbps and no application-layer protection despite the "DDoS protected" label on the page. OVHcloud's unmetered promise is the strongest wording available, and it comes with no number attached.

## FAQ

**Will mitigation add latency?** Cloudzy states you should not notice any increase during normal operation and that servers stay online and responsive during an attack. Rad says most users will not notice a significant difference. Both are vendor statements; neither company publishes independent latency measurements, so treat them as claims to test in your first month.

**Can I still run my own firewall on top?** Yes. Cloudzy gives full root access for iptables, nftables, ufw or fail2ban. Rad does not pre-configure any port blocks, so every rule is yours. SpinServers closes port 25 by default and opens it on request.

**Do these plans stop Layer 7 attacks?** No. Volumetric mitigation is the standard inclusion at every host in this piece. HTTP floods, credential stuffing and scraper traffic need rate limiting or a WAF that you configure.

**When is a VPS the wrong product?** When attacks are frequent or sustained enough to affect uptime, when CPU, RAM or bandwidth max out after optimisation, or when you need full hardware control and custom configurations. At that point a dedicated server with contracted scrubbing capacity is the next step, not a bigger VPS.

## Before you order

Two things to settle first. Get the mitigation capacity in writing, as a Gbps figure plus an explicit yes or no on Layer 7. Then confirm the billing cycle and cancellation terms for the exact configuration you picked, because a monthly cycle is the cheapest way to test a network before committing further.

Match the plan to the traffic you actually serve. A single site or small API runs fine on the 2 vCPU / 2 GB plan at $12.00/month. Anything with checkout, logins or a game server should size up and put request filtering in front. If you are already under repeated attack, skip the VPS tier altogether.

👉 [Pick your SpinServers configuration and check today's price](https://bit.ly/Spinservers)
