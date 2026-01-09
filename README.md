### From Lightweight CNNs to SpikeNets: Benchmarking Accuracy–Energy Tradeoffs with Pruned Spiking SqueezeNet  

*Code will be released after conference proceedings*

---

## Overview

This repository contains the official implementation of:

**“From Lightweight CNNs to SpikeNets: Benchmarking Accuracy–Energy Tradeoffs with Pruned Spiking SqueezeNet”**

Lightweight CNNs such as ShuffleNet, MixNet, MnasNet, and SqueezeNet are widely used for mobile/edge deployment.  
We benchmark their **converted spiking variants (SNNs)** under a unified pipeline using **LIF neurons + surrogate gradients**.

We further introduce **SNN SqueezeNet-P**, a *structured-pruned* spiking version of SqueezeNet that:

- ⚡ Improves CIFAR-10 accuracy by **+6%**
- 📉 Reduces parameters by **19%**
- 🔋 Achieves **88.1% lower energy consumption** than its CNN counterpart

> ** Code Release Notice:**  
> The full source code will be released **after conference proceedings** in accordance with publication policy.

---

##  Benchmark Summary

### **Datasets**
- CIFAR-10  
- CIFAR-100  
- TinyImageNet  

---

##  Table 1 — SNN Model Statistics  

| Dataset | Model | Acc | F1 | AC (k) | MAC (k) | Params (k) | Energy (mJ) |
|---------|-------|-----|----|--------|----------|------------|--------------|
| CIFAR-10 | SNN-ShuffleNetV2 | 0.40 | 0.40 | 93 | 894 | 911.0 | 0.0042 |
| CIFAR-10 | SNN-Xception | 0.75 | 0.75 | 1510 | 96,300 | 1025.0 | 0.4444 |
| CIFAR-10 | SNN-MnasNet | 0.78 | 0.77 | 3430 | 12,130 | 151.8 | 0.0589 |
| CIFAR-10 | SNN-MixNet | 0.73 | 0.73 | 523 | 506.9 | 84.9 | 0.0028 |
| CIFAR-10 | SNN-SqueezeNet | 0.75 | 0.74 | 16,610 | 4470 | 736.5 | 0.0355 |
| CIFAR-10 | **SNN-SqueezeNet-P (Ours)** | **0.81** | **0.81** | 11,200 | 4230 | 599.1 | **0.0295** |
| CIFAR-100 | SNN-ShuffleNetV2 | 0.12 | 0.10 | 163 | 894.6 | 1000.0 | 0.0043 |
| CIFAR-100 | SNN-Xception | 0.36 | 0.34 | 1780 | 96,310 | 1025.0 | 0.4446 |
| CIFAR-100 | SNN-MnasNet | 0.49 | 0.48 | 3050 | 12,930 | 163.5 | 0.0622 |
| CIFAR-100 | SNN-MixNet | 0.44 | 0.43 | 862 | 506.9 | 108.0 | 0.0023 |
| CIFAR-100 | SNN-SqueezeNet | 0.47 | 0.47 | 20,790 | 4470 | 782.6 | 0.0393 |
| CIFAR-100 | **SNN-SqueezeNet-P (Ours)** | 0.54 | 0.53 | 13,490 | 4230 | 645.3 | 0.0316 |
| Tiny ImageNet | SNN-ShuffleNetV2 | 0.11 | 0.09 | 642 | 3780 | 1110.0 | 0.0180 |
| Tiny ImageNet | SNN-Xception | 0.23 | 0.21 | 6440 | 385,630 | 10,460.0 | 1.7797 |
| Tiny ImageNet | SNN-MnasNet | 0.38 | 0.37 | 12,040 | 51,690 | 176.4 | 0.2486 |
| Tiny ImageNet | SNN-MixNet | 0.34 | 0.33 | 2000 | 203.0 | 133.7 | 0.0093 |
| Tiny ImageNet | SNN-SqueezeNet | 0.41 | 0.40 | 80,094 | 17,880 | 833.9 | 0.1543 |
| Tiny ImageNet | **SNN-SqueezeNet-P (Ours)** | 0.45 | 0.44 | 51,970 | 16,920 | 696.6 | 0.1246 |

---

##  Table 2 — CNN vs SNN Comparison (CIFAR-10)

| Model | CNN Acc | SNN Acc | ΔA | CNN Energy (mJ) | SNN Energy (mJ) | Energy Ratio (×) |
|-------|---------|---------|----|-----------------|-----------------|-----------------|
| ShuffleNetV2 | 70 | 40 | 30 | 0.010 | 0.004 | 2.5 |
| Xception | 79 | 75 | 4 | 2.44 | 0.444 | 5.5 |
| MnasNet | 83 | 78 | 5 | 0.113 | 0.059 | 1.9 |
| MixNet | 82 | 73 | 9 | 0.047 | 0.003 | 15.7 |
| SqueezeNet | 81 | 75 | 6 | 0.252 | 0.036 | 7.0 |
| **SqueezeNet-P (Ours)** | 82 | 81 | 1 | 0.168 | 0.030 | 5.6 |

---

##  Table 3 — Ablation Study: Fire Module Pruning (CIFAR-10)

| Schedule | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | Acc | Params | Energy (mJ) |
|----------|----|----|----|----|----|----|----|----|-----|--------|--------------|
| Baseline | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | 0.75 | 736,500 | 0.0355 |
| Head-1 | ✓ | ✓ | ✓ | ✓ | – | – | – | ✓ | 0.77 | 559,080 | 0.0241 |
| Head-2 | ✓ | ✓ | ✓ | ✓ | – | – | ✓ | – | 0.77 | 376,220 | 0.0257 |
| Tail-1 | ✓ | – | – | ✓ | ✓ | ✓ | ✓ | ✓ | 0.78 | 673,720 | 0.0304 |
| Tail-2 | ✓ | – | ✓ | – | ✓ | ✓ | ✓ | ✓ | 0.79 | 621,660 | 0.0291 |
| Alt-1 | ✓ | – | ✓ | – | ✓ | – | ✓ | – | 0.79 | 362,030 | 0.0260 |
| Alt-2 | – | ✓ | – | ✓ | – | ✓ | – | ✓ | 0.76 | 363,050 | 0.0226 |
| **Ref-1 (Ours)** | – | – | ✓ | – | ✓ | – | ✓ | ✓ | 0.81 | 599,130 | 0.0295 |
| Ref-2 | ✓ | – | ✓ | ✓ | ✓ | – | ✓ | ✓ | 0.79 | 735,950 | 0.0279 |

---

##  Pipeline Summary

### 1. ANN → SNN Conversion
- ReLU → **LIF neurons**
- Surrogate gradient training
- Threshold balancing to maintain activations

### 2. Lightweight CNN Backbones
- ShuffleNetV2-0.3×  
- MnasNet-B1  
- MixNet-S  
- SqueezeNet  

### 3. Pruning Strategy
- Structured pruning of **Fire modules**  
- Retains only {F4, F6, F8, F9} for best accuracy/energy tradeoff  
- Generates **SNN SqueezeNet-P**

---

##  Code Release

>  The full source code will be released after WACV 2026 proceedings.

---

##  Contact

**Mehedi Ahamed** — mehedi.ahamed@seu.edu.bd

---

