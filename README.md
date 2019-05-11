# DL4MCU
List of recent works on bringing deep learning to microcontrollers and deeply embedded devices. 

## ASIC Implementation
### 2019
### 2018
- [CHIPMUNK(花栗鼠): A Systolically Scalable 0.9 mm2, 3.08 Gop/s/mW @ 1.2 mW Accelerator for Near-Sensor Recurrent Neural Network Inference](https://arxiv.org/pdf/1711.05734.pdf) (CICC, ETHZ)

## Compiler

## Software

## Applications

## Sort by group


# MISCELLANEOUS
## Features of MCU-based DL systems
The design target of DL accelerators for server or mobile applications is high throughput and versatility in order to meet the goal of real-time processing of various NN models. Design constraints such as power consumption can be realitively loosen. And for the purpose of compatibility, the hardware should support a wide range of ops dictated by new NN models. 

But for embedded systems, the power constraint is as important as computational capability. The major challenge of enabling DL in MCU based systems is the gap between computational capability and energy budget. Since here I focus on deeply embedded systems, the power envelop is usually no more than 100 mW (for some battery powered IoT end-nodes the power enevlop is even tighter). And we need to co-design the algorithm and hardware rather than adpating hardware to alogrithm, in order to fill the efficiency gap. And for some batteried powered applications there is even no throughpu requirement. 

The application scenario of MCU-based DL can be roughly classified into two types. 
### 1. DL Normally-OFF applications
These applications usually uses battery as power source and expects very long battery life. The system maintains a minimum always-on circuit while the DL inference is performed periodically or triggered by external events. In such systems, the energy consumption per inference does not really matters since the average power can be as low as several microwatts by heavily duty-cycling, but the standby power is crucial since it contributes to most of overall energy consumption. This riases an insteresting question: where to store the DL model during OFF time and during ON (inference) time?

We have 3 choices if the model is small enough to fit in on-chip SRAM. This usually holds true for applications that takes audio, ECG or other sensor signals as input. The former two methods have larger inference energy while the last one has higher leakage power. 
1. Store the model in NVM during off time, and use it directly from NVM during inference. 
2. Store the model in NVM during off time, and load the model to on-chip SRAM before inference. 
3. Store the model in SRAM during off time. 

If the model does not fit the on-chip SRAM, external memory should be used. Since standby power is most critical in normally-off systems, using dynamic memory will be prohibitive because 

Below are some examples of normally-off applications:
- Invasion detection system (periodically or event driven)
- Wearable ECG/EEG monitoring system (periodically)

### DL Always-ON applications
In always-on applications the DL task is processed continuously. 
Below are some examples of always-on applications:
- micro powered uav or robots

## How to deploy DL on ULP systems
There is no consensus on how to deploy DL on MCU based systems, but a common view is using heterogeneous architecture to fill the efficiency gap. The heterogeneous system includes a Cortex-M (or equivalnet) MCU (or clusters), memory system and HW accelerators. For small NN models (which is common in aplications that takes a 1-dim signal as input, such as ECG/KEYWORD/VIBRATION), deployment is easy since on-chip SRAMs (200-500KB) are usually capable to hold all models and intermediate results. But for large models (such as embedded vision applications) 

MCU市场碎片化严重，同一系列的MCU可根据不同应用需求衍生出不同型号。如何用同一种可扩展的架构支持从小到大的应用？

Consensus: Using heterogeneous architecture (Cortex-M or RISC-V + HW Accelerator).
Challenge:
1. How to support intelligent applications with different memory footprint and different ops.
- Scalable HW accelerator. (small to large)
- ULP memory system. (How to harmonize FLASH, TCDM, EXT-SRAM). 

Or:
Challenge: how to deploy intelligent applications with different memory footprint, different ops on MCU based systems with limited power envelop?
1. Use heterogeneous architecture to fill the efficiency gap. 
2. Scalable HW accelerator with unified interface and toolchain. 
3. ULP memory system. (How to harmonize FLASH, ext-SRAM, TCDM and SCM, considering both power and BW requirements).  


### 
