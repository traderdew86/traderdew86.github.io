---
layout: post
title:  "How GPU works"
date:   2025-01-03 22:50:08 -0500
image: /assets/images/nvidia_a100.jpg
comments: true
---

# Intro
The purpose of this page is to provide some details on how a GPU works. The depth of this article is limited by personal experience and research. We will use the RTX 4090 as example, since this is the top-end consumer grade GPU, and has been well-known by the community. Some parts of this page do not apply to AMD GPUs.
![rtx4090](../../../assets/images/rtx4090official.jpg)

&nbsp;
# The simple stuffs
The GPU is a physical card that's made up of many components.
- Cooler
- Output ports
- Power delivery
- PCB
- PCIe connector
- VRAM
- GPU die

![gpu parts](../../../assets/images/gpu_parts.jpg)

Some of the components are relatively simpler comparing to the few, and we will cover these first.

## Cooler
Usually the largest and most visible part on the GPU. The main purpose of the cooler is to manage the temperature of the electrical components, primarily the GPU die and VRAM. The cooler consists of aluminum fins acting at heatsink, together with a vapor chamber that directly touches the GPU die, would help spread out the heat over a much larger surface. The attached fans increase airflow in the heatsink to help the heat dissipate. Some models even have water cooler to divert the heat toward a radiator that's attached to the outer edge of a case, achieving faster cooling and lower noise. Some models may have RGB lights or other designs to improve visuals.

## Output ports
At the end of the GPU, we find a few output ports. It varies by model, but the ports usually consists of some display ports and HDMI ports.

## Power delivery
The GPU requires a lot of power to run. The 4090 is rated at 450W TDP, and it cannot get all this power through the PCI slot. There is an additional 12VHPWR connector that directly draws power from the power supply unit.

## PCB
The PCB(Printed Circuit Board) houses all components. Similar to the motherboard, the PCB serves as the skeleton to connect all compoenents of the GPU

## PCIe connector
The interface between GPU and CPU. The card is physically placed inside the PCIe slot of the motherboard, where all data is transferred using this connector. The interface allows 31.508 GB/s of data transfer.

## VRAM
VRAM is a dedicated high speed memory on GPU. A typical GPU workload starts with VRAM. CPU loads all the data onto VRAM through the PCI-e BUS, then cores on GPU reads the data from VRAM to perform their tasks. The results are saved onto VRAM, with some being sent to the video output as frame data, which is ultimately displayed on screen. VRAM has a much higher bandwidth comparing to RAM, this is the primary reason large scale parallelism can be achieved on GPU but not CPU.

Naturally, games running higher resolution would need bigger VRAM. Games with more complex models, textures, and other visual effects also need more VRAM. Having low VRAM may lead to some parts of the game not loading objects or textures correctly. In AI, models with more parameters require more VRAM to load all the weights. Some AI architecture such as transformers have minimum VRAM requirement as it needs the entire model loaded to run inference.

RTX 4090 has 24GB of VRAM. This enables very good gaming performance at 4K resolution, typically with graphics at max or near-max setting for modern games. It also allows running some LLMs locally, depending on model size and quantization. Some popular ones are gemma2-27b-Q4, Mistral-7B

## GPU die
Sitting in the middle of the PCB is the GPU, model AD102. According to offcial whitepaper, the AD102 has 16384 CUDA Cores, 128 RT Cores, and 512 Tensor Cores.

### CUDA Core
A CUDA core is a small processoring unit designed to run computations in parallel. The cores generally run 32-bit floating point operations, but some cores can perform both floating and integer operations. Graphical operations primarly use floating point calculations, but for some integer operations, they are handled by the CUDA cores capable of integer operations.

The CUDA core performs Fused Multiply and Add (FMA) operations every clock cycle, which is essentially 1 multiply and 1 add operations. FMA counts as 2 operations. With 16384 of these CUDA core on a single AD102 die, and running at the 2.52 GHz clock speed, the GPU can perform 2x16384x2.52x10<sup>9</sup> = 82.57536x10<sup>12</sup> floating point (32-bit) operations per second, or simply 82.6 TFLOPS. This is one simple performance measurement of a GPU.

### RT Core
An RT (Ray-Tracing) core is a specialized core to run ray tracing algorithm. This process is primarily used in games to render realistic looking light and reflection. The renaming from GTX to RTX series is influenced by the introduction of RT cores.

However, there is no noticeable usage in AI.

### Tensor Core
A tensor core is a specialized core aiming to run matrix operations very quickly. This is crucial for AI, as majority of the neural network calculations are matrix multiply-and-accumulate (MMA) operations. Tensor core was introduced in 2017 with NVidia's Volta lineup, and later landing on the RTX 20-series for consumers.

Their primarily use case in gaming was DLSS (Deep Learning Super Sampling). Games were rendered at a lower resolution than normal, then an AI model would upscale each image to the desired resolution. This drastically reduced traditional rasterization run by CUDA & RT cores, shifting some workload onto these specialized tensor cores, while at the same time introducing small blurriness. DLSS 3 added frame-gen that uses AI models to generate artificial frames at the cost of some small input latency and visual artifacts.

Similar to CUDA cores, tensor cores perform FMA operations, but on matrices (aka GEMM). If A is a matrix of dimension m by k, and B is a k by n matrix, then the resulting product C would have dimension m by n, while the entire multiplication will take m*n*k FMAs. For example a 16x16 matrix multiplied by another, would result in 16x16x16 FMAs = 4096 FMAs = 8192 operations. Performance here is dependent on input size, tensor cores on AD102 work best on data with dimensions that are multiples of 16 bytes. According to NVidia, each tensor core achieves 128 FMA per clock on FP16, here I assume the 128 FMA comes from matrix multiplication of 4x4 and 4x8: 4x4x8 = 128 FMA/core/clock. As a result, the tensor performance on a 4090 is 128 FMA/core/clock x 512 cores x 2.52 GHz = 330.3 TFLOPS. 

### Streaming Multiprocessors
A Streaming Multiprocessors (SM) is a collection of CUDA, RT, Tensor cores, along a few other supporting hardware. As a result, an SM can be seen as an atomic unit inside a GPU, or a "mini-GPU" inside the GPU. Each unit has its own cache (L1 cache) that it can utilize to optimize computations. Each SM also schedules workload internally to limit data transfer across SMs, improving overall performance.

In a 4090, each SM contains 128 CUDA cores, 1 RT core, and 4 tensor cores. There are 128 SMs total. SMs are grouped into TPC and GPCs, each level adds some hardware to optimize data flow across the sub-tiers, but the idea remains unchanged. GPC is the highest level, and RTX 4090 has 11 GPCs.

&nbsp;
# Workflow
NVidia explains well in this graph
![graphic_pipeline](../../../assets/images/graphic_pipeline.jpg)

CPU first places various assets into the VRAM, these assets typically include objects (geometry) and textures. To render a frame, all 3D objects in the scene would be projected onto a 2D plane, this is what the T&L (a.k.a TCL) process is doing. Once this is done, all objects are converted into polygons, which are simply triangles formed by the vertices of the objects. Rasterization process then convert these vector-form polygons into pixelated projections, while at the same time applying colors and textures to these pixels. This would yield a complete image (frame) which is sent to the frame buffer of the VRAM, and then  displayed by the monitor.

While most of the operations are not complex, parts of the process needs to be done for each pixel generated, and pixel count is generally in the millions. For example a 1080p resolution would have about 2.1 million pixels. And this is why large scale parallelism is required for GPU. On top of that, running additional operations such as ray tracing would require more calculations. The workflow is done repeatedly to achieve a playable frame rate, typically 60+ frames/sec (FPS).

In AI, calculations are defined by each model's architecture so there are many varieties. But neural network typically involves many matrix multiplications, which the CUDA & Tensor cores excel at. The large bandwidth in VRAM also plays a vital role in speeding up read/write operations at each stage of the neural network.

&nbsp;
# References
[4090 Teardown](https://www.youtube.com/watch?v=5tz4bYa3vkE){:target="_blank"}

[NVIDIA ADA GPU ARCHITECTURE](https://images.nvidia.com/aem-dam/Solutions/Data-Center/l4/nvidia-ada-gpu-architecture-whitepaper-v2.1.pdf){:target="_blank"}

[Tensor Core Requirements](https://docs.nvidia.com/deeplearning/performance/dl-performance-matrix-multiplication/index.html#requirements-tc){:target="_blank"}

[Ray Tracing Algorithm](https://en.wikipedia.org/wiki/Ray_tracing_(graphics)){:target="_blank"}

[Graphics Pipeline Performance](https://developer.nvidia.com/gpugems/gpugems/part-v-performance-and-practicalities/chapter-28-graphics-pipeline-performance){:target="_blank"}