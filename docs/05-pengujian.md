# 05 — Ringkasan Pengujian

| No | Uji | Dari → ke | Hasil | Bukti |
|---|---|---|---|---|
| 1 | VLAN dan port | SW-Kantor | Fa0/1–5 di VLAN 20, Fa0/6–10 di VLAN 10 | [screenshot](../screenshots/06-vlan-port-switch.png) |
| 2 | Inter-VLAN routing | PC → 192.168.1.67 | Balasan 4/4 | [ping](../screenshots/07-ping-antar-vlan.png) |
| 3 | Nirkabel ke server dan internet | Laptop → .146 dan .130 | Balasan 4/4, 0% loss | [ping](../screenshots/09-ping-laptop-wireless.png) |
| 4 | Rute OSPF | Semua router | Rute `O` ke semua segmen | [Kantor](../screenshots/10-ip-route-r-kantor.png), [Server](../screenshots/11-ip-route-r-server.png), [Internet](../screenshots/12-ip-route-r-internet.png) |
| 5 | Jalur ke server dan internet | PC → .130 dan .146 | Hop: .1 → .150 → .154 → tujuan | [tracert](../screenshots/13-tracert-pc0.png) |
| 6 | Website | Laptop → `jayaabadi.com` | Halaman tampil | [browser](../screenshots/14-web-jayaabadi.png) |
| 7 | Database | Smartphone → `db.jayaabadi.com` | Halaman tampil | [browser](../screenshots/15-web-db-jayaabadi.png) |
