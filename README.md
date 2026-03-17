# IPv6 Multi-Site Routing Network (Cisco Packet Tracer)

## Overview

This project simulates a **multi-site IPv6 network** built in Cisco Packet Tracer. The network connects three locations:

* Toledo
* Port Clinton
* Napoleon

Each location contains a **router and a local PC network**. The routers are interconnected using multiple point-to-point links.

The goal of the project was to configure IPv6 networking and implement several routing methods to allow communication between all networks.

This project demonstrates:

* IPv6 network configuration
* Router interface configuration
* Static routing
* RIPng dynamic routing
* OSPFv3 dynamic routing
* IPv6 Access Control Lists (ACLs)
* Network connectivity testing and troubleshooting

---

# Network Topology

The network consists of **three routers connected in a triangular topology**, allowing redundancy between sites.

Each router connects to:

* A local LAN
* Two neighboring routers

This design allows each network to reach the others through multiple routing methods.

<img width="1109" height="1045" alt="Network SS" src="https://github.com/user-attachments/assets/2b17d5ba-5d59-499a-9815-4dc19bca36fc" />


Each site contains:

* 1 Router
* 1 PC
* 1 Local IPv6 subnet

---

# IPv6 Addressing Plan

## Toledo LAN

| Device          | IPv6 Address           | Prefix |
| --------------- | ---------------------- | ------ |
| Router          | 2001:9A01:C10C:1010::1 | /64    |
| PC              | 2001:9A01:C10C:1010::3 | /64    |
| Default Gateway | 2001:9A01:C10C:1010::1 |        |

---

## Port Clinton LAN

| Device          | IPv6 Address           | Prefix |
| --------------- | ---------------------- | ------ |
| Router          | 2001:9A01:C10C:2010::1 | /64    |
| PC              | 2001:9A01:C10C:2010::3 | /64    |
| Default Gateway | 2001:9A01:C10C:2010::1 |        |

---

## Napoleon LAN

| Device          | IPv6 Address           | Prefix |
| --------------- | ---------------------- | ------ |
| Router          | 2001:9A01:C10C:3010::1 | /64    |
| PC              | 2001:9A01:C10C:3010::3 | /64    |
| Default Gateway | 2001:9A01:C10C:3010::1 |        |

---

## Router-to-Router Networks

| Link                    | Network                  |
| ----------------------- | ------------------------ |
| Toledo ↔ Port Clinton   | 2001:9A01:C10C:4010::/64 |
| Toledo ↔ Napoleon       | 2001:9A01:C10C:5010::/64 |
| Port Clinton ↔ Napoleon | 2001:9A01:C10C:6010::/64 |

---

# Router Interface Configuration

Each router interface was manually configured with an IPv6 address and enabled.

Example configuration:

```
interface GigabitEthernet0/0
 ipv6 address 2001:9A01:C10C:3010::1/64
 no shutdown
```

IPv6 forwarding was enabled globally:

```
ipv6 unicast-routing
```

This allows the router to forward IPv6 packets between interfaces.

---

# Static Routing

Static routes were configured so routers could reach remote networks.

Example:

```
ipv6 route 2001:9A01:C10C:1010::/64 2001:9A01:C10C:5010::1
```

This instructs the router to forward packets destined for the Toledo network to the next-hop router.

Static routing provides **full manual control over network paths**.

---

# RIPng Configuration

Dynamic routing was implemented using **RIPng (Routing Information Protocol for IPv6)**.

RIPng allows routers to automatically share network information and update routing tables.

Example configuration:

```
ipv6 router rip NETWORK
interface GigabitEthernet0/0
 ipv6 rip NETWORK enable
```

Advantages of RIPng:

* Automatic route learning
* Simplified configuration
* Easier scalability than static routes

---

# OSPFv3 Configuration

The network was also configured using **OSPFv3**, a link-state routing protocol designed for IPv6.

Example configuration:

```
ipv6 router ospf 1
router-id 1.1.1.1

interface GigabitEthernet0/0
 ipv6 ospf 1 area 0
```

Advantages of OSPFv3:

* Faster convergence
* Scalable for large networks
* More efficient routing than RIP

---

# Access Control Lists (ACLs)

IPv6 Access Control Lists were configured to control network traffic.

Example:

```
ipv6 access-list BLOCK_TRAFFIC
 deny ipv6 any 2001:9A01:C10C:3010::/64
 permit ipv6 any any
```

ACLs allow administrators to:

* Block specific traffic
* Allow permitted traffic
* Implement security policies

---

# Connectivity Testing

Connectivity was verified using `ping` commands from both routers and PCs.

Example test:

```
ping 2001:9A01:C10C:2010::3
```

Successful results showed:

```
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

Testing confirmed:

* PC-to-router connectivity
* PC-to-PC connectivity across sites
* Router-to-router communication

---

# Verification Commands

Useful Cisco commands used during testing:

```
show ipv6 route
show running-config
show ipv6 interface
ping ipv6 <address>
```

These commands verify:

* Routing tables
* Interface status
* Connectivity

---

# Repository Structure

```
Final Project CSET 4750
│
├── 0Router Setup
│
├── 1Static Routes
│
├── 2RIP Routes
│
├── 3OSPF Routes
│
├── 4Access List
│
└── Screenshots
```

Each folder contains router configuration files and command outputs for the corresponding routing method.

---

# Screenshots

The repository includes screenshots demonstrating:

* PC IPv6 configurations
* Router CLI configuration
* Static route tables
* RIP routing tables
* OSPF routing tables
* Successful ping tests between all sites

---

# Learning Outcomes

This project demonstrates practical understanding of:

* IPv6 network architecture
* Router configuration using Cisco IOS
* Static routing implementation
* Dynamic routing with RIPng
* Dynamic routing with OSPFv3
* Network security using ACLs
* Network troubleshooting and verification

---

# Tools Used

Cisco Packet Tracer
Cisco IOS CLI
GitHub

---

# Author

AJ Flower
University of Toledo

Course: **CSET 4750 – Networking**
