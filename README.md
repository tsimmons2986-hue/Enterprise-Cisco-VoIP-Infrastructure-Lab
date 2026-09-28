# Enterprise Cisco VoIP & Telephony Infrastructure Deployment

## Executive Summary
This project demonstrates the design, configuration, and verification of an enterprise-grade Voice over IP (VoIP) network deployed on Cisco routing and switching hardware within Cisco Packet Tracer. The infrastructure integrates **Cisco Unified Communications Manager Express (CME)** telephony services, dual-VLAN access architecture (Voice + Data segmentation), DHCP Option 150 provisioning, TFTP firmware delivery, and centralized Syslog telemetry.

---

## Architecture & Topology Overview

The network topology implements an access-layer distribution model connecting desktop PCs daisy-chained through **Cisco 7960 IP Phones** to a centralized Cisco Catalyst switch, routed via a Cisco 2811 Integrated Services Router (ISR).

![VoIP Network Topology](NETWORK.jpg)

### Core Infrastructure Components
* **Voice Gateway / Call Processing Router:** Cisco 2811 ISR running Cisco IOS Telephony Service (CME).
* **Access Switch:** Cisco Catalyst 2960 / 3560 with 802.1Q trunking and auxiliary Voice VLAN tagging.
* **Telephony Endpoints:** Cisco 7960 IP Phones with inline PC bridge ports.
* **Network Services:** Centralized TFTP Server (firmware/XML configs) and Syslog Server (telephony event logging).

---

## Technical Implementation Details

### 1. VLAN Segmentation & Switchport Voice Configuration
To prevent voice traffic degradation from standard workstation data bursts, access ports were configured with separate Data and Voice VLANs (e.g., VLAN 40 for VoIP) using Cisco auxiliary VLAN tagging. 

![Switch VLAN Configuration](VLAN_DATA_VOIP.jpg)

```text
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 40
 spanning-tree portfast
