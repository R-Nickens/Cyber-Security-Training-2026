# 🌐 Cisco Packet Tracer — LAN & DNS Server Lab

## 📌 Project Overview

This project was created in **Cisco Packet Tracer** to practice building and configuring a small local area network (LAN).

The network consists of multiple end devices connected to a **Cisco 2960-24TT switch**, with a dedicated server providing **DNS services**.

The main goal of this lab was to understand how devices communicate within the same IPv4 network and how a DNS server can translate a domain name into an IP address.

---

## 🗺️ Network Topology

The topology contains:

* 1 × Cisco 2960-24TT switch
* 1 × Server
* 2 × PCs
* 1 × Laptop
* Ethernet connections between all devices

```text
                    ┌─────────────┐
                    │    PC1      │
                    │192.168.1.10 │
                    └──────┬──────┘
                           │
                           │
                    ┌──────┴──────┐
                    │             │
              ┌─────┴─────┐      │
              │  Switch0  │──────┼────── Server0
              │ 2960-24TT │      │      192.168.1.100
              └─────┬─────┘      │      DNS: patrick.com
                    │             │
              ┌─────┴─────┐      │
              │    PC2    │      │
              │192.168.1.11│     │
              └────────────┘      │
                                  │
                           ┌──────┴──────┐
                           │   Laptop1   │
                           │192.168.1.12 │
                           └─────────────┘
```

---

## 🧩 IP Addressing

All devices are configured within the same subnet:

**Network:** `192.168.1.0/24`

**Subnet Mask:** `255.255.255.0`

| Device  | IP Address      | Subnet Mask     | Role       |
| ------- | --------------- | --------------- | ---------- |
| PC1     | `192.168.1.10`  | `255.255.255.0` | Client     |
| PC2     | `192.168.1.11`  | `255.255.255.0` | Client     |
| Laptop1 | `192.168.1.12`  | `255.255.255.0` | Client     |
| Server0 | `192.168.1.100` | `255.255.255.0` | DNS Server |

### Why `/24`?

The `/24` network provides:

* Network address: `192.168.1.0`
* Usable host range: `192.168.1.1 – 192.168.1.254`
* Broadcast address: `192.168.1.255`
* Subnet mask: `255.255.255.0`

This is more than enough for this small LAN and makes the addressing scheme easy to understand while learning.

---

## 🖥️ Server Configuration

The server was assigned the static IP address:

```text
IP Address:   192.168.1.100
Subnet Mask:  255.255.255.0
```

The server is configured to provide **DNS (Domain Name System)** functionality.

### DNS Record

The DNS server contains a record for:

```text
patrick.com → 192.168.1.100
```

This allows clients on the network to use the domain name instead of directly entering the server's IP address.

For example:

```text
patrick.com
       │
       ▼
DNS Server
192.168.1.100
```

---

## 🔎 What DNS Does

Before this lab, I understood DNS mainly as the system that translates website names into IP addresses.

This project helped me understand the process more practically.

Instead of accessing a server using:

```text
http://192.168.1.100
```

a client can resolve:

```text
http://patrick.com
```

The DNS server looks up the domain and provides the corresponding IP address:

```text
patrick.com
       ↓
192.168.1.100
```

This demonstrated the relationship between **human-readable domain names** and **IP addresses**.

---

## 🔌 Switching

All end devices are connected to a **Cisco 2960-24TT Layer 2 switch**.

The switch provides connectivity between the devices on the local network.

For example:

```text
PC1 ──┐
PC2 ──┤
      ├── Switch ── Server
Laptop┘
```

Because all devices are in the same `192.168.1.0/24` subnet, they can communicate directly through the switch without requiring a router for local communication.

---

## 🧪 Testing & Verification

After configuring the devices, network connectivity can be tested using `ping`.

### Test 1 — PC1 → Server

```text
ping 192.168.1.100
```

Expected result:

```text
Reply from 192.168.1.100
```

### Test 2 — PC2 → Server

```text
ping 192.168.1.100
```

### Test 3 — PC1 → PC2

```text
ping 192.168.1.11
```

### Test 4 — Laptop → Server

```text
ping 192.168.1.100
```

Successful responses demonstrate that the devices have Layer 3 connectivity within the LAN.

---

## 🧠 What I Learned

### 1. IPv4 Addressing

I learned how to manually assign IPv4 addresses to end devices and servers.

I also became more comfortable understanding the relationship between:

* IP address
* Subnet mask
* Network address
* Host address
* Broadcast address

---

### 2. Subnetting

This project helped reinforce how a `/24` subnet works.

For example:

```text
192.168.1.10/24
192.168.1.11/24
192.168.1.12/24
192.168.1.100/24
```

All of these addresses belong to:

```text
192.168.1.0/24
```

Therefore, they can communicate directly on the local network.

---

### 3. Ethernet Switching

I learned how a Layer 2 switch provides connectivity between devices on the same LAN.

The switch forwards Ethernet frames between connected devices rather than requiring every device to connect directly to every other device.

---

### 4. Client-Server Communication

This lab gave me practical experience with the client-server model.

The PCs and laptop act as **clients**, while the server provides a network service—in this case, DNS.

```text
Clients
   │
   ▼
Switch
   │
   ▼
DNS Server
```

---

### 5. DNS

One of the most important concepts I practiced was DNS.

I learned that DNS allows a domain name such as:

```text
patrick.com
```

to be associated with an IP address:

```text
192.168.1.100
```

This makes network resources easier for users to access and understand.

---

### 6. Troubleshooting

Building the network also helped me understand that connectivity problems can come from several different configuration errors.

When troubleshooting, I learned to check:

1. Physical connections
2. Device interfaces
3. IP addresses
4. Subnet masks
5. DNS configuration
6. Connectivity using `ping`
7. Service configuration on the server

This gave me a more structured approach to troubleshooting network problems.

---

## 🛠️ Tools & Technologies

* **Cisco Packet Tracer**
* IPv4
* Subnetting
* Ethernet
* Cisco 2960 Switch
* DNS
* Client-Server Networking
* ICMP / `ping`
* TCP/IP fundamentals

---

## 🚧 Challenges & Troubleshooting

One of the main lessons from this project was that networking depends heavily on correct addressing and configuration.

A device may be physically connected to the switch but still fail to communicate if:

* The IP address is incorrect
* The subnet mask is incorrect
* The DNS server address is incorrect
* The DNS record is missing
* The server service is disabled
* The cable/interface is not functioning correctly

This helped me understand the importance of troubleshooting networking issues systematically rather than changing configurations randomly.

---

## 📚 Key Takeaways

This project helped me move from understanding networking concepts theoretically to seeing how they work in a simulated environment.

The main concepts I practiced were:

> **IP addressing → Switching → Client/Server communication → DNS → Testing → Troubleshooting**

I also learned that even a small network requires careful planning of IP addresses and services.

---

## 🚀 Future Improvements

I plan to expand this project by adding more networking concepts, such as:

* [ ] Add a router and create multiple networks
* [ ] Configure a default gateway
* [ ] Create multiple VLANs
* [ ] Configure inter-VLAN routing
* [ ] Configure DHCP
* [ ] Add an HTTP/Web server
* [ ] Add an FTP server
* [ ] Configure SSH for network-device management
* [ ] Experiment with ACLs
* [ ] Introduce a second subnet
* [ ] Practice dynamic routing protocols

These improvements will allow me to progress from a simple LAN toward a more realistic enterprise-style network.

---

## 📁 Project Files

```text
.
├── Lab3-Server.pkt
└── README.md
```

### `Lab3-Server.pkt`

The Cisco Packet Tracer project containing the complete network topology and configuration.

---

## 🎯 Learning Progress

This project is part of my ongoing networking learning journey.

Rather than treating each Packet Tracer lab as just an assignment, I am using these projects to build a practical understanding of how computer networks are designed, configured, tested, and troubleshot.

**Next goal:** build a more complex topology using multiple subnets, VLANs, routing, and additional network services.
