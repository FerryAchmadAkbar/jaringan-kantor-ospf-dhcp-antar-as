# 01 — Perancangan Pengalamatan IP

Blok yang dipakai: `192.168.1.0/24`, dipecah dengan **VLSM** dari segmen terbesar ke terkecil.

## Tabel subnet

| Segmen | Network ID | Prefix | Mask | Range host | Gateway | Broadcast |
|---|---|---|---|---|---|---|
| LAN Kabel (VLAN 10) | 192.168.1.0 | /27 | 255.255.255.224 | .1 – .30 | .1 | .31 |
| LAN Nirkabel (VLAN 20) | 192.168.1.64 | /26 | 255.255.255.192 | .65 – .126 | .65 | .127 |
| LAN Server | 192.168.1.128 | /29 | 255.255.255.248 | .129 – .134 | .129 | .135 |
| LAN Internet | 192.168.1.144 | /30 | 255.255.255.252 | .145 – .146 | .145 | .147 |
| Link Kantor–Server | 192.168.1.148 | /30 | 255.255.255.252 | .149 – .150 | — | .151 |
| Link Server–Internet | 192.168.1.152 | /30 | 255.255.255.252 | .153 – .154 | — | .155 |

## Pengalamatan interface router

| Router | Interface | IP | Mask | Terhubung ke |
|---|---|---|---|---|
| R-Kantor | Gi0/0/0.10 | 192.168.1.1 | /27 | VLAN 10 (kabel) |
| R-Kantor | Gi0/0/0.20 | 192.168.1.65 | /26 | VLAN 20 (nirkabel) |
| R-Kantor | Se0/1/0 | 192.168.1.149 | /30 | R-Server |
| R-Server | Gi0/0/0 | 192.168.1.129 | /29 | LAN Server |
| R-Server | Se0/2/0 | 192.168.1.150 | /30 | R-Kantor |
| R-Server | Se0/2/1 | 192.168.1.153 | /30 | R-Internet |
| R-Internet | Gi0/0/0 | 192.168.1.145 | /30 | Server Internet |
| R-Internet | Se0/1/0 | 192.168.1.154 | /30 | R-Server |

## Pengalamatan host

| Perangkat | IP | Gateway | Metode |
|---|---|---|---|
| WEB-SERVER | 192.168.1.130/29 | .129 | Statis (`jayaabadi.com`) |
| DATABASE | 192.168.1.131/29 | .129 | Statis (`db.jayaabadi.com`) |
| Server Internet | 192.168.1.146/30 | .145 | Statis |
| PC kabel | 192.168.1.2 – .30 | .1 | DHCP (pool `KABEL`) |
| Perangkat nirkabel | 192.168.1.66 – .126 | .65 | DHCP (pool `NIRKABEL`) |

Bukti: [PC0](../screenshots/01-ip-pc0.png), [Laptop0](../screenshots/02-ip-laptop0-dhcp.png), [WEB-SERVER](../screenshots/03-ip-web-server.png), [Server Internet](../screenshots/04-ip-server-internet.png), [DATABASE](../screenshots/05-ip-database.png).
