Cisco **CRS (Carrier Routing System)** routers are basically telecom-grade beasts, built for insane scale and nonstop uptime. At a high level, the hardware is modular and split across a few major subsystems:

### 🧠 1. Route Processor (RP)

Think of this as the brain.

* Runs **Cisco IOS XR**
* Handles routing protocols (BGP, OSPF, IS-IS, etc.)
* Manages control plane, system monitoring, and configuration
* Typically deployed in **redundant pairs** (active/standby)

---

### 🚀 2. Line Cards (LCs)

These are the muscle that actually push packets.

* Provide physical interfaces (10G, 40G, 100G depending on CRS model)
* Handle **data plane forwarding**
* Perform packet lookup, QoS, ACLs, and forwarding decisions
* Hot-swappable

---

### 🧩 3. Fabric Cards (FCs)

The high-speed internal highway.

* Form the **switch fabric** that interconnects all line cards
* Provide massive backplane bandwidth (multi-terabit)
* Redundant and load-balanced
* Failure-tolerant by design

---

### 🔌 4. Power Supply Units (PSUs)

Built for carrier environments.

* Multiple **AC and/or DC** power supplies
* Fully redundant (N+1 or better)
* Hot-swappable

---

### ❄️ 5. Fan Trays / Cooling Modules

Keeping the monster cool.

* High-capacity fan trays
* Front-to-back or side-to-side airflow (model-dependent)
* Redundant and hot-swappable

---

### 🏗️ 6. Chassis / Backplane

The physical backbone.

* Houses all modules
* Integrated midplane/backplane
* Designed to support **multi-slot scalability**
* Engineered for shock, heat, and continuous operation

---

### 🧪 7. Timing & Clocking Modules (model-dependent)

Important in carrier networks.

* Provides precise timing (SyncE, GPS, BITS)
* Used for mobile backhaul and carrier sync requirements

---

### 🧯 8. Alarm & Monitoring Modules

Carrier-grade observability.

* Environmental monitoring (temp, voltage)
* External alarm interfaces
* LEDs, logs, and SNMP telemetry
