# 🌐 CCNA Network Topology Analyzer

<div align="center">

[![Live Demo](https://img.shields.io/badge/▶_Live_Demo-3B82F6?style=for-the-badge)](https://sazzadmahfuz.github.io/ccna-network-analyzer)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](.)
[![Cisco](https://img.shields.io/badge/CCNA-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)](.)
[![Course](https://img.shields.io/badge/HAMK-CCNA_Networking-003087?style=for-the-badge)](.)

> **Course project for CCNA: Introduction to Networks — HAMK / Cisco Networking Academy**  
> Interactive drag-and-drop network topology builder with Dijkstra's shortest-path algorithm, ping packet simulation, per-node routing tables, and a full device inventory panel.

</div>

---

## 📸 Screenshot

```
┌───────────────────────────────────────────────┬────────────────┐
│  NET ANALYZER     drag nodes · click to select │ [Add][Info]... │
│                                               │                │
│              🔷 R1 (192.168.1.1)             │  Node type     │
│             ╱          ╲                     │  [🔷 Router]   │
│       🔷 R2              🔷 R3               │  [🔶 Switch]   │
│       │  (192.168.2.1)  (192.168.3.1)  │    │  [💻 Host PC]  │
│      🔶 SW1             🔶 SW2               │  [🖥 Server]   │
│     ╱    ╲             ╱    ╲                │                │
│  💻 PC1  💻 PC2     💻 PC3  💻 PC4           │  [+ Add node]  │
│                                               │  [📡 Ping]     │
│  ─────── DIJKSTRA PATH: R1→R2→SW1→PC1 ──────│  [🗺 Dijkstra] │
│  Nodes: 9 · Links: 8            [+][🔗][🗑][⊞]│                │
└───────────────────────────────────────────────┴────────────────┘
```

---

## ✨ Features

| Feature | Description |
|---|---|
| **Drag-and-Drop Canvas** | Reposition any device freely on the topology canvas |
| **4 Device Types** | Router 🔷, Switch 🔶, Host PC 💻, Server 🖥 — each with unique rendering |
| **Link Mode** | Click 🔗 then click two nodes to draw a link; link cost auto-assigned |
| **Dijkstra Shortest Path** | Highlights the minimum-cost path between first and last node in amber |
| **Ping Simulation** | Animated packet travels the optimal path with trail effect |
| **Per-Node Routing Table** | Select any router/switch to see its adjacency-based routing table |
| **Node Info Panel** | IP, MAC, subnet, gateway, connection count for selected device |
| **Default Topology** | Pre-loaded 3-router, 2-switch, 4-PC hierarchy — typical CCNA lab |
| **Fit All / Reset** | Auto-centre all nodes or restore the default topology |
| **Link Cost Labels** | Every link shows its routing cost (used by Dijkstra) |

---

## 🧠 Algorithms & Networking Concepts

### Dijkstra's Shortest Path Algorithm

The shortest-path computation uses a **greedy priority approach** — the same algorithm underpinning OSPF (Open Shortest Path First), the dominant routing protocol in enterprise networks and a core CCNA exam topic.

```javascript
function dijkstra(src, dst) {
    const dist = {}, prev = {};
    nodes.forEach(n => { dist[n.id] = Infinity; prev[n.id] = null; });
    dist[src.id] = 0;
    const unvisited = new Set(nodes.map(n => n.id));

    while (unvisited.size) {
        // Pick unvisited node with lowest tentative distance
        let u = null;
        unvisited.forEach(id => { if (u === null || dist[id] < dist[u]) u = id; });
        if (u === null || dist[u] === Infinity) break;
        unvisited.delete(u);
        if (u === dst.id) break;

        // Relax edges
        links.filter(l => l.a === u || l.b === u).forEach(l => {
            const v   = l.a === u ? l.b : l.a;
            const alt = dist[u] + l.cost;          // link cost = metric
            if (alt < dist[v]) { dist[v] = alt; prev[v] = u; }
        });
    }
    // Reconstruct path by backtracking prev[]
    const path = []; let cur = dst.id;
    while (cur) { path.unshift(nodes.find(n => n.id === cur)); cur = prev[cur]; }
    return path[0]?.id === src.id ? path : [];
}
```

**Complexity**: O(V²) with adjacency list — optimal for the small topologies typical in CCNA labs.

### Network Addressing Model

Each device is auto-assigned a realistic IP based on its type, mirroring CCNA addressing conventions:

| Device Type | Address Block | Example |
|---|---|---|
| Router | `192.168.x.x/24` | 192.168.1.1 |
| Switch | `10.0.x.x/24` | 10.0.1.1 |
| Host PC | `172.16.x.x/24` | 172.16.1.10 |
| Server | `10.10.x.x/24` | 10.10.1.1 |

This matches the RFC 1918 private address space organisation tested in the Cisco CCNA exam.

### Routing Table Logic

Each node's routing table is computed from its **direct adjacencies** — equivalent to directly connected routes (the `C` entries in a Cisco `show ip route` output):

```javascript
// For selected node n, neighbours nb:
// Dest           Next Hop   Cost    Interface
// 10.0.1.0/24    10.0.1.1   2       eth0
// 172.16.1.0/24  172.16.1.10 4      eth1
```

---

## 🗂️ File Structure

```
ccna-network-analyzer/
└── index.html        # Self-contained — Canvas 2D API, Dijkstra, all interaction in-browser
```

---

## 🔗 CCNA Exam Topics Covered

This project demonstrates practical understanding of:

- ✅ **Network topology types** (hierarchical: core → distribution → access)
- ✅ **IPv4 addressing and subnetting** (RFC 1918 private ranges)
- ✅ **MAC addressing** (48-bit hex notation)
- ✅ **Routing concepts** (routing table, next-hop, cost/metric)
- ✅ **OSPF metric model** (Dijkstra is the OSPF SPF algorithm)
- ✅ **ICMP / Ping** (connectivity verification between hosts)
- ✅ **Layer 2 vs Layer 3 devices** (switch vs router distinction)

---

## 🎓 Academic Context

**Course**: CCNA: Introduction to Networks (Cisco Networking Academy via HAMK)  
**Certificate**: Cisco CCNA — Introduction to Networks (March 2025)  
**Programme**: BEng ICT & Robotics, HAMK University of Applied Sciences  
**Topics covered**: OSI model, IP addressing, routing protocols, switching, OSPF, ICMP.

---

## 👤 Author

**Sazzad Ibna Mahfuz** — BEng ICT & Robotics, HAMK · Cisco CCNA Certified  
[Portfolio](https://sazzadmahfuz.github.io) · [LinkedIn](https://www.linkedin.com/in/sazzad-mahfuz) · [GitHub](https://github.com/sazzadmahfuz)
