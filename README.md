 # Secure Boot FSM Controller for FPGAs
A runtime tamper-hardened Secure Boot Finite State Machine (FSM), integrated with a high-performance **cryptographic hash core** optimized for Xilinx Artix-7 FPGA architectures.

# Block Diagram
<img width="1062" height="697" alt="612377680-715604ff-c04c-4b91-ae42-ab2c745e17b1" src="https://github.com/user-attachments/assets/5e3e6e1c-ee6d-40c2-89a5-59c9e31adb98" />

---

## Reports 

- Timing closes at 100 MHz on Artix-7 via a 4-stage round pipeline in the compression core.
 
| Parameter | Metric / Value |
| :--- | :--- |
| **Target Hardware** | Xilinx Artix-7 (Basys3 Evaluation Kit) |
| **Operating Frequency** | 100 MHz |
| **Worst Negative Slack (WNS)** | `+0.263 ns` |
| **Look-Up Tables (LUTs)** | 4,871 |
| **Flip-Flops (FFs)** | 2,605 |
| **Total Thermal Power** | 0.189 W (Design Power Budget: 0.500 W) |

---
### Trojan Stealth: Power vs Switching Activity

Example: A 64-bit `junk_toggle` always on trojan increments every cycle when `trojan_en=1`. 

```diff
# diff dormant3_power.rpt active3_power.rpt
< | Total On-Chip Power (W)  | 0.082 |
> | Total On-Chip Power (W)  | 0.083 |
< |   Register |  0.000 | 4732 |
> |   Register | <0.001 | 4732 |  # 3-decimal rounding
# Dynamic 0.014W / Static 0.068W identical - delta ~32uW in noise (Medium confidence)
```
```diff
# diff dormant_trojan3.saif active_trojan3.saif | grep junk_toggle_int
< (junk_toggle_int[0] (T0 1000000) (T1 0) (TX 0) (TC 0))
> (junk_toggle_int[0] (T0 500000) (T1 500000) (TX 0) (TC 100))
< (junk_toggle_int[1] (T0 1000000) (T1 0) (TC 0))
> (junk_toggle_int[1] (T0 500000) (T1 500000) (TC 50))
< (junk_toggle_int[2] (T0 1000000) (T1 0) (TC 0))
> (junk_toggle_int[2] (T0 495100) (T1 504900) (TC 25))
# Dormant TC=0, Active TC=100/50/25... = stealth trojan active but invisible to top-level power.
```
---
## Verification 
- Hash core checked against RFC 7693
- RTL-level fault injection testbench for FSM resilience: 480/480 single-bit injections pass
- SystemVerilog assertions on state invariants, parity, and handshake sequencing
 
---

## Source Access
RTL and testbenches are not public, this work is under submission.

 

 
