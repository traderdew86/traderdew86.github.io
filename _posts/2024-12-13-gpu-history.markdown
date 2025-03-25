---
layout: post
title:  "History of modern GPU"
date:   2024-12-13 20:36:54 -0500
image: /assets/images/ati_vs_nvidia.jpg
comments: true
---

# Intro
Today we go over the history of GPUs. The term GPU is widely known as the computing hardware that focuses on rendering graphics, but in the early days they were commonly called video cards.

&nbsp;
# 1990s
The 90s was very important in video card hisotry. Although the concept of a dedicate video processor (as apposed to processing everything in CPU) dates many years back, the 90s was when we saw drastic increase in the video card market and competition. Entering 1990, the major players are Matrox, S3, IBM, Intel, and ATI. At this stage, all video cards are primarily for 2D graphics rendering. Two new players, Nvidia and 3dfx, entered the scene and heated up the battlefield with 3D rendering. Nvidia released NV1 in 95, while 3dfx released Voodoo in 96. While these products each have their own shortcomings, they set the course for the next stage of the evolution - Nvidia Riva 128 (97) and 3dfx Voodoo 2 (98). When ATI released the Rage Pro in 97, the three players are locked into a fierce competition.

All players kept releasing products in an attempt to gain a lead, it was cut-throat. In 98, Nvidia release Riva TNT, and ATI released 2 variants of their Rage 128. 3dfx followed up with Voodoo 3 in 99, then Nvidia released the TNT 2, and ATI showed 3 new high-end Rage 128 cards. However, 3dfx started cracking. Its unique GLIDE API, while well-praised, is being abandoned by developers as the gaming industry transitioned to Microsoft's Direct3D (AKA DirectX) as the standard API. The dominance of Windows in the PC market also played a major role here. 3dfx's reluctance to adopt Direct3D led to large financial losses that kept accumulating.

&nbsp;
## The first GeForce
In 1999, Nvidia released the legendary GeForce 256 (220nm), a card way ahead of its competition in term of performance and features. It is the first of their GeForce series, but more importantly, this gave birth to the buzzword "GPU" as Nvidia's marketing team calls it "world's first GPU".

&nbsp;
## ATI's failed counter attack
To combat the GeForce 256 ATI had a mad idea. Just put 2 processors on the same card, this would double the performance right? Introducing the Rage Fury Maxx (250nm), a single video card with 2 Rage 128 Pro chips. The card would run games on both cores, each core renders frames alternatively. In reality, this ws not that simple. Most software do not support the way ATI set up this dual GPU card, on top of that, the newer Windows (2000 & XP) also cannot take advantage of the cores, causing to it performance similarly to a single Rage 128 Pro in games. This card failed to shake the dominance of the GeForce 256.

&nbsp;
# New millennium
In early 2000s, 3dfx's financial trouble led to bankrupcy. After Nvidia acquired 3dfx's IP, only two players remain. And Nvidia has the edge over ATI.

## ~~Rage 6~~ Radeon
At this point ATI's Rage series is at the 4th iteration, the latest Rage Fury Maxx is a Rage 4 card. Naturally the next iteration would be the Rage 5. But the failed Rage Fury Maxx led ATI to completely scrape the Rage series and start fresh. And viola, the Radeon series is born. The intent here was clear, the rebranded Radeon series would go head to head with the new GeForce series as they both evolve through their iterations.

And the Radeon delivers.

The first Radeon, Radeon DDR/7200 (180nm), launched in April of 2000. Is the card faster than GeForce 256? Well, not only the card not only beats the GeForce 256, it could go toe-to-toe with its next iteration - GeForce 2 (180nm). In multiple games and benchmarks, the first Radeon showed similar FPS or scores as the GeForce 2. Aside from the raw performance, it also introduced HyperZ, which could increase vram performance during game rendering. Though later driver updates from Nvidia improved GeForce 2's performance in many games to give the edge back to Nvidia. Regardless, the impact of the Radeon line became a significant threat to Nvidia.

And this marked the official start of decades long battles between the only two players - team green (Nvidia) and team red (ATI)..

## Live to fight
Nvidia launched GeForce 3 in 2001. Then ATI followed up with the Radeon 8000 series. The comptition continues as both sides trade blows while innovating. It's hard to argue which side came out on top in the following 2 decades (though Nvidia had more market share). Each company has a different focus. Nvidia tends to bring the fastest cards while still providing decent coverage in the mid-performance market. On the other hand, ATI aims to offer the best value, as majority of their cards at the same performance level are usually priced lower. So both teams had armies of strong supporters. In addition, both sides introduced new tech in these years, to name a few:
- Shader Model
- Multi-GPU via SLI/Crossfire
- Supersampled AA
- Tessellation
- Ray tracing
- AI upscaling
- CUDA (maybe ROCm?)

This trend continued until the early 2020s. During this period, ATI was acquired by AMD. But its GPU business was mainly on-track with Nvidia's, so this acquisition had no large impact on the business trajectory. The acquisition gave the GPU maker somewhat of a better financial stability, although AMD also struggled until their come-back in the CPU space with the Ryzen series. Gamers generally benefits from this competition, as we saw dramatic graphical improvements in the past 20 years. The computing performance grows exponentially, while the inflation-adjusted cost stays around the same level.

## Gaming Consoles
PC market is not the only battleground where the two giants fought. They have been fighting fiercely in the console market as well. Since the 6th console generation, console makers began to install GPUs as 3D graphics in gaming becomes proliferate. Successes of a particular console would have large impact on the financials of a GPU maker, though it's debatable if it has any effect on the company's reputation as console makers rarely print GPU logos on their physical console, or in their OS. However, it is worth mentioning that ATI (or now AMD) has more dominance in this world, presumably due to their lower cost of performance and heat generation.
- Gen 6
    - ATI Flipper (180 nm) on Nintendo gamecube
- Gen 7
    - ATI Xenos (various nm) on Xbox 360
    - Nvidia RSX (various nm) on PS3
    - ATI Hollywood (90 nm) on Nintendo Wii
- Gen 8
    - AMD Durango (28 nm) on Xbox One
    - AMD Durango 2 (16 nm) on Xbox One S
    - AMD Scorpio (16 nm) on Xbox One X
    - AMD Liverpool (28 nm) on PS4
    - AMD Liverpool (16 nm) on PS4 Slim
    - AMD Neo (16 nm) on PS4 Pro
    - AMD Latte (40 nm) on Nintendo Wii

## Crypto
As a side note, the crypto mining scene had some impact on GPU pricing. Bitcoin was mined on CPU & GPUs in its early days, while Ethereum's proof-of-work blockchain continued until the proof-of-stake change was implemented in 2022. The rise of crypto market inevitably pushed GPU demand to certain extent, which caused permanent price up-ticks in the late 2010s and early 2020s.

## GenAI craze
The usage of GPUs in data centers saw growth due to AI research and analytics, but PC market has been the primary revenue for Nvidia and AMD until 2022. This all changed after the launch of ChatGPT. In 2022, Nvidia in particular saw huge revenue spike in the data centers. Everyone is trying to get in on this AI race, but Nvidia is the only one selling the tools. Having fast GPUs was not the main advantage, Nvidia has no real competition in the software realm. Their CUDA API gave developers the layer needed to harness all the power from the hardware. All popular AI packages are built on top of CUDA. Software engineers and researchers have been using this for years, switching to other infra would be costly.

Another big advantage is the NVlink. Since each GPU resides on a PCB that has limited VRAM, training LLMs often requires many GPUs running together in parallel, otherwise the model would not fit in VRAM. The cross-GPU communication can become a bottleneck in both training and inference time. NVlink enabled this. As of now there's no alternative, AMD and many partners are developing their version called UALink, but no clue when this would be ready.

&nbsp;
# Current
As of December of 2024, the most modern GPUs on the market are:

## Data Centers
- Nvidia B series (5 nm)
    - B100
    - B200
- Nvidia H series (5 nm)
    - H100
    - H200
    - H800

## Retail
- Nvidia 40 series (5 nm)
    - RTX 4090
    - RTX 4080
    - and more
- Nvidia 30 series (8 nm)
    - RTX 3090
    - RTX 3080
    - and more
- AMD Radeon 7000 series (5 nm)
    - RX 7900-XTX
    - RX 7900 XT
    - RX 7800 XT
    - and more

## Gaming Consoles
- AMD Viola (4 nm) on PS5 Pro
- AMD Oberon (7 nm) on PS5
- AMD Scarlett (6 & 7 nm) on Xbox Series X
- AMD Lockhart (7 nm) on Xbox Series S
- Nvidia GM20B (16 & 20 nm) on Nintendo Switch

&nbsp;
# References
[techpowerup GPU Specs Database](https://www.techpowerup.com/gpu-specs/){:target="_blank"}

[NVIDIA HGX AI Supercomputer](https://www.nvidia.com/en-us/data-center/hgx/){:target="_blank"}

[NVIDIA NVLink](https://www.nvidia.com/en-us/data-center/nvlink/){:target="_blank"}

[History of video game consoles](https://en.wikipedia.org/wiki/History_of_video_game_consoles){:target="_blank"}

[UALink](https://www.tomshardware.com/tech-industry/ualink-consortium-officially-incorporates-nvlink-competitor-headed-by-amd-and-intel-opens-doors-to-contributor-members){:target="_blank"}
