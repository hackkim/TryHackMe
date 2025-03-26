# TryHackMe - Intro to LAN

> A beginner-friendly introduction to Local Area Networks (LANs): topologies, switches, routers, subnetting, ARP, and DHCP.

---

## 🏷️ Task 1: LAN Topologies + Switches & Routers

### 1. LAN Topologies

A **network topology** describes how devices connect within a LAN.  
Common topologies include:

1. **Star Topology**  
   - All devices connect to a central hub or switch.  
   - ✅ Easy to expand  
   - ❌ If the central device fails, the entire network can fail


  ![Star Topology Diagram](https://github.com/user-attachments/assets/fce384ee-583e-4d76-acf0-29a1703e9c22)

2. **Bus Topology**  
   - All devices share a single backbone cable.  
   - ✅ Simple and inexpensive  
   - ❌ One break can bring down the whole network

   ![Bus Topology Diagram](https://github.com/user-attachments/assets/dfef707f-cb0f-4857-9e8b-9989b9f7e426)

3. **Ring Topology**  
   - Devices form a closed loop; data travels in one direction.  
   - ✅ Reduced collisions  
   - ❌ One fault disrupts the entire ring


   ![Ring Topology Diagram](https://github.com/user-attachments/assets/bd44c84c-1300-4c25-ab1c-0929ffa5033c)

---

### 2. What is a Switch?

A **Switch** is a device that connects multiple devices within a LAN and forwards data based on **MAC addresses**.

- Operates at **Layer 2** (Data Link layer) of the OSI model  
- Maintains a MAC address table to reduce unnecessary traffic  
- Modern LANs typically use switches for efficiency

 
![Switch Diagram](https://github.com/user-attachments/assets/8bee6c27-2af2-4df1-b0fd-c29ef6602981)

---

### 3. What is a Router?

A **Router** connects different networks (e.g., LAN to the Internet) and forwards data packets based on **IP addresses**.

- Operates at **Layer 3** (Network layer) of the OSI model  
- Uses routing tables to find the best path  
- Performs **NAT** (Network Address Translation) for multiple LAN hosts to share one public IP

![Router Diagram](https://github.com/user-attachments/assets/f7796bfe-312f-4b9b-899b-2115a0b261f4)

---

## 🧩 Task 2: A Primer on Subnetting

**Subnetting** is the practice of dividing a network into smaller subnetworks for:

- **Efficiency** (smaller broadcast domains)  
- **Security** (isolating sensitive segments)  
- **Manageability** (allocating IP ranges by department)

Example:  
Split a corporate network into subnets for different teams or a café network into Staff vs. Guest subnets.

![Subnetting Example](https://github.com/user-attachments/assets/218574bf-2775-4c5c-b76d-640e995cc285)

---

## 🔄 Task 3: ARP (Address Resolution Protocol)

**ARP** maps IP addresses to MAC addresses within the same LAN.

1. **ARP Request** – Broadcast: “Who has 192.168.1.10?”  
2. **ARP Reply** – The device with that IP responds with its MAC address.

Devices store these mappings in an ARP cache for quicker lookups.

  
![ARP Process Diagram](https://github.com/user-attachments/assets/19a28acb-9c63-44fc-9d2b-704267bab755)

---

## 📡 Task 4: DHCP (Dynamic Host Configuration Protocol)

**DHCP** automatically assigns IP addresses, subnet masks, default gateways, and DNS server info to devices.

Typical workflow:

1. **DHCP Discover** – Client broadcasts to find a DHCP server.  
2. **DHCP Offer** – Server offers an IP lease.  
3. **DHCP Request** – Client requests the offered IP.  
4. **DHCP ACK** – Server confirms the IP assignment.

**Advantages**:

- No manual IP configuration  
- Avoid IP conflicts  
- Centralized IP management

![DHCP Workflow](https://github.com/user-attachments/assets/96ca1118-5ad8-4ba1-bbdb-eb992b87f213)

---

## 📌 Conclusion

In this **Intro to LAN** room, you explored:

- **LAN Topologies** (Star, Bus, Ring)
- **Switches** (Layer 2) and **Routers** (Layer 3)
- **Subnetting** for dividing networks
- **ARP** to resolve IP-to-MAC
- **DHCP** for automatic IP assignment

Mastering these fundamentals is essential before moving on to advanced networking topics like VLANs, routing protocols, and network security tools.
