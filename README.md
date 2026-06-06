# Jin
# OTFS-Based Hybrid-CNN Symbol Detection for LEO Doppler Channels

This project simulates OTFS-QPSK transmission over a LEO Doppler channel and evaluates a confidence-based Hybrid-CNN detector.

## Overview

Low Earth Orbit (LEO) satellite communication suffers from large Doppler shift due to high satellite mobility.  
This project investigates an OTFS-based receiver structure that combines:

- Coarse detector
- CNN residual symbol classifier
- Confidence-based hybrid decision rule

The goal is to improve BER performance under a 7500 km/h LEO Doppler condition.

## System Setup

- Modulation: QPSK
- OTFS grid: M = 32, N = 16
- Channel: NTN-TDL-A based LEO Doppler channel + AWGN
- Carrier frequency: 2 GHz
- Subcarrier spacing: 15 kHz
- Speed: 7500 km/h
- SNR points: 0, 5, 10, 15, 20 dB

## Proposed Method

The CNN is not a full equalizer.  
It is used as a residual symbol classifier after coarse equalization.

Input features:

- Re{X_coarse}
- Im{X_coarse}
- |X_coarse|
- QPSK-distance logits

The final detector uses CNN softmax confidence:

- If confidence >= threshold: use CNN decision
- If confidence < threshold: fallback to coarse decision

## Results

The proposed Hybrid-CNN detector achieved lower BER than the coarse detector at all tested SNR points.

Maximum relative BER improvement:

- 28.0% at 20 dB

## Limitations

This project is a proof-of-concept simulation.

Future work:

- Fractional Doppler modeling
- Multiple LEO speed conditions
- Higher-order modulation such as 16-QAM
- Coded BER evaluation
- SDR or FPGA-based implementation
