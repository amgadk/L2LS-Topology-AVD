# DC1

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)
- [Connected Endpoints](#connected-endpoints)
  - [Connected Endpoint Keys](#connected-endpoint-keys)
  - [Firewalls](#firewalls)
  - [Servers](#servers)
  - [Port Profiles](#port-profiles)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| DC1 | l2leaf | LEAF1 | 192.168.0.20/24 | cEOSLab | Provisioned | - |
| DC1 | l2leaf | LEAF2 | 192.168.0.21/24 | cEOSLab | Provisioned | - |
| DC1 | l2leaf | LEAF3 | 192.168.0.22/24 | cEOSLab | Provisioned | - |
| DC1 | l2leaf | LEAF4 | 192.168.0.23/24 | cEOSLab | Provisioned | - |
| DC1 | l3spine | SPINE1 | 192.168.0.111/24 | cEOSLab | Provisioned | - |
| DC1 | l3spine | SPINE2 | 192.168.0.112/24 | cEOSLab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | --------- | -------------- |
| l2leaf | LEAF1 | Ethernet1 | l3spine | SPINE1 | Ethernet1 |
| l2leaf | LEAF1 | Ethernet2 | l3spine | SPINE2 | Ethernet1 |
| l2leaf | LEAF1 | Ethernet47 | mlag_peer | LEAF2 | Ethernet47 |
| l2leaf | LEAF1 | Ethernet48 | mlag_peer | LEAF2 | Ethernet48 |
| l2leaf | LEAF2 | Ethernet1 | l3spine | SPINE1 | Ethernet2 |
| l2leaf | LEAF2 | Ethernet2 | l3spine | SPINE2 | Ethernet2 |
| l2leaf | LEAF3 | Ethernet1 | l3spine | SPINE1 | Ethernet3 |
| l2leaf | LEAF3 | Ethernet2 | l3spine | SPINE2 | Ethernet3 |
| l2leaf | LEAF3 | Ethernet47 | mlag_peer | LEAF4 | Ethernet47 |
| l2leaf | LEAF3 | Ethernet48 | mlag_peer | LEAF4 | Ethernet48 |
| l2leaf | LEAF4 | Ethernet1 | l3spine | SPINE1 | Ethernet4 |
| l2leaf | LEAF4 | Ethernet2 | l3spine | SPINE2 | Ethernet4 |
| l3spine | SPINE1 | Ethernet47 | mlag_peer | SPINE2 | Ethernet47 |
| l3spine | SPINE1 | Ethernet48 | mlag_peer | SPINE2 | Ethernet48 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.255.0.0/24 | 256 | 2 | 0.79 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC1 | SPINE1 | 10.255.0.1/32 |
| DC1 | SPINE2 | 10.255.0.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |

## Connected Endpoints

### Connected Endpoint Keys

| Key | Default Type | Description |
| --- | ------------ | ----------- |
| firewalls | firewall | - |
| servers | server | - |

### Firewalls

| Name | Type | Port | Fabric Device | Fabric Port | Description | Shutdown | Mode | Access VLAN | Trunk Allowed VLANs | Profile |
| ---- | ---- | ---- | ------------- | ----------- | ----------- | -------- | ---- | ----------- | ------------------- | ------- |
| FIREWALL | firewall | Eth1 | SPINE1 | Port-Channel5(Ethernet5) | FIREWALL_FIREWALL | False | trunk | - | 10,20,30 | PP-FIREWALL |
| FIREWALL | firewall | Eth2 | SPINE2 | Port-Channel5(Ethernet5) | FIREWALL_FIREWALL | False | trunk | - | 10,20,30 | PP-FIREWALL |

### Servers

| Name | Type | Port | Fabric Device | Fabric Port | Description | Shutdown | Mode | Access VLAN | Trunk Allowed VLANs | Profile |
| ---- | ---- | ---- | ------------- | ----------- | ----------- | -------- | ---- | ----------- | ------------------- | ------- |
| Host1 | server | Eth1 | LEAF1 | Ethernet3 | SERVER_Host1_Eth1 | False | access | 10 | - | PP-BLUE |
| Host2 | server | Eth1 | LEAF2 | Ethernet3 | SERVER_Host2_Eth1 | False | access | 20 | - | PP-GREEN |
| Host3 | server | Eth1 | LEAF3 | Ethernet3 | SERVER_Host3_Eth1 | False | access | 10 | - | PP-BLUE |
| Host4 | server | Eth1 | LEAF4 | Ethernet3 | SERVER_Host4_Eth1 | False | access | 20 | - | PP-GREEN |
| Host11 | server | Eth1 | LEAF1 | Ethernet4 | SERVER_Host11_Eth1 | False | access | 30 | - | PP-ORANGE |
| Host22 | server | Eth1 | LEAF2 | Ethernet4 | SERVER_Host22_Eth1 | False | access | 40 | - | PP-YELLOW |

### Port Profiles

| Profile Name | Parent Profile |
| ------------ | -------------- |
| PP-BLUE | PP-DEFAULTS |
| PP-DEFAULTS | - |
| PP-FIREWALL | - |
| PP-GREEN | PP-DEFAULTS |
| PP-ORANGE | PP-DEFAULTS |
| PP-YELLOW | PP-DEFAULTS |
