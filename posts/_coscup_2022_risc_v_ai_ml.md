---
title: Building RISC-V AI/ML Solutions
description: A note about COSCUP
date: 2022-07-30
tags:
  - posts
layout: layouts/post.njk
---

# Building RISC-V AI/ML Solutions

- This my first to attend COSCUP and this is my note about the talks from SiFive.

- Speaker
    - Hong-Rong Hsu
        - SiFive technical Head
        - AI runtime/system software 

## Intro of SiFive
- From Risc-V inventors
- From 2015, july23
- 食譜的發明者兼廚師
- 全球1000個員工
- 市值2.5Billion

## Before we start
- Risc-V is the trend
    - 預估到 2025有62.4 billion的risc-v需求
- AI/ML is the trend 
- Every domain needs CPU
    - `Our Risc-V CPU can satisfy your AI requirement w/o attaching other GPU/DLA`
    - DLA: Deep Learning Accerlators

## SiFIve Risc-V Product Families 
- Sifive Intellengence: https://www.sifive.com/cores/intelligence

### Sifive Intellengence X280 Processor

- Vector Processing for AI/ML workloads
    - seems like arm's SIMD but more flexible
    - 512-bit vector length extension with RISC-V Vectors(RVV) 1.0
    - Sifive Intellengence Extensions, custom instructions that accerlerate AI/ML performance
    
### Sifive Intellengence Extensions accelerate AI Computation 

### Sifive Intellengence: Designed for evolving AI needs


- 若過了幾年有新的算法，已經設計好的DLA是無法支援的
- Support for softmax, TopK, etc
- 提供的粒度是比較細的，提供linear/non-linear的function可以使用

- Programmability is the key, we provide it 
    - RVV intrinsic


## How about Software?

### TensorflowLite+ NN library

- TFLite is a simple and quick deployment runtime
- Dispatch op to Sifive NN library 
    - optimized by RVV intinsic and extended instructions

- Performance 
    - MobileBERT-int8(NLP) achieve ? 3FPS @1G x280-dual cores
    - MobileNetV3-unint8(Classification) achieve > 70FPS @1G  

### The limits of TFLite

- Pros
    - Easy to deploy. Time to market
    
- Cons
    - Bad parallelism
    - Graph optimization limitation. We want the best perfromance on SiFIve Platform
        - 一個單純的interperter，無法做到op fusion 
    - Only support TF/TFlite
    
    
### What is the something Great?

- Interpreter is not enough, we need:
    - Compiler: More optimization & code-gen automatically 不用再手刻
    - Runtime: Execute Efficiently
    
    
### Recommendation Software

- MLIR
    - Multi-Level Intermediate Representation
    - Mainly solve 2 problems
        - Significantly reduce the cost of buliding domain specific compilers 
        - Software segmentation: 解決太多廠商重複造輪子(AI compiler)
        
    - 如何讓更多廠商進來協作？
        - MLIR Dialects(方言)
            - 可以讓多種IR放進來
            - 提供run trip
    - 是透過LLVM去做code gen

- IREE
    - https://github.com/iree-org/iree
    - 接下來想推在Risc-V上的
    - from Google
    - MLIR的其中一個User
    - 目前Sifive跟Google cowork去打開risc-V上的使用
    - AI compiler and runtime
    
- IREE RVV code-gen
    - End to End flow 
        - TFlite-> TOSA MLIR -> Linalg -> Vector +scf -> LLVM IR ->RVV
        
- Perforamce of IREE
    - IREE vs TFLite
        - mobileBERT-f32: IREE +70% than TFLite
        
        
        
## Summary
- HW: SiFive intellengence Provide not only computation but also programmablity 

- SW
    - TFlite
    - IREE 
    - 提供 QEMU 來模擬  


