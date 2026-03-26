# DNS Protocol Performance Analysis

Analysis and visualization of DNS resolution and web performance across five encrypted DNS protocols — **Do53 (UDP/TCP)**, **DoT**, **DoH**, and **DoQ** — measured from 7 AWS vantage points worldwide.

This repository contains the Jupyter notebooks and data used to produce the results of my [Master's thesis](https://github.com/Lucapaulo/dns-analysis/tree/master/report) at TU Munich.

## What I Built

I designed and ran a large-scale measurement study comparing DNS protocol performance:

- Measured DNS resolution times for **100+ public resolvers** across 5 protocols
- Deployed measurement infrastructure on **7 AWS EC2 regions** (US East/West, EU Central, Africa South, Asia Pacific NE/SE, South America East)
- Analyzed **web page load times** (Top 12 Tranco sites) to quantify the real-world impact of DNS protocol choice on browsing performance
- Built a custom testbed to isolate DNS-related latency from other page load factors

## Key Findings

- DoQ (DNS over QUIC) achieves the lowest resolution times in most scenarios, especially benefiting from 0-RTT connection resumption
- DoH and DoT add measurable overhead compared to unencrypted DNS, but the gap narrows with connection reuse
- Geographic distance to the resolver has a larger impact on performance than protocol choice
- Web page load times are only marginally affected by DNS protocol, since DNS resolution is a small fraction of total load time

## Notebooks

| Notebook | Thesis Section | Description |
|----------|---------------|-------------|
| [`Performance.ipynb`](Performance.ipynb) | §5.1.1 – 5.1.4 | DNS resolution time analysis across all protocols, resolvers, and vantage points |
| [`Performance-Top5.ipynb`](Performance-Top5.ipynb) | §5.1.5 | Focused comparison of the top 5 resolvers |
| [`Meta.ipynb`](Meta.ipynb) | §5.1 (resolver list) | Resolver metadata and selection criteria for DNS measurements |
| [`Web-Performance.ipynb`](Web-Performance.ipynb) | §5.2.1 – 5.2.5 | Page load time analysis (Top 12 websites × 5 protocols × 7 regions) |
| [`Web-Performance-Testbed.ipynb`](Web-Performance-Testbed.ipynb) | §5.2.6 | Controlled testbed measurements isolating DNS latency |
| [`Meta-Web.ipynb`](Meta-Web.ipynb) | §5.2 (resolver list) | Resolver metadata for web performance measurements |
| [`Vantage-Points-Map.ipynb`](Vantage-Points-Map.ipynb) | Fig. 4.1 | World map visualization of the 7 AWS vantage points |
| [`Compare-Misc.ipynb`](Compare-Misc.ipynb) | — | Cross-vantage-point comparison (supplementary, not in thesis) |

## Tech Stack

- **Analysis**: pandas, NumPy, SQLite
- **Visualization**: matplotlib
- **Network**: pyasn (IP-to-ASN mapping)
- **Infrastructure**: AWS EC2 (7 regions), custom Go-based [measurement tool](https://github.com/Lucapaulo/dns-measurements) and [DNS proxy](https://github.com/Lucapaulo/dnsproxy)
