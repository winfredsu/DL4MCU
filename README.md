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

## MISCELLANEOUS
The major challenge of enabling DL in MCU based systems is the gap between computational capability and energy budget. Since here I focus on deeply embedded systems, the power envelop is usually no more than 100 mW (for some battery powered IoT end-nodes the power enevlop is even tighter). How to make DL work with such limitation requires co-design of application, alogirithm and hardware. Here are some of my thoughts, following the top-down approach. 

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
Always-ON applications means that the DL task is continous. 

Below are some examples of always-on applications:


### 
