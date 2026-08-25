# Router Between Two Networks — Cisco Packet Tracer Lab

## 📌 Project Overview

This lab demonstrates how a **router connects two different IP networks** and allows devices on one network to communicate with devices on another network.

The topology was built in **Cisco Packet Tracer** and contains:

* 2 end devices
* 2 Cisco 2960 switches
* 1 Cisco ISR4331 router
* 2 separate IPv4 networks

The main learning objective was to understand how a router acts as the **default gateway** and forwards packets between different subnets.

## 🎯 Session Learning Objectives

By completing this lab, I learned how to:

* Understand communication between two different IPv4 networks.
* Configure IP addresses on end devices.
* Configure router interfaces with IP addresses.
* Configure the correct default gateway on hosts.
* Understand the role of a Layer 3 router in inter-network communication.
* Connect end devices to switches and switches to a router.
* Verify connectivity using `ping`.
* Identify common causes of connectivity problems.
* Understand how subnet masks determine whether devices are on the same network.

## 🗺️ Network Topology

```text
PC3
192.168.1.11/24
Gateway: 192.168.1.1
      |
   Switch1
      |
   Router0
  /        \
Network 1  Network 2
192.168.1.1  192.168.2.1
      |        |
   Switch2
      |
Laptop2
192.168.2.12/24
Gateway: 192.168.2.1
```

## 📊 Addressing Table

| Device  | IP Address     | Subnet Mask     | Default Gateway |
| ------- | -------------- | --------------- | --------------- |
| PC3     | `192.168.1.11` | `255.255.255.0` | `192.168.1.1`   |
| Router0 | `192.168.1.1`  | `255.255.255.0` | —               |
| Router0 | `192.168.2.1`  | `255.255.255.0` | —               |
| Laptop2 | `192.168.2.12` | `255.255.255.0` | `192.168.2.1`   |

### Networks

* **Network 1:** `192.168.1.0/24`
* **Network 2:** `192.168.2.0/24`

## 🔧 Router Configuration

```text
enable
configure terminal

interface GigabitEthernet0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface GigabitEthernet0/0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

end
```

> Interface names may vary depending on the Packet Tracer router model.

## 🧪 Connectivity Testing

From PC3:

```text
ping 192.168.1.1
ping 192.168.2.1
ping 192.168.2.12
```

From Laptop2:

```text
ping 192.168.2.1
ping 192.168.1.1
ping 192.168.1.11
```

Successful communication between `192.168.1.11` and `192.168.2.12` demonstrates that the router is forwarding traffic between the two networks.

## 🧠 What I Learned

### Default Gateway

When a host wants to communicate with a device outside its own subnet, it sends the traffic to its **default gateway**.

* PC3 → `192.168.1.1`
* Laptop2 → `192.168.2.1`

### Router vs Switch

A **switch** primarily connects devices within a LAN, while a **router** connects different IP networks and forwards packets between them.

### Directly Connected Networks

Because both networks are directly connected to Router0, the router automatically knows about them.

```text
192.168.1.0/24 → directly connected
192.168.2.0/24 → directly connected
```

## 🔍 Verification Commands

```text
show ip interface brief
```

Checks interface status and IP addresses.

```text
show ip route
```

Displays the router's routing table.

```text
show running-config
```

Displays the current configuration.

```text
ping 192.168.2.12
```

Tests connectivity from the router to the remote host.

## 🛠️ Troubleshooting Checklist

If connectivity fails, check:

* IP addresses
* Subnet masks
* Default gateways
* Router interface configuration
* `no shutdown`
* Cable connections
* Switch/router interface status
* Routing table
* Local gateway connectivity

A useful approach is to troubleshoot **one hop at a time**, starting with the local gateway and moving toward the remote host.

## 📚 Key Concepts

| Concept         | What I Learned                               |
| --------------- | -------------------------------------------- |
| IPv4 Address    | Identifies a device on an IP network         |
| Subnet Mask     | Defines the network and host portions        |
| `/24`           | Equivalent to `255.255.255.0`                |
| Default Gateway | Used to reach other networks                 |
| Switch          | Connects devices within a LAN                |
| Router          | Connects different networks                  |
| Routing Table   | Determines where packets should be forwarded |
| `ping`          | Tests IP connectivity using ICMP             |

## 🚀 Next Steps

Future labs I can build from this project:

* Static routing
* OSPF
* VLANs
* Inter-VLAN routing
* DHCP
* Access Control Lists (ACLs)
* Multiple routers
* Network troubleshooting
* Packet analysis using Simulation Mode

## 💡 Key Takeaway

This lab helped me understand one of the fundamental concepts of networking:

> **A router connects different IP networks and forwards traffic between them.**

The basic communication flow is:

```text
Host
  ↓
Default Gateway
  ↓
Router
  ↓
Destination Network
```

This project is part of my networking learning journey and demonstrates practical experience with **IPv4 addressing, subnetting, routing, default gateways, and connectivity troubleshooting**.
::: 
