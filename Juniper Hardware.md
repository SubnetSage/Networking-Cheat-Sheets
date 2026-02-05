Juniper **MX960** and **MX320** are classic carrier-grade workhorses. Same family, same architecture, just very different scale. I’ll break them down cleanly and then call out the key differences.

---

## 🧠 1. Routing Engine (RE)

The control-plane brain.

* Runs **Junos OS**
* Handles routing protocols, management, and system control
* Installed as **RE-S** or **RE-X** (older → newer)
* **Redundant** (RE0 / RE1)

**MX960**

* 2 Routing Engine slots (typically RE-S-1800 or RE-X)

**MX320**

* 2 Routing Engine slots (same RE options, higher overall system scale)

---

## 🚀 2. Line Cards (FPCs – Flexible PIC Concentrators)

This is where traffic actually moves.

* Perform packet forwarding (data plane)
* Contain forwarding ASICs
* Accept PICs or MICs for interfaces
* Hot-swappable

**MX960**

* **8 FPC slots**
* Up to multi-terabit throughput depending on FPC generation

**MX320**

* **16 FPC slots**
* Roughly double the capacity of the MX960

---

## 🔌 3. PICs / MICs (Physical Interface Cards / Modular Interface Cards)

These provide the actual ports.

Common options:

* 1G / 10G / 40G / 100G Ethernet
* POS / SONET (legacy)
* Channelized interfaces

Installed *into* FPCs, not directly into the chassis.

---

## 🧩 4. Switch Fabric (SCB / SFB)

The internal high-speed interconnect.

* Connects all FPCs to each other
* Provides non-blocking bandwidth
* Fully redundant

**MX960**

* Uses **Switch Control Boards (SCBs)**
* Multiple SCBs for redundancy and throughput

**MX320**

* Uses **Switch Fabric Boards (SFBs)**
* Higher fabric capacity to support more FPCs

---

## 💾 5. Packet Forwarding Engines (PFE)

The ASIC layer doing the heavy lifting.

* Embedded within FPCs
* Handles:

  * MPLS
  * QoS
  * ACLs
  * Fast lookups
* Not field-replaceable separately (part of FPC)

---

## ❄️ 6. Fan Trays

Cooling at carrier scale.

* Multiple fan trays
* Hot-swappable
* Front-to-back airflow
* Critical for chassis health

**MX960**

* Fewer fan trays than MX320

**MX320**

* Larger cooling system due to higher density

---

## 🔋 7. Power Supplies

Designed for telco environments.

* AC or DC power options
* **Redundant (N+1 or better)**
* Hot-swappable

**MX960**

* Fewer PSUs required

**MX320**

* More PSUs to support full chassis load

---

## ⏱️ 8. Timing / Clocking (Optional)

Used in service provider networks.

* BITS
* SyncE
* GPS timing (via external modules)

---

## 🏗️ 9. Chassis / Midplane

The physical backbone.

* High-speed midplane
* Supports all control, fabric, and line cards
* Built for continuous operation

---

## 🔍 Quick Comparison

| Feature        | MX960       | MX320      |
| -------------- | ----------- | ---------- |
| Rack Units     | ~25RU       | ~40RU      |
| FPC Slots      | 8           | 16         |
| RE Slots       | 2           | 2          |
| Fabric Boards  | SCBs        | SFBs       |
| Power Capacity | Lower       | Higher     |
| Use Case       | Core / Edge | Large Core |

---

### Mental model

* **RE** = brain
* **FPC + PIC/MIC** = packet movers + ports
* **Fabric boards** = internal highway
* **Power + fans** = keep it alive

