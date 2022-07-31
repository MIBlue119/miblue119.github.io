---
title: 設計精簡又快速的 RISC-V 指令集模擬器 - Lambert Wu
description: A note about COSCUP
date: 2022-07-30
tags:
  - posts
layout: layouts/post.njk
---


- This my first to attend COSCUP and this is my note about the talks from SiFive.
- Speaker
    - Kito Cheng 
    - https://github.com/kito-cheng

- Brief
    - How to use 
    - How to write
- What topics are covered today?
    - assembly
    - compiler
    
### What is Risc-V?
- From UC Berkeley,2010 
    - promote from 
        - Krste Asanovic 
        - Andrew 
- The goal of risc-v 
    - provide a ISA support embedded system to HPC
    - design a baseline ISA and some standard extension and some companies non-standard extension 
    
    
### Risc-V Vector Extension?


### Start from an example `Vector Addition` 
- a twao array addition 
```
void add(int *a, int *b, int*c, int len)
{
for ()
{
    a[i] = b[i]+c[i]
}
    
}
```      

### How to optimize that?
- Software solution
    - Loop unrolling
    - Compilter optimization
        - gcc -O3    
- Micro-arch 
- 加指令
 

### 加指令: SIMD

- Single Instuction Multiple Data
    - 一個指令可以處理多筆資料
    - 許多架構會提供更大的暫存器來做操作

- ARM Neon
    - VADD.I32 q1, q2, q3
    - 4x 32 bit
- 想看更多SIMD?
    - 看更多網路黑貓
    -  https://champyen.blogspot.com/2017/01/simd-introduction.html 


### SIMD 的應用狀況
- 迴圈處理倍數處理很麻煩
    - tail loop
- Memory Alignment: 沒對齊會變慢
- 需處理長度非指令集所支援的
- 可能會讓原本的程式長度變更長

### 編譯器是我們的救星
- 可以使用 GCC/LLVM 來協助處理
- 穿插工商 SiFIve的 LLVM compiler的職缺招募


## RiscV Vector Extension 
- 指令集層級解決SIMD遇到的問題
    - No tail loop
    - solve memory alignment 
- SIMD 錯了嗎？
    - SIMD 指令集特性：長度固定
    - x86:
        - AVX(128-bits)
        - AVX2(256-bits)
        - AVX-512(512bits)
    - 不同的opcode相同的運算，但...只有長度一樣
    - 增加硬體的複雜度
        - 同樣的東西要一直做/支援，也要相應的延展
    - 舊有程式也無法運用新的指令集
        - 例如舊的程式用AVX指令集寫，跑在支援AVX-512機器上但無法利用
            - 程式可能過兩三年就要重新compile
            
- (Scalable) Vector Extension
    - Risc-V Vector Extension提供可變長度而非固定長度的指令
    - 用Vector Extention 寫的程式在新的Risc-V core 是無痛升級

- 這個概念從1975 Cray-1就有類似設計理念


## 正片開始：Risc-V Vector Extension

- 提供32個可變長度的Vector Register
    - 最短32bits

### 指令集簡介

- 理念
    - 最小化指令數量
    - 彈性
    
- 範例
    - 4 x 32 bit int vector addition
        - vsetivli x0, 4, e32, m1
        - vadd.vv, v1, v2, v3


### 以Risc-V的指令集 來實作前面的array相加

### 與SIMD 比較
- 不需處理tail loop
- 無痛升級
    - 在同樣也是Risc-V新架構上跑，假如寬度有升級
        - 程式不用改寫也不用compile，binary放上之後就能使用

### 指令集小結
- 彈性的設計
- 軟體效能無痛升級
- 用不同的暫存器長度來透過一套指令集涵蓋各種目標市場
    - 嵌入式：為了能耗，讓register寬度小
    - 桌上型
    - Server: 讓register可以到很寬

### 缺點
- 硬體與SIMD相比複雜許多
- 軟體撰寫與傳統SIMD不同，需要額外學習成本
- 目前軟體(Compiler/OS/Kernel)支援還在路上


## Programming Model
- 軟體要怎麼使用呢？

### 軟體支援
- 手排：使用intrinsic 以及Language Extention 撰寫
- 自排：自動向量化，你寫迴圈，compiler來幫你

### 手排範例
- 過往：主流compiler 會提供語法extension
- 基於sifive 難用過往方式寫
    - 本質上與SIMD不同，會需要引入些輔助函數
        - 在c 引入 vsetvli_e32m1() 來查詢
    - 困擾
        - 難讓使用者快速切入
        - C語言介面與assembly又有些落差
    - 與低階組合語言比起來多了型別與長度設定
    - 利於編譯器最佳化跟code design

### 自排可能性追求

- 你寫迴圈，編譯器自動向量化
- 待發展

### 其他可能：混合式

- OpenMP, OpenCL
    - 讓用戶寫的比較矩陣的操作，也讓編譯器更好轉


## 大結
- Risc-V vector Extension 有彈性的設計與強大的運算能力
- 目前軟體則有多種選項且持續發展

## 工商
- 如果你對上述的東西很有興趣？
    - https://www.sifive.com/careers/5169976003/llvm-compiler-engineer-risc-vector-hsinchu-taiwan 
    


## Q&A
- 目前simulator 
- 現在想找板子：平頭哥T1開發版(12塊美金)
- Kernel Context Switch 成本變這麼高
- 這邊要讓效能變更好？    
    - Vector Extension 
    
- x86 20年
    - 可能程式跑在後面
        
    - risc v 改善
        - 會在risc v 程式上標記使用了什麼指令集
        - kernel 那要寫load來判斷，MIPS已經有開洞
        
- Thead
    - https://www.t-head.cn/ 

