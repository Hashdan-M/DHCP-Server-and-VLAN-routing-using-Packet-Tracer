# DHCP Server and VLAN Routing using Cisco Packet Tracer

---

## Objective
This setup will allow you to understand how devices in a network can automatically
obtain IP addresses and other network configuration details from a DHCP server.

## Software Requirements:
- CISCO Packet Tracer

## Lab Setup

<img src="https://github.com/Hashdan-M/DHCP-Server-and-VLAN-routing-using-Packet-Tracer/blob/main/Cisco%20PT/c0.PNG"/></a>

## Step-by-Step Instructions
Step 1: Add Devices to the Workspace
1. Open Cisco Packet Tracer.
2. From the End Devices section, drag and drop the following devices onto the workspace:
- Add PCs for each VLAN/subnet (e.g., three PCs for this homelab).
- Add a Server to configure as the DHCP server.
3. From the Network Devices section, drag and drop:
- Drag a Router (e.g., 2911 or 1941) into the workspace.
- Add a Switch (e.g., 2960).

Step 2: Physically Connect Devices
1. Click on the cable icon and select a copper straight-through cable.
2. Connect the following devices using the copper straight-through cable.
- Router (GigabitEthernet 0/0) to the Switch (FastEthernet 0/1).
- Each PC to the Switch.
- The Server to the Switch.

Step 3: Configure the VLANs on the Switch
Access the Switch:
- Click on the switch to open the configuration window.
- Select the CLI (Command Line Interface) tab.
Create VLANs:
- Enter global configuration mode
Switch>enable
Switch#configure terminal
Switch(config)#
