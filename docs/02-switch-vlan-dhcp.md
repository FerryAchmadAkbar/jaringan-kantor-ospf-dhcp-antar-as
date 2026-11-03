# 02 — Switch, VLAN, dan DHCP

## Pemetaan port SW-Kantor (Catalyst 2960)

| Port | Mode | VLAN | Terhubung ke |
|---|---|---|---|
| Fa0/1 – Fa0/5 | access | 20 (NIRKABEL) | Access Point 1–5 |
| Fa0/6 – Fa0/10 | access | 10 (KABEL) | PC |
| Fa0/11 | trunk | 10, 20 | R-Kantor Gi0/0/0 |

SW-Server menghubungkan WEB-SERVER dan DATABASE ke R-Server.

## Konfigurasi VLAN

```text
vlan 10
 name KABEL
vlan 20
 name NIRKABEL

interface range fa0/1-5
 switchport mode access
 switchport access vlan 20
interface range fa0/6-10
 switchport mode access
 switchport access vlan 10
interface fa0/11
 switchport mode trunk
```

## Router-on-a-stick di R-Kantor

```text
interface GigabitEthernet0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.224
interface GigabitEthernet0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.1.65 255.255.255.192
```

## DHCP di R-Kantor

```text
ip dhcp excluded-address 192.168.1.1
ip dhcp excluded-address 192.168.1.65

ip dhcp pool KABEL
 network 192.168.1.0 255.255.255.224
 default-router 192.168.1.1
 dns-server 192.168.1.130

ip dhcp pool NIRKABEL
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.65
 dns-server 192.168.1.130
```

## Pengujian

- Status VLAN per port: [screenshot](../screenshots/06-vlan-port-switch.png)
- Ping antar-VLAN (PC ke perangkat nirkabel `192.168.1.67`): [screenshot](../screenshots/07-ping-antar-vlan.png)

Konfigurasi lengkap: [SW-Kantor](../configs/SW-Kantor.txt), [R-Kantor](../configs/R-Kantor.txt).
