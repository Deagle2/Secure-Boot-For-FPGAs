 # Secure Boot FSM Controller for FPGAs

# 🔒 Source Code Access Note
Note: The HDL source code and testbench files are currently maintained in a private development branch for intellectual property (**IP**) protection and academic evaluation. For access inquiries or academic collaboration regarding the complete SystemVerilog implementation, please contact the repository owner directly.

# Secure Boot Finite State Machine (FSM) with Hardware Security Hardening

A runtime tamper-resistant Secure Boot Finite State Machine (FSM) implemented in SystemVerilog, integrated with a high-performance **cryptographic hash core** optimized for Xilinx Artix-7 FPGA architectures.
 

# Block Diagram
<img width="1062" height="697" alt="image" src="https://github.com/user-attachments/assets/715604ff-c04c-4b91-ae42-ab2c745e17b1" />

---

## Reports (PPA)

The complete design achieves strict timing closure at **100 MHz** on the Artix-7 fabric. High-throughput cryptographic execution is achieved via a **4-stage round pipeline** embedded within the compression function core.

### Post-Route Physical Implementation Metrics (PPA)
| Parameter | Metric / Value |
| :--- | :--- |
| **Target Hardware** | Xilinx Artix-7 (Basys3 Evaluation Kit) |
| **Operating Frequency** | 100 MHz |
| **Worst Negative Slack (WNS)** | `+0.263 ns` (Timing Closed) |
| **Look-Up Tables (LUTs)** | 4,871 |
| **Flip-Flops (FFs)** | 2,605 |
| **Total Thermal Power** | 0.189 W (Design Power Budget: 0.500 W) |

---

## Verification 

* **Algorithmic Validation:** Fully verified the hashing core output correctness against standard RFC test vectors
* **Runtime Fault Injection:** Evaluated FSM resilience against environmental and adversarial disruptions using a directed RTL-level runtime fault injection testbench.
* **Formal & Behavioral Assertions:** Implemented strict **SystemVerilog Assertions (SVA)** to continuously monitor and guarantee state invariants, parity correctness, and proper handshake sequences during simulation.

---
 
