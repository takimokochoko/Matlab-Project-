# Dual-Controller Security Architecture for Cyber-Physical Systems

This repository contains the MATLAB/Simulink implementation of a **Parallel Dual-Controller Defense Framework** designed to detect stealthy cyber-attacks in Cyber-Physical Systems (CPS). 

By leveraging a time-varying parameter $a$ and an isolated internal "Shadow Loop," this architecture strips away an adversary's ability to manipulate sensor feedback and remain undetected.

---

## 📌 Project Overview

Standard single-loop control systems are vulnerable to **sensor spoofing and false data injection (FDI) attacks**. An adversary can manipulate physical system states while injecting fake, nominal sensor readings onto the network to trick monitoring systems.

This project introduces a **Dual-Controller Architecture** that creates a secure, untamperable reference baseline inside local software memory. Even if an attacker hijacks network communication lines, any deviation between the physical plant and the internal shadow reference triggers an immediate anomaly detection spike.

---

## 🏗️ Key Features & Architecture

* **Isolated Shadow Loop:** Runs completely within secure local processor memory. The attacker has zero network visibility or physical access to it.
* **Time-Varying Parameter Tracking ($a$):** The plant dynamics use a dynamic parameter $a(t)$. Because the attacker does not know $a(t)$, their attack model uses an incorrect zero, causing physical plant output to diverge rapidly.
* **Sensor Spoofing Protection:** Even if the attacker spoofs sensor feedback lines to look "flat and safe," the spoofed data instantly mismatches with the moving output of the isolated shadow loop.
* **Noise-Tolerant Detection Thresholds:** Parameter tuning ensures clear detection spikes above background measurement noise without triggering false alarms.

---

## 📐 Core Logic & Detection Mechanism

The architecture forces the adversary into an **unmaskable dilemma**:

$$\text{Detection Trigger} = |y_{\text{real/network}} - y_{\text{shadow}}| > \text{Threshold}$$

1. **If the attacker does NOT spoof sensors:** The wrong parameter $a$ causes a structural zero mismatch, leading to an immediate physical explosion in plant output that violates safety bounds.
2. **If the attacker DOES spoof sensors:** The fake, flat signal sent over the network immediately mismatches with the dynamic $y_{\text{shadow}}$ calculated continuously inside the isolated processor.

> **Result:** Stealthy attacks become mathematically impossible.

---

## 📁 Repository Structure

* `simulink/` — Contains `.slx` MATLAB/Simulink models:
  * Single-loop attack failure baseline model.
  * Complete Dual-Controller architecture with time-varying $a(t)$.
* `docs/` — Summary logic and architecture design files.

---

## 🚀 How to Run the Simulation

1. Open **MATLAB** (R2020b or newer recommended) and launch **Simulink**.
2. Clone this repository:
   ```bash
   git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
