# 04 — Routing OSPF

OSPF dipilih karena konvergen cepat, mendukung VLSM, dan mudah dikembangkan saat jaringan bertambah. Semua router berada di **proses 1, area 0**.

**R-Kantor**
```text
router ospf 1
 network 192.168.1.0 0.0.0.31 area 0
 network 192.168.1.64 0.0.0.63 area 0
 network 192.168.1.148 0.0.0.3 area 0
```

**R-Server**
```text
router ospf 1
 network 192.168.1.148 0.0.0.3 area 0
 network 192.168.1.128 0.0.0.7 area 0
 network 192.168.1.152 0.0.0.3 area 0
```

**R-Internet**
```text
router ospf 1
 network 192.168.1.152 0.0.0.3 area 0
 network 192.168.1.144 0.0.0.3 area 0
```

## Pengujian

| Router | Bukti |
|---|---|
| R-Kantor | [show ip route](../screenshots/10-ip-route-r-kantor.png) |
| R-Server | [show ip route](../screenshots/11-ip-route-r-server.png) |
| R-Internet | [show ip route](../screenshots/12-ip-route-r-internet.png) |

Tracert dari PC kantor ke server dan internet melewati `R-Kantor → R-Server → R-Internet`: [screenshot](../screenshots/13-tracert-pc0.png).

Konfigurasi lengkap: [R-Kantor](../configs/R-Kantor.txt), [R-Server](../configs/R-Server.txt), [R-Internet](../configs/R-Internet.txt).
