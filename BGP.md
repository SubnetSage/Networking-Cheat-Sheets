Here’s a **no-fluff, real-world BGP cheat sheet** — the kind that actually helps in **ISP / core / enterprise edge** work *and* on exams (CCNA → CCNP → SP). This is written in the same style you’d use on shift when something’s broken.

---

# 🌍 BGP Cheat Sheet (Quick Reference)

## 1️⃣ What BGP Is

* **Path-vector routing protocol**
* Runs over **TCP port 179**
* Used **between Autonomous Systems (AS)**
* Focused on **policy**, not fastest path
* Scales to the **entire Internet**

---

## 2️⃣ BGP Types

| Type     | Description                  |
| -------- | ---------------------------- |
| **eBGP** | Between different AS numbers |
| **iBGP** | Within the same AS           |

**Key Rule**

> iBGP routers **do NOT** re-advertise routes learned from another iBGP peer (split-horizon rule)

---

## 3️⃣ BGP Neighbor States (🔥 Memorize)

```
Idle → Connect → Active → OpenSent → OpenConfirm → Established
```

**Established = routes can flow**

---

## 4️⃣ BGP Attributes (Order of Decision)

### 🥇 Path Selection (MOST IMPORTANT)

1. **Highest Weight** (Cisco only)
2. **Highest Local Preference**
3. **Locally originated**
4. **Shortest AS-Path**
5. **Lowest Origin type** (IGP < EGP < Incomplete)
6. **Lowest MED**
7. **eBGP over iBGP**
8. **Lowest IGP cost to next-hop**
9. **Oldest path**
10. **Lowest Router ID**

📌 **90% of traffic engineering uses Weight + Local Pref**

---

## 5️⃣ Well-Known Attributes

| Attribute        | Scope              |
| ---------------- | ------------------ |
| Weight           | Local (Cisco only) |
| Local Preference | AS-wide            |
| AS-Path          | Inter-AS           |
| Next-Hop         | Reachability       |
| MED              | Neighbor AS        |
| Origin           | Path source        |

---

## 6️⃣ Next-Hop Behavior

* **eBGP** → next-hop = neighbor IP
* **iBGP** → next-hop **unchanged**

📌 Common fix:

```
neighbor x.x.x.x next-hop-self
```

---

## 7️⃣ iBGP Scaling Rules

iBGP requires **full mesh** unless using:

| Method          | Purpose               |
| --------------- | --------------------- |
| Route Reflector | Scales large networks |
| Confederations  | Split AS internally   |

**Route Reflector Roles**

* RR
* Client
* Non-client

---

## 8️⃣ Synchronization Rule (Legacy)

* Old rule: BGP waits for IGP
* **Disabled by default**
* Ignore unless dealing with legacy gear

---

## 9️⃣ BGP Message Types

| Type         | Purpose                   |
| ------------ | ------------------------- |
| Open         | Establish session         |
| Update       | Advertise/withdraw routes |
| Keepalive    | Maintain session          |
| Notification | Error handling            |

---

## 🔟 Administrative Distance (Cisco)

| Route | AD      |
| ----- | ------- |
| eBGP  | **20**  |
| iBGP  | **200** |

---

## 1️⃣1️⃣ Route Advertisement Rules

* eBGP: advertise **best path only**
* iBGP: advertise **only eBGP or local routes**
* Never advertise routes **back to the neighbor they came from**

---

## 1️⃣2️⃣ Common BGP Policies

### AS-Path Prepending

```bash
route-map PREPEND permit 10
 set as-path prepend 65001 65001 65001
```

### Local Preference

```bash
set local-preference 200
```

### Weight

```bash
set weight 500
```

---

## 1️⃣3️⃣ Filtering Routes

### Prefix-Lists

```bash
ip prefix-list BLOCK seq 5 deny 0.0.0.0/0
```

### AS-Path Filters

```bash
ip as-path access-list 10 deny _65050_
```

---

## 1️⃣4️⃣ BGP Timers (Defaults)

| Timer     | Value   |
| --------- | ------- |
| Keepalive | 60 sec  |
| Hold Time | 180 sec |

📌 Must match or be negotiated lower

---

## 1️⃣5️⃣ BGP Troubleshooting (🔥 On-Shift Commands)

```bash
show ip bgp summary
show ip bgp
show ip bgp neighbors
show ip bgp neighbors x.x.x.x received-routes
show tcp brief
```

---

## 1️⃣6️⃣ Common BGP Failure Causes

❌ TCP 179 blocked
❌ Neighbor IP wrong
❌ ASN mismatch
❌ No route to next-hop
❌ Route filters blocking prefixes
❌ iBGP missing full mesh / RR

---

## 1️⃣7️⃣ BGP in ISP Networks (Reality Check)

* **IGP (OSPF/IS-IS)** = reachability
* **BGP** = policy + scale
* BGP does **not** care about bandwidth
* Most outages = **policy mistakes**

---

## 🧠 Memory Hooks

* **OSPF finds paths, BGP chooses policy**
* **Local Pref in, AS-Path out**
* **iBGP needs help to scale**
* **BGP won’t fix broken IGP**

---

If you want, I can:

* Build a **GNS3 ISP-style BGP lab** (iBGP + RR + eBGP)
* Create a **1-page printable PDF**
* Make a **BGP vs OSPF vs IS-IS comparison**
* Write a **LinkedIn post in your tone** about real BGP work

Just tell me which direction you want to go 🚀
