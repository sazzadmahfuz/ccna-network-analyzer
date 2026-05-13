# 🌐 CCNA Network Topology Analyzer

<div align="center">

[![Live Demo](https://img.shields.io/badge/▶_Live_Demo-3B82F6?style=for-the-badge)](https://sazzadmahfuz.github.io/ccna-network-analyzer)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](.)
[![Cisco](https://img.shields.io/badge/CCNA-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)](.)
[![Canvas API](https://img.shields.io/badge/Canvas_API-7B61FF?style=for-the-badge)](.)
[![Networking](https://img.shields.io/badge/Network_Analysis-Dijkstra-orange?style=for-the-badge)](.)
[![Course](https://img.shields.io/badge/HAMK-CCNA_Networking-003087?style=for-the-badge)](.)

> **Course project for CCNA: Introduction to Networks — HAMK / Cisco Networking Academy**  
> Advanced interactive network topology simulator featuring drag-and-drop device management, Dijkstra shortest-path routing, ICMP ping simulation, routing table generation, topology analysis, and enterprise-inspired network visualisation.

---

### Developed by

# Sazzad Ibna Mahfuz

Bachelor of Engineering — ICT Robotics  
Häme University of Applied Sciences (HAMK), Finland

</div>

---


## Project Overview

This project demonstrates a fully interactive **network topology analysis and simulation environment** inspired by real enterprise networking tools and Cisco CCNA laboratory exercises.

using:

- JavaScript
- HTML5 Canvas API
- Networking algorithms
- Graph theory
- Routing logic
- Cisco CCNA concepts

The application simulates core networking operations including:

- Network topology design
- Router and switch connectivity
- Pathfinding algorithms
- ICMP ping simulation
- Routing table generation
- Link metrics and costs
- Network device inventory
- Interactive topology management

The project reflects practical networking concepts commonly used in:

- Cisco Packet Tracer
- GNS3
- EVE-NG
- Enterprise routing environments
- Network monitoring systems

---

## System Interface Preview

```text
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

## Features

| Feature | Description |
|---|---|
| **Interactive Topology Canvas** | Fully draggable and editable network topology workspace |
| **4 Device Categories** | Routers, Switches, Host PCs, and Servers with unique rendering |
| **Dynamic Link Creation** | Interactive link mode for creating network connections |
| **Dijkstra Shortest Path Algorithm** | Real-time path optimisation between devices |
| **Ping Packet Simulation** | Animated ICMP-style packet traversal |
| **Per-Node Routing Table** | Dynamically generated routing information |
| **Device Inventory Panel** | Live topology device management system |
| **Routing Metrics** | Cost-based path calculations |
| **Default Enterprise Topology** | Pre-built hierarchical CCNA-style lab network |
| **Topology Auto-Centering** | Automatic graph fitting and layout management |
| **Network Statistics** | Real-time node and link tracking |
| **Responsive UI** | Optimised for desktop and modern browsers |

---

## Networking Concepts Demonstrated

The project combines several fundamental networking and graph theory concepts commonly studied in CCNA and enterprise networking.

### Core Concepts Covered

- IPv4 addressing
- Routing and switching
- Graph traversal algorithms
- OSPF shortest-path calculation
- ICMP packet simulation
- Routing table generation
- Network topology hierarchy
- Link metrics and costs
- Layer 2 vs Layer 3 networking
- Enterprise network visualisation

---

## System Architecture

The topology system models a hierarchical enterprise network structure.

```text
                    Core Router
                         │
          ┌──────────────┴──────────────┐
          │                             │
    Distribution Router           Distribution Router
          │                             │
      Access Switch                Access Switch
       │        │                  │         │
      PC       PC                 PC        PC
```

The architecture follows standard CCNA hierarchical design principles:

| Layer | Purpose |
|---|---|
| Core Layer | Backbone routing |
| Distribution Layer | Routing aggregation |
| Access Layer | End-device connectivity |

---

## Device Types

The simulator supports multiple enterprise network devices.

| Device | Role |
|---|---|
| Router | Layer 3 packet routing |
| Switch | Layer 2 frame forwarding |
| Host PC | End-user client device |
| Server | Centralised network services |

Each device includes:

- IP address
- MAC address
- subnet mask
- gateway
- connection count
- routing information

---

## Dijkstra Shortest Path Algorithm

The application implements the **Dijkstra Shortest Path First (SPF)** algorithm used in:

- OSPF routing
- graph optimisation
- enterprise routing protocols

The algorithm computes the minimum-cost route between two devices based on:

- link cost
- topology structure
- cumulative path weight

---

## Dijkstra Workflow

```text
Source Router
      │
      ▼
Evaluate Neighbor Costs
      │
      ▼
Select Lowest Distance Node
      │
      ▼
Update Path Metrics
      │
      ▼
Repeat Until Destination Found
      │
      ▼
Generate Shortest Path
```

---

## Dijkstra Algorithm Implementation

```javascript
function dijkstra(src, dst) {

    const dist = {}, prev = {};

    nodes.forEach(n => {
        dist[n.id] = Infinity;
        prev[n.id] = null;
    });

    dist[src.id] = 0;

    const unvisited = new Set(nodes.map(n => n.id));

    while (unvisited.size) {

        let u = null;

        unvisited.forEach(id => {
            if (u === null || dist[id] < dist[u]) {
                u = id;
            }
        });

        if (u === dst.id) break;

        unvisited.delete(u);

        links
            .filter(l => l.a === u || l.b === u)
            .forEach(l => {

                const v = l.a === u ? l.b : l.a;

                const alt = dist[u] + l.cost;

                if (alt < dist[v]) {
                    dist[v] = alt;
                    prev[v] = u;
                }
            });
    }
}
```

---

## Relation to OSPF Routing

The simulator directly reflects the behaviour of:

### Open Shortest Path First (OSPF)

used in real enterprise routers.

OSPF internally uses:

```text
Dijkstra Shortest Path First Algorithm
```

to compute:

- optimal routes
- routing metrics
- path selection
- next-hop calculation

This makes the project highly relevant to:

- Cisco CCNA
- enterprise routing
- Layer 3 networking

---

## Ping Packet Simulation

The dashboard includes an animated packet simulation system inspired by:

- ICMP echo requests
- traceroute visualisation
- packet flow analysis

The animation simulates:

```text
Source Device
      │
      ▼
Shortest Path Traversal
      │
      ▼
Destination Device
      │
      ▼
Reply Returned
```

The packet animation includes:

- motion interpolation
- trail effects
- route highlighting
- visual feedback

---

## Routing Table Generation

Each selected node dynamically generates a routing table based on:

- connected interfaces
- neighbouring devices
- link metrics

Example:

```text
Destination        Next Hop       Cost     Interface
10.0.1.0/24        10.0.1.1       2        eth0
172.16.1.0/24      172.16.1.10    4        eth1
```

This reflects the structure of:

```bash
show ip route
```

used in Cisco IOS.

---

## IPv4 Addressing Model

The project uses realistic RFC1918 private addressing ranges.

| Device Type | Address Range |
|---|---|
| Routers | 192.168.x.x |
| Switches | 10.0.x.x |
| PCs | 172.16.x.x |
| Servers | 10.10.x.x |

This mirrors real enterprise addressing practices taught in CCNA coursework.

---

## MAC Address Simulation

Each device receives a randomly generated:

```text
48-bit hexadecimal MAC address
```

Example:

```text
7a:4f:91:2d:af:31
```

This demonstrates:

- Layer 2 addressing
- Ethernet concepts
- network interface identification

---

## Interactive Topology System

The topology editor allows users to:

- drag devices
- create links
- delete nodes
- analyse paths
- view metrics
- simulate connectivity

The entire graph operates dynamically inside the browser using:

### HTML5 Canvas 2D API

---

## Link Metrics and Costs

Every network connection contains a randomly assigned:

```text
Link Cost
```

used by the routing engine.

Example:

| Link | Cost |
|---|---|
| R1 → R2 | 2 |
| R2 → SW1 | 3 |
| SW1 → PC1 | 1 |

The shortest-path system calculates:

```text
Total Path Cost = Sum of Link Costs
```

---

## Canvas Rendering Engine

The application uses:

```text
CanvasRenderingContext2D
```

to render:

- routers
- switches
- links
- packet animations
- labels
- routing highlights
- topology overlays

The rendering system updates dynamically during:

- dragging
- routing
- packet simulation
- path calculation

---

## User Interaction System

Supported interactions include:

| Interaction | Action |
|---|---|
| Click | Select device |
| Drag | Move device |
| Link Mode | Create connections |
| Ping | Simulate ICMP |
| Dijkstra | Compute shortest path |
| Reset | Restore default topology |
| Fit All | Center graph |

---

## Default Enterprise Topology

The simulator ships with a default CCNA-style network including:

- 3 routers
- 2 switches
- 4 PCs

representing a small enterprise architecture.

The default topology demonstrates:

- hierarchical networking
- subnet separation
- routing distribution
- access-layer connectivity

---

## Educational Objectives

The project was designed to reinforce understanding of:

- network topology design
- routing protocols
- graph algorithms
- IPv4 addressing
- OSPF principles
- packet forwarding
- subnetting concepts
- network visualisation
- Layer 2 and Layer 3 operations

---

## Learning Outcomes

This project helped develop practical skills in:

- JavaScript application engineering
- Canvas graphics programming
- networking algorithms
- routing logic
- enterprise topology design
- graph data structures
- network visualisation systems
- interactive UI systems
- shortest-path computation
- packet simulation

---

## Industrial Relevance

The concepts demonstrated are widely used in:

- enterprise networking
- ISP infrastructure
- data centers
- cloud networking
- Cisco environments
- network monitoring systems

The project reflects practical concepts used by:

- Network Engineers
- CCNA Engineers
- Infrastructure Specialists
- Systems Administrators
- Network Operations Centers (NOC)

---

## Future Improvements

Potential future extensions include:

- Real packet simulation
- VLAN support
- OSPF neighbour states
- Spanning Tree Protocol simulation
- DHCP server implementation
- DNS simulation
- Firewall rules
- TCP/UDP packet analysis
- Wireshark-style monitoring
- Real subnet calculator
- IPv6 support
- Multi-area OSPF
- Routing protocol comparison
- Cisco CLI emulator
- WebSocket multi-user collaboration

---

## Academic Context

**Course**: CCNA: Introduction to Networks (Cisco Networking Academy via HAMK)  
**Certificate**: Cisco CCNA — Introduction to Networks (March 2025)  
**Programme**: BEng ICT & Robotics, HAMK University of Applied Sciences  

### Topics Covered

- OSI Model
- IPv4 Addressing
- Routing and Switching
- OSPF Routing Protocol
- ICMP and Ping
- MAC Addressing
- Ethernet Networking
- Network Topology Design
- Routing Metrics
- Cisco Networking Fundamentals

---

## Performance Characteristics

| Component | Performance |
|---|---|
| Topology Rendering | Real-time |
| Dijkstra Calculation | O(V²) |
| Packet Animation | Smooth browser rendering |
| Node Management | Dynamic |
| UI Rendering | Responsive |
| Canvas Updates | Real-time |

---

## Real Enterprise Mapping

| Project Feature | Real Industry Equivalent |
|---|---|
| Dijkstra Routing | OSPF SPF Calculation |
| Routing Table | Cisco IOS Routing Table |
| Ping Simulation | ICMP Echo |
| Device Inventory | Network Monitoring Systems |
| Link Costs | Routing Metrics |
| Interactive Graph | Topology Management Tools |

---

## Technical Implementation

The complete system was implemented using:

| Technology | Purpose |
|---|---|
| HTML5 | Application structure |
| CSS3 | Enterprise-inspired UI styling |
| JavaScript | Logic and networking algorithms |
| Canvas API | Topology rendering |
| Graph Theory | Pathfinding algorithms |

The entire application runs fully client-side inside the browser without external backend infrastructure.

---

## Conclusion

This project demonstrates a comprehensive implementation of interactive networking concepts commonly studied in Cisco CCNA coursework and enterprise networking environments.

The system combines:

- graph algorithms
- routing logic
- topology visualisation
- packet simulation
- interactive UI systems
- enterprise networking concepts

into a fully functional browser-based network simulator.

The project reflects real networking workflows used in:

- enterprise routing environments
- educational networking labs
- topology analysis systems
- infrastructure monitoring tools

while providing hands-on visual understanding of:

- shortest-path routing
- IP networking
- routing tables
- packet traversal
- network hierarchy
- OSPF principles

---

## 👤 Author

**Sazzad Ibna Mahfuz** — BEng ICT & Robotics, HAMK · Cisco CCNA Certified  
[Portfolio](https://sazzadmahfuz.github.io) · [LinkedIn](https://www.linkedin.com/in/sazzad-mahfuz) · [GitHub](https://github.com/sazzadmahfuz)


<div align="center">

# ⭐ If you found this project interesting, consider starring the repository!

</div>
