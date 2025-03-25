---
layout: post
title:  "Landscape of GPU compute"
date:   2024-12-05 22:15:37 -0500
image: /assets/images/rainbow_road.jpg
comments: true
---

# Intro
With the recent rise of Gen-AI, the demand for GPU compute power has exploded, fueled by AI, data-heavy tech, and crypto. GPUs are no longer just for gaming, they’re also the engines behind everything from running AI models to powering scientific breakthroughs. Here I sum up the GPU compute landscape

&nbsp;
# Supply Side
There are two distinct groups of suppliers - hardware makers and compute providers.

## Hardware Makers
It is no doubt that Nvidia is the king of GPU in 2024. AMD is playing the catch-up game. But is that all?

Unfortunately yes, they are the only meaningful GPU makers when it comes to AI compute. Google has TPUs, Apple has ARM-based SoC, and Intel has AI chips, but they are nowhere near the dominance of the big two. In fact, AMD is only barely relevant at the moment as Nvidia had a dominant 95%+ market share in data center GPUs during 2023, but AMD is the only company that has a slim chance at shaking Nvidia's dominance due to their experience in GPUs, Dr. Su's leadership and their talent pool.

## Compute Providers
The providers allow users the access the power of the GPUs, primarily through some cloud service. The biggest players are:
- AWS
- Azure
- GCP
- Alibaba Cloud
- Oracle
- IBM

There are also a few smaller players that caught my attention:
- andromeda.ai
- vast.ai
- LambdaLabs
- tensordock
- huixingyun
- SFcompute

Cloud compute prividers are considered hyperscalers as most of them offer services to quickly scale up/down compute capacity. It is also worth mentioning that some large firms such as Meta and Tesla have in-house GPU servers, which makes it hard to gauge the computing power. But they are also not part of compute landscape as they likely will not open their servers to public. 

&nbsp;
# Demand Side
The demand side is interesting. I think there are three groups here.

## play2win
The launch of ChatGPT in 2022 sent shockwaves across the world, which led to a few notable companies rushing to a race for AI dominance. These specific firms are all trying to gain a strong-hold in a fiercesome battlefield. Each has sizable funding to fight the fight. These companies are playing to win at all cost:
- OpenAI
- Meta
- Google
- Anthropic
- HuggingFace
- Microsoft
- xAI

## Old friends
There's another group of companies that are using compute for various purposes. These companies are not strangers to AI/ML, but are greatly increasing compute usage to explore opportunities in Gen-AI. 
- AI-related tech firm
- Defense
- Medical
- Hedge fund

## Retail
Last and least, the retail consumers AKA gamers. This group used to be the target audience of GPU sales, priding themselves as either team green or team red, showing hard-core overclock on nitrogen cooled hardware just to squeeze out that extra 2fps to win some short-lived bragging rights online. We are the reason GPUs still existed to this day. The demand is still growing, but the raw power pales in comparison to what AI consumes today.

&nbsp;
# References
[Visualizing Nvidia Revenue by Product Line](https://www.visualcapitalist.com/nvidia-revenue-by-product-line/){:target="_blank"}

[Nvidia data-center market share](https://www.hpcwire.com/2024/06/10/nvidia-shipped-3-76-million-data-center-gpus-in-2023-according-to-study/){:target="_blank"}

[Cloud Market Shares](https://www.statista.com/chart/18819/worldwide-market-share-of-leading-cloud-infrastructure-service-providers/){:target="_blank"}

