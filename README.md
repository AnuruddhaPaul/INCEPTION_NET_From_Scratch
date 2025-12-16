# InceptionNet (GoogLeNet) from Scratch on MNIST

![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

This repository contains a full implementation of the **GoogLeNet (Inception v1)** architecture built from scratch using PyTorch. The model is specifically adapted to train on the **MNIST dataset** (grayscale handwritten digits).

## 📌 Project Overview

**GoogLeNet**, introduced in the 2014 paper *"Going Deeper with Convolutions"*, revolutionized deep learning by increasing network depth while drastically reducing the number of parameters (approx **6.8M** vs VGG's **138M**).

It achieves this using the **Inception Module**, which performs convolutions with multiple kernel sizes ($1\times1$, $3\times3$, $5\times5$) in parallel and concatenates the results.

### ⚙️ Adaptations for MNIST
The original GoogLeNet was designed for ImageNet ($224 \times 224 \times 3$). To make it work for MNIST, we applied the following changes:
1.  **Input Channels:** Modified the first convolution layer to accept **1 channel** (Grayscale) instead of 3 (RGB).
2.  **Image Resizing:** MNIST images ($28 \times 28$) are resized to **$96 \times 96$**.
    * *Reason:* GoogLeNet performs downsampling (pooling) 4 times. A $28 \times 28$ image would shrink to $1 \times 1$ too early in the network, causing a crash. Resizing to $96$ ensures valid feature maps throughout the deep architecture.
3.  **Output Layer:** The final fully connected layer is modified to output **10 classes** (Digits 0-9).

## 🏗️ Architecture Details

### The Inception Module
The core component of this network. It uses $1\times1$ convolutions for **dimensionality reduction** before expensive $3\times3$ and $5\times5$ convolutions.

| Branch | Operation | Purpose |
| :--- | :--- | :--- |
| **Branch 1** | $1\times1$ Conv | Capture local features / reduce depth |
| **Branch 2** | $1\times1$ Conv $\to$ $3\times3$ Conv | Spatial features with reduced computation |
| **Branch 3** | $1\times1$ Conv $\to$ $5\times5$ Conv | Larger spatial field features |
| **Branch 4** | MaxPool $\to$ $1\times1$ Conv | Pooling with depth reduction |

### Model Summary
* **Total Parameters:** ~6.8 Million
* **Deep Layers:** 22 Layers (with weights)
* **Auxiliary Classifiers:** Removed for simplicity (standard for modern implementations).

## 🚀 Getting Started

### Prerequisites
* Python 3.x
* PyTorch
* Torchvision

### Installation
Clone the repository and install dependencies:

```bash
git clone [https://github.com/your-username/googlenet-mnist-scratch.git](https://github.com/your-username/googlenet-mnist-scratch.git)
cd googlenet-mnist-scratch
pip install torch torchvision


## 📜 References
* **Primary Paper:** Szegedy, C., Liu, W., Jia, Y., Sermanet, P., Reed, S., Anguelov, D., ... & Rabinovich, A. (2015). [Going deeper with convolutions](https://arxiv.org/abs/1409.4842). *Proceedings of the IEEE conference on computer vision and pattern recognition*, 1-9.
