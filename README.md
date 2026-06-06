
# 📡 RIPv2 Dynamic Routing Infrastructure

## 🛡️ Core Objective
Autonomous multi-subnet network architecture designed and deployed using **Routing Information Protocol (RIPv2)** inside Cisco Packet Tracer. The infrastructure eliminates static pathway definitions, allowing classless telemetry synchronization across multiple edge networks dynamically.

---

## 🗺️ Architectural Topology Matrix
![Network Topology](./topology.png)

### Network Architecture Key Metrics
* **Routing Protocol:** RIPv2 (Classless Routing with CIDR)
* **Transport Layer:** UDP Port 520
* **Metric Metric:** Hop Count (Max 15 Hops)
* **Subnet Synchronization:** Updated dynamically every 30 seconds

### IP Addressing Architecture
| Device | Interface | Assigned IP | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **PC0** | Fa0 (NIC) | `10.0.0.1` | `255.0.0.0` | `10.0.0.10` |
| **PC1** | Fa0 (NIC) | `20.0.0.1` | `255.0.0.0` | `20.0.0.10` |
| **PC2** | Fa0 (NIC) | `30.0.0.1` | `255.0.0.0` | `30.0.0.10` |
| **Router0** | Fa0/0 | `10.0.0.10` | `255.0.0.0` | — |
| **Router0** | Fa0/1 | `192.168.1.1` | `255.255.255.0` | — |
| **Router1** | Fa0/1 | `192.168.1.2` | `255.255.255.0` | — |
| **Router1** | Fa0/0 | `20.0.0.10` | `255.0.0.0` | — |
| **Router1** | Fa0/3 | `30.0.0.10` | `255.0.0.0` | — |

---

## 🛠️ CLI Core Engine Deployments

### Router0 Configuration (Boundary Edge)
```text
Router0> enable
Router0# configure terminal
Router0(config)# router rip
Router0(config-router)# version 2
Router0(config-router)# network 10.0.0.0
Router0(config-router)# network 192.168.1.0
Router0(config-router)# no auto-summary
Router0(config-router)# exit
Router0# write

```

### Router1 Configuration (Internal Gateway)

```text
Router1> enable
Router1# configure terminal
Router1(config)# router rip
Router1(config-router)# version 2
Router1(config-router)# network 192.168.1.0
Router1(config-router)# network 20.0.0.0
Router1(config-router)# network 30.0.0.0
Router1(config-router)# no auto-summary
Router1(config-router)# exit
Router1# write

```

---

## 🧪 Verification & Telemetry Output

### Verified Routing Logs via `show ip route` on Router0:

```text
     10.0.0.0/8 is variably subnetted
C        10.0.0.0/8 is directly connected, FastEthernet0/0
C        192.168.1.0/24 is directly connected, FastEthernet0/1
R        20.0.0.0/8 [120/1] via 192.168.1.2, 00:00:14, FastEthernet0/1
R        30.0.0.0/8 [120/1] via 192.168.1.2, 00:00:14, FastEthernet0/1

```

> 📌 **Metrics Parsed:** `[120/1]` indicates an Administrative Distance of 120 (RIP Standard) and a Hop Count of 1 to reach remote segments.

### End-to-End Connectivity Status

* **PC0 to PC1 (20.0.0.1):** `SUCCESS` (via dynamic RIP routing interface)
* **PC0 to PC2 (30.0.0.1):** `SUCCESS` (via dynamic RIP routing interface)

```

Isay save (commit) kar dein, aapka poora professional data ek baar mein upload ho jayega!

```
