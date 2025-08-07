<img src="https://cisco-packet-tracer.fileion.com/storage/software/logos/2025/06/cisco-packet-tracer.png" width=15% height=15%>

# 🛠️ DHCP Server and VLAN Routing using Cisco Packet Tracer

---

This lab demonstrates how to configure a **DHCP server** with **Inter-VLAN Routing** using Cisco Packet Tracer. Devices in the network automatically obtain IP addresses from a central DHCP server, and routing between VLANs is managed via router sub-interfaces.

## Software Requirements:
- CISCO Packet Tracer

## Lab Setup

<img src="https://github.com/Hashdan-M/DHCP-Server-and-VLAN-routing-using-Packet-Tracer/blob/main/Cisco%20PT/c0.PNG"/></a>

---

## 🎯 Objective

Understand how DHCP and Inter-VLAN routing function together in a switched network. Learn to:
- Configure VLANs on a switch.
- Assign VLANs to access ports.
- Set up a router for inter-VLAN routing.
- Enable DHCP server with multiple scopes.
- Use IP helper addresses for DHCP relay across VLANs.

---

## 💻 Software Requirements

- **Cisco Packet Tracer**

---

## 🧑‍💻 Step-by-Step Instructions

### 🔹 Step 1: Add Devices to the Workspace

1. Open Cisco Packet Tracer.
2. From **End Devices**, add:
   - 3 PCs (one per VLAN)
   - 1 Server (for DHCP)
3. From **Network Devices**, add:
   - 1 Router (e.g., 2911 or 1941)
   - 1 Switch (e.g., 2960)

---

### 🔹 Step 2: Physically Connect Devices

Use **Copper Straight-Through** cables to connect:

- Router (GigabitEthernet0/0) → Switch (FastEthernet0/1)
- Each PC → Switch
- Server → Switch

---

### 🔹 Step 3: Configure VLANs on the Switch

Access CLI on the Switch:

```bash
Switch>enable
Switch#configure terminal
Switch(config)#vlan 10
Switch(config-vlan)#name Sales
Switch(config)#vlan 20
Switch(config-vlan)#name IT
Switch(config)#vlan 30
Switch(config-vlan)#name HR
```

Assign VLANs to access ports:

```bash
Switch(config)#interface range FastEthernet 0/2-5
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config)#interface range FastEthernet 0/6-10
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20
Switch(config)#interface range FastEthernet 0/11-15
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 30
```

Configure trunk port to router:

```bash
Switch(config)#interface FastEthernet 0/1
Switch(config-if)#switchport mode trunk
Switch(config-if)#switchport trunk allowed vlan all
```

---

### 🔹 Step 4: Configure Router for Inter-VLAN Routing

Access Router CLI:

```bash
Router>enable
Router#configure terminal
```

Create sub-interfaces:

```bash
Router(config)#interface GigabitEthernet0/0.10
Router(config-if)#encapsulation dot1Q 10
Router(config-if)#ip address 192.168.10.1 255.255.255.0
Router(config)#interface GigabitEthernet0/0.20
Router(config-if)#encapsulation dot1Q 20
Router(config-if)#ip address 192.168.20.1 255.255.255.0
Router(config)#interface GigabitEthernet0/0.30
Router(config-if)#encapsulation dot1Q 30
Router(config-if)#ip address 192.168.30.1 255.255.255.0
```

Enable physical interface and save config:

```bash
Router(config)#interface GigabitEthernet0/0
Router(config-if)#no shutdown
Router(config-if)#exit
Router#write
```

---

### 🔹 Step 5: Configure the DHCP Server

1. Click on Server → Config tab → Select **FastEthernet0**
2. Assign:
   - IP: `192.168.10.2`
   - Subnet Mask: `255.255.255.0`
   - Default Gateway: `192.168.10.1`

3. Go to **Services > DHCP** → Enable DHCP
4. Create DHCP Pools:

**VLAN 10 (Sales)**:
```
Pool Name: Sales
Default Gateway: 192.168.10.1
Start IP: 192.168.10.10
Subnet Mask: 255.255.255.0
Max Users: 20
```

**VLAN 20 (IT)**:
```
Pool Name: IT
Default Gateway: 192.168.20.1
Start IP: 192.168.20.10
Subnet Mask: 255.255.255.0
Max Users: 20
```

**VLAN 30 (HR)**:
```
Pool Name: HR
Default Gateway: 192.168.30.1
Start IP: 192.168.30.10
Subnet Mask: 255.255.255.0
Max Users: 20
```

Click **Add** after creating each pool.

---

### 🔹 Step 6: Configure DHCP Relay on Router

Go back to the Router CLI:

```bash
Router#configure terminal
```

Set up IP helper addresses:

```bash
Router(config)#interface GigabitEthernet0/0.20
Router(config-subif)#ip helper-address 192.168.10.2
Router(config)#interface GigabitEthernet0/0.30
Router(config-subif)#ip helper-address 192.168.10.2
```

---

### 🔹 Step 7: Configure PCs to Use DHCP

1. Click on each PC → Desktop tab → **IP Configuration**
2. Select **DHCP**
3. Confirm that each PC receives an IP from its VLAN’s subnet

---

### 🔹 Step 8: Verify the Configuration

- On each PC, open the **Command Prompt** and type:

```bash
ipconfig
```

- Ensure the IP address matches the correct subnet.

- Test connectivity between VLANs using:

```bash
ping <IP address of PC in different VLAN>
```

---

## ✅ Outcome

Each PC receives a dynamic IP from the DHCP server based on its VLAN. Inter-VLAN routing allows communication between PCs on different subnets through the router’s sub-interfaces.

---

## 🧰 Tools Used

- Cisco Packet Tracer
- Cisco 2911/1941 Router, Cisco 2960 Switch, PCs and Server (from End Devices)

---

## 🧠 Key Concepts Practiced

- VLAN creation and port assignment
- Router-on-a-stick configuration
- DHCP server setup and relay using IP helper
- Inter-VLAN routing and subnetting
