# 📚 Activity 2: DHCP and DNS
## 🎯 Objective
Configure a DHCP and DNS server in the Library Building using Packet Tracer. You will set up automatic IP address assignment and enable domain name resolution for local devices.

---

## 🧰 What You’ll Need
- Cisco Packet Tracer
- Basic understanding of DHCP and DNS
- Familiarity with Packet Tracer interface

---

## 🗺️ Scenario
The Library Building is being upgraded with network automation. Instead of manually assigning IP addresses, you will configure a DHCP server to handle this task. Additionally, you’ll set up a DNS server so that devices can resolve domain names like `library.pc01`.

---

## 🛠️ Step-by-Step Instructions

### Step 1: Create the Network Topology
1. Open Packet Tracer.
2. Drag **1 Switch**, **1 Server**, and **3 PCs** onto the workspace.
3. Use **Copper Straight-Through cables** to connect:
   - Server → Switch (Fa0/1)
   - PC0 → Switch (Fa0/2)
   - PC1 → Switch (Fa0/3)
   - PC2 → Switch (Fa0/4)

---

### Step 2: Configure the Server
1. First, assign an IP address to the Server, as we did it in Activity 1:

| Parameters | Address Value |
| --- | --- |
| Static IPv4 | 192.168.2.2 |
| Subnet mask | 255.255.255.0|
| Default Gateway | 192.168.2.1 |

2. Inside the Server → Go to **Services** tab.
2. Enable **DHCP**. Modify and save the following parameters in the "serverPool"
   - Default Gateway: `192.168.2.1`
   - DNS Server: `192.168.2.2`
   - Start IP Address: `192.168.2.100`
   - Subnet Mask: `255.255.255.0`
   - Maximum Number of Users: `50`

2. Configure de *DNS*:
    - Go to the **Services** tab on the server.
    - Active the DNS service **ON** (The server IP must match the one used in the DHCP pool)
    - Now, add as many names (alias) as you'd like, having into account their IPs. For instance:
      - "library_pc1" -- 192.168.2.100
      - "pc2_library" -- 192.168.2.101
      
      As long as they are the IPs assigned by our previous DHCP.

---
### Step 3: Configure PCs to Use DHCP
1. Click each PC → Desktop tab → IP Configuration.
2. Select **DHCP**.
3. Wait for IP assignment from the server.


---

### Step 5: Test Connectivity and DNS
1. Open **Command Prompt** on a PC.
2. Use `ping library.pc01` to test DNS resolution.
3. Use `ipconfig /all` to verify DHCP settings.

✅ **Expected Result**: PCs should receive IPs automatically and successfully ping `library.pcXX`.

---

## 🧠 Reflection Questions
1. What are the advantages of using DHCP over static IPs?
2. How does DNS improve usability in a network?
3. What happens if the DHCP server goes offline?

---

## 🏁 Completion Criteria
- Server is configured with DHCP and DNS.
- PCs receive IPs automatically.
- DNS resolution for `library.pcXX` works correctly.
