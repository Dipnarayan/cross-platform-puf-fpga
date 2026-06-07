<div align="center">

# 🔐 Cross-Platform PUF for FPGA-Based IoT Devices

### A Novel Platform-Independent Hardware Security Primitive for Emerging IoT Systems

An IEEE-published hardware security framework introducing a Cross-Platform Ring Oscillator Physically Unclonable Function (CPRO-PUF) that eliminates FPGA placement constraints and enables scalable deployment across multiple FPGA families.

![Research](https://img.shields.io/badge/Type-Research-blue)
![IEEE](https://img.shields.io/badge/Publication-IEEE%20AsianHOST%202022-success)
![Hardware Security](https://img.shields.io/badge/Domain-Hardware%20Security-red)
![FPGA](https://img.shields.io/badge/Platform-FPGA-green)
![IoT Security](https://img.shields.io/badge/Application-IoT%20Security-orange)

</div>

---

# 📖 Overview

As billions of IoT devices become interconnected, hardware-level security has become a critical requirement for authentication, device identification, secure key generation, and anti-counterfeiting.

Traditional FPGA-based Physically Unclonable Functions (PUFs) often suffer from a major limitation:

> Platform dependence.

Most delay-based FPGA PUFs require carefully matched routing paths, manual placement constraints, and board-specific validation, making large-scale deployment difficult.

This work introduces a novel **Cross-Platform Ring Oscillator PUF (CPRO-PUF)** architecture that removes these constraints and enables deployment across multiple FPGA families without redesign or post-implementation validation.

The proposed design provides:

- Platform-independent operation
- Placement-constraint-free implementation
- Hardware fingerprint generation
- Cryptographic key generation
- FPGA portability
- Lightweight IoT security

---

# 📚 Publication

This repository is based on the IEEE conference publication:

> **Das, D., Roy, S., Mahalat, M. H., & Sen, B.**
>
> **A Novel Cross-Platform Physically Unclonable Function for Emerging FPGA-Based IoT Devices**
>
> 2022 Asian Hardware Oriented Security and Trust Symposium (AsianHOST)
>
> Singapore, 2022
>
> Pages: 1–4
>
> DOI: 10.1109/AsianHOST56390.2022.10022185

---

# 🎯 Research Motivation

Modern FPGA-based IoT systems face several security challenges:

- Hardware cloning
- Device counterfeiting
- Reverse engineering
- Secure key storage
- Hardware Trojan insertion
- Side-channel attacks

Physically Unclonable Functions (PUFs) provide a hardware-rooted security mechanism by exploiting manufacturing variations present in semiconductor devices.

However, existing FPGA PUF architectures typically require:

- Symmetrical routing
- Placement constraints
- Board-specific tuning
- Manual validation

These limitations hinder widespread industrial adoption.

The proposed CPRO-PUF eliminates these challenges through a fundamentally different design approach. :contentReference[oaicite:1]{index=1}

---

# ✨ Key Contributions

## 🌍 Platform-Independent PUF Design

The proposed architecture operates without:

- Placement constraints
- Relative path matching
- Manual floorplanning
- FPGA-family-specific redesign

This significantly simplifies deployment across FPGA platforms.

---

## 🔄 Single-Path Response Generation

Conventional delay-based PUFs compare two identical paths.

CPRO-PUF introduces:

```text
One Path
→ One Response Bit
```

This eliminates bias caused by path matching requirements.

---

## ⚡ Cross-Family FPGA Compatibility

The architecture was validated across:

| FPGA Family | Technology Node |
|-------------|----------------|
| Spartan-3E | 90 nm |
| Spartan-6 | 45 nm |
| Artix-7 | 28 nm |

The same design was deployed without platform-specific modifications. :contentReference[oaicite:2]{index=2}

---

# 🏗️ System Architecture

```text
Global Enable
       │
       ▼
Clock Pulse Generator
       │
       ▼
Clock Starters
       │
       ▼
PUF Cells
       │
       ▼
Response Generation
       │
       ▼
128-bit Hardware Fingerprint
```

The architecture consists of two major components:

1. PUF Cells
2. Clock Pulse Generator Circuit

---

# 🧠 PUF Cell Architecture

Each PUF cell contains:

- NAND Gate
- D Flip-Flop

The NAND gate forms an inverter-based oscillator.

The oscillator output is sampled through a D flip-flop to generate a single response bit.

### Characteristics

- One cell = One response bit
- No path comparison required
- Lightweight implementation
- High scalability

The architecture is illustrated in Figure 1 of the paper. :contentReference[oaicite:3]{index=3}

---

# ⏱️ Clock Pulse Generator

One of the novel aspects of the design is the custom clock pulse generation mechanism.

Instead of relying on FPGA board clocks, the design introduces:

### Clock Starters

Each Clock Starter consists of:

- AND Gate
- D Flip-Flop

Multiple Clock Starters are connected sequentially.

Purpose:

- Precise response capture timing
- Improved reliability
- Platform independence

The experimental analysis showed that eight Clock Starters provide sufficient delay for stable response generation. :contentReference[oaicite:4]{index=4}

---

# ⚙️ Working Principle

## Step 1

Global Enable activates the architecture.

## Step 2

The Clock Pulse Generator introduces controlled delay.

## Step 3

Each PUF cell oscillates independently.

## Step 4

The D Flip-Flop captures the oscillator state.

## Step 5

The captured state becomes a response bit.

## Step 6

All response bits are combined into a:

```text
128-bit PUF Response
```

This response serves as a unique hardware fingerprint.

---

# 💻 Hardware Implementation

The design was implemented using:

### Design Language

```text
Verilog HDL
```

### Toolchain

```text
Xilinx ISE 14.7
```

### Embedded Controller

```text
MicroBlaze
```

### FPGA Families

- Spartan-3E
- Spartan-6
- Artix-7

The prototype consists of:

```text
128 PUF Cells
8 Clock Starters
128-bit Response Vector
```

:contentReference[oaicite:5]{index=5}

---

# 📊 Performance Evaluation

The design was validated using four standard PUF metrics.

---

## Uniqueness

Measures how different responses are between chips.

### Results

| FPGA Family | Average Uniqueness |
|-------------|------------------|
| Spartan-3E | ~47% |
| Spartan-6 | ~50% |
| Artix-7 | ~55% |

Close to the ideal value of 50%. :contentReference[oaicite:6]{index=6}

---

## Reliability

Measures response stability under environmental variations.

### Results

| FPGA Family | Reliability |
|-------------|-------------|
| Spartan-3E | 97.21% |
| Spartan-6 | 96.63% |
| Artix-7 | 96.89% |

Responses remained stable across temperature variations from 25°C to 65°C. :contentReference[oaicite:7]{index=7}

---

## Uniformity

Measures the balance between zeros and ones.

### Results

| FPGA Family | Uniformity |
|-------------|------------|
| Spartan-3E | ~43% |
| Spartan-6 | ~59% |
| Artix-7 | ~42% |

Demonstrating acceptable randomness characteristics. :contentReference[oaicite:8]{index=8}

---

## Randomness Validation

The generated responses were evaluated using the:

### NIST SP 800-22 Test Suite

Tests Passed:

- Monobit Test
- Block Frequency Test
- Cumulative Sum Test
- Run Test
- Longest Run Test
- Approximate Entropy Test

All FPGA implementations successfully passed NIST randomness validation. :contentReference[oaicite:9]{index=9}

---

# 🚀 Advantages

### Platform Independent

No redesign required for different FPGA families.

### Placement Constraint Free

No manual floorplanning.

### Lightweight

Low hardware overhead.

### Scalable

Supports large response sizes.

### Reliable

Stable under environmental variations.

### Secure

Suitable for cryptographic applications.

---

# 🔒 Security Applications

## Device Authentication

Unique hardware identity generation.

---

## Hardware Fingerprinting

Counterfeit prevention and device tracking.

---

## Cryptographic Key Generation

Secure key derivation from silicon variations.

---

## Secure Boot

Hardware-rooted trust establishment.

---

## IoT Device Security

Low-cost security for resource-constrained devices.

---

# 🌍 Potential Applications

- Internet of Things (IoT)
- Industrial IoT (IIoT)
- Edge Devices
- FPGA-Based Systems
- Secure Embedded Systems
- Hardware Root of Trust
- Supply Chain Security
- Anti-Counterfeiting Solutions

---

# 🏛 Academic Contribution

This work contributes to:

- Hardware Security
- FPGA Security
- Physically Unclonable Functions
- Trusted Computing
- IoT Security
- Cryptographic Hardware
- Hardware Authentication

The proposed CPRO-PUF demonstrates that platform-independent FPGA-based PUF implementations can achieve high reliability, acceptable uniqueness, and strong randomness while eliminating the traditional requirement for placement constraints and board-specific tuning. :contentReference[oaicite:10]{index=10}

---

# 📖 Citation

```bibtex
@inproceedings{Das2022CPROPUF,
  author    = {Dipnarayan Das and Sourav Roy and Mahabub Hasan Mahalat and Bibhash Sen},
  title     = {A Novel Cross-Platform Physically Unclonable Function for Emerging FPGA-based IoT Devices},
  booktitle = {2022 Asian Hardware Oriented Security and Trust Symposium (AsianHOST)},
  year      = {2022},
  pages     = {1--4},
  doi       = {10.1109/AsianHOST56390.2022.10022185}
}
```

---

# 📚 Keywords

- Physical Unclonable Function
- PUF
- FPGA Security
- Hardware Security
- IoT Security
- Hardware Authentication
- Hardware Fingerprinting
- Cryptographic Key Generation
- Trusted Computing
- Ring Oscillator PUF
- Platform Independent PUF
- CPRO PUF

---

# License

This project is released under the MIT License.
