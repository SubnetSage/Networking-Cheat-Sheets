# 🚀 MPLS Cheat Sheet (Service Provider & Enterprise)

## 1️⃣ What MPLS Is

* **Multiprotocol Label Switching**
* Forwards packets using **labels**, not IP lookups
* Sits **between Layer 2 and Layer 3** (“Layer 2.5”)
* Designed for **scale, speed, and traffic engineering**

---

## 2️⃣ Core MPLS Devices

| Device | Role                                 |
| ------ | ------------------------------------ |
| **CE** | Customer Edge (no MPLS awareness)    |
| **PE** | Provider Edge (VRFs, labels, VPNs)   |
| **P**  | Provider Core (labels only, no VRFs) |

📌 **P routers never see customer IPs**

---

## 3️⃣ MPLS Labels

* **20-bit label**
* Pushed / swapped / popped
* Label stack allows **multiple services**

| Action | Meaning       |
| ------ | ------------- |
| Push   | Add label     |
| Swap   | Replace label |
| Pop    | Remove label  |

---

## 4️⃣ MPLS Forwarding Plane

* **LFIB** (Label Forwarding Information Base)
* Packet forwarding based on:

```
Incoming Label → Outgoing Label + Interface
```

---

## 5️⃣ Label Distribution

### LDP (Most Common)

* Automatic label exchange
* Used with IGP (OSPF / IS-IS)
* Best-effort traffic

### RSVP-TE

* Explicit paths
* Bandwidth reservation
* Traffic engineering

---

## 6️⃣ MPLS Control Plane Stack

```
IGP → LDP → MPLS Forwarding
```

* IGP finds loopbacks
* LDP binds labels to IGP routes
* MPLS forwards traffic

📌 **MPLS depends entirely on a healthy IGP**

---

## 7️⃣ MPLS VPN Types

| Type      | Use Case                      |
| --------- | ----------------------------- |
| **L3VPN** | Most common (Enterprise WANs) |
| **L2VPN** | VPLS, VPWS                    |
| **EVPN**  | Modern DC & SP fabrics        |

---

## 8️⃣ MPLS L3VPN (🔥 Most Important)

### VRFs

* Separate routing tables per customer
* Prevent route leakage

### Route Distinguisher (RD)

* Makes overlapping IPs unique
* **Not used for routing decisions**

### Route Target (RT)

* Controls **import/export**
* **Policy mechanism**

---

## 9️⃣ MPLS VPN Routing Flow

```
CE → PE → (Label Stack) → P → P → PE → CE
```

**Label Stack**

* Outer label = transport (LDP)
* Inner label = VPN (MP-BGP)

---

## 🔟 MP-BGP (VPNv4 / VPNv6)

* Carries customer routes across provider
* Exchanges:

  * RD
  * RT
  * VPN labels

📌 **BGP distributes VPN labels, not LDP**

---

## 1️⃣1️⃣ Penultimate Hop Popping (PHP)

* Second-to-last router removes transport label
* Reduces PE workload
* Controlled via **implicit-null label**

---

## 1️⃣2️⃣ MPLS TTL

* Prevents loops
* Can be:

  * **Propagated**
  * **Hidden**

Common in ISP cores to **hide topology**

---

## 1️⃣3️⃣ MPLS Traffic Engineering

| Feature            | Purpose              |
| ------------------ | -------------------- |
| RSVP-TE            | Explicit paths       |
| Fast Reroute (FRR) | Sub-50ms failover    |
| CSPF               | Constraint-based SPF |

---

## 1️⃣4️⃣ MPLS QoS

* EXP bits (3 bits)
* Map IP DSCP → MPLS EXP
* Preserve QoS across backbone

---

## 1️⃣5️⃣ MPLS Troubleshooting (🔥 On-Shift)

```bash
show mpls interfaces
show mpls ldp neighbor
show mpls forwarding-table
show ip route vrf <name>
show bgp vpnv4 all
traceroute mpls ipv4
```

---

## 1️⃣6️⃣ Common MPLS Failures

❌ IGP down → MPLS down
❌ LDP session down
❌ Wrong RT import/export
❌ VRF not applied to interface
❌ BGP not advertising VPN routes

---

## 1️⃣7️⃣ MPLS Mental Model (🔥 Memorize This)

> **IGP finds the path**
> **LDP labels the path**
> **BGP decides whose traffic rides the path**

---

## 🧠 Memory Hooks

* **P routers swap, PE routers think**
* **RD = uniqueness, RT = policy**
* **No IGP = no MPLS**
* **BGP carries VPN labels, not LDP**

---

## 🔧 Real ISP Example

* OSPF/IS-IS in the core
* LDP for transport labels
* MP-BGP for VPNv4
* VRFs on PE
* PHP enabled
* FRR for protection
