<div align="center">

# 🚀 CNDC Enterprise Network Architecture

## Multi-Campus Network Design & Implementation

### SZABIST - Computer Networks & Data Communications Project

---

![Network Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Packet Tracer](https://img.shields.io/badge/Packet%20Tracer-8.x-blue)
![OSPF](https://img.shields.io/badge/Routing-OSPF-purple)
![VLANs](https://img.shields.io/badge/VLANs-30%2B-orange)
![Campuses](https://img.shields.io/badge/Campuses-6-red)

---

</div>

## 📊 Project Overview

This project presents a **comprehensive enterprise-grade network design** connecting **6 distributed campuses** to a centralized hub. The infrastructure supports **30+ VLANs**, **inter-VLAN routing**, **dynamic IP allocation**, and **secure internet access** through a single gateway.

### 🎯 Key Achievements

| Metric | Value |
|--------|-------|
| Total Campuses Connected | 6 |
| VLANs Configured | 30+ |
| Subnets Designed | 25+ |
| End Devices Supported | 200+ |
| Routing Protocol | OSPF (Area 0) |
| Internet Gateway | NAT/PAT at EDGE-99 |

---

## 🏗️ Network Architecture

### Hub-and-Spoke Topology

```
                    ┌─────────────┐
                    │    ISP      │
                    │  11.11.11.2 │
                    └──────┬──────┘
                           │ Serial
                    ┌──────▼──────┐
                    │  EDGE-99    │
                    │  (Main Hub) │
                    └──────┬──────┘
           ┌───────┬───────┼───────┬───────┐
           │       │       │       │       │
      ┌────▼───┐ ┌─▼────┐ ┌─▼────┐ ┌▼─────┐ ┌▼────────┐
      │Campus  │ │Campus│ │Campus│ │Campus│ │ Media   │
      │ 100    │ │ 154  │ │ 153  │ │ 79   │ │ Villa   │
      │(13VLANs│ │(5VLAN│ │(3VLAN│ │(6VLAN│ │(3 VLANs)│
      └────────┘ └──────┘ └──────┘ └──────┘ └─────────┘
```

### Campus Distribution

| Campus | Router | VLAN Count | Department Focus | Link Type |
|:------:|:------:|:----------:|:-----------------|:---------:|
| 🏢 **Campus 99** | EDGE-99 | 7 | Main Hub + Data Center | - |
| 💻 **Campus 100** | R-100 | 13 | Computer Labs (CS, AI, Gaming) | GigabitEthernet |
| 📚 **Campus 154** | R-154 | 5 | Academic + Mechatronics | GigabitEthernet |
| 🎓 **Campus 153** | R-153 | 3 | Classrooms + Admissions | Serial |
| 📋 **Campus 79** | R-79 | 6 | HR, Finance, Library, EDC | Serial |
| 🎬 **Media Villa** | R-MEDIA | 3 | Classrooms + Faculty | Serial |

---

## 🌐 IP Addressing Scheme

### Public IP Block

| Network | Usage | Gateway |
|---------|-------|---------|
| `11.11.11.0/30` | ISP WAN Link | 11.11.11.1 |

### WAN Interconnect Links (/30 Subnets)

| Connection | Subnet | EDGE-99 IP | Remote IP |
|------------|--------|------------|-----------|
| EDGE-99 ↔ R-100 | `23.12.145.108/30` | .109 | .110 |
| EDGE-99 ↔ R-154 | `23.12.145.112/30` | .113 | .114 |
| EDGE-99 ↔ R-153 | `23.12.145.116/30` | .117 | .118 |
| EDGE-99 ↔ R-79 | `23.12.145.120/30` | .121 | .122 |
| EDGE-99 ↔ R-MEDIA | `23.12.145.124/30` | .125 | .126 |

### Private IP Allocation

| IP Block | Campus | Purpose |
|----------|--------|---------|
| `23.12.145.0/24` | C99 + C154 | Main Campus VLANs + WAN |
| `23.12.151.0/24` | C100 | CS, AI, Lab3, Lab4 |
| `192.168.1.0/24` | C100 | Lab5, Lab6, Smart Lab |
| `192.168.2.0/24` | C100 | Gaming, Faculty, Admin, IT |
| `192.168.3.0/24` | C153 | Classrooms, Admissions |
| `192.168.4.0/24` | C79 | Library, HR, Finance, EDC |
| `192.168.5.0/24` | Media Villa | Classrooms, Faculty |

---

## 🔧 Technical Implementation

### Routing Protocol - OSPF

```
All routers configured in OSPF Area 0
├── EDGE-99: DR/BDR (Default Information Originate)
├── R-100: Internal Router
├── R-154: Internal Router
├── R-153: Internal Router
├── R-79: Internal Router
└── R-MEDIA: Internal Router
```

### VLAN Segmentation Strategy

| VLAN Range | Department Type | DHCP | Static |
|------------|----------------|------|--------|
| 140-200 | Campus 99 Services | ✓ | Servers |
| 10-130 | Campus 100 Labs | ✓ | FTP/Printers |
| 210-250 | Campus 154 Academic | ✓ | Printers |
| 260-280 | Campus 153 Academic | ✓ | Printers |
| 310-360 | Campus 79 Admin | ✓ | Printers |
| 380-400 | Media Villa | ✓ | Printers |

### Security Features

```
┌─────────────────────────────────────────────────────┐
│  🔐 ACL IMPLEMENTATION                              │
│  ├── Faculty-only printer access (Campus 99/100/154/Media)
│  ├── ZABDESK server restricted to lab access        │
│  └── Default deny policies for sensitive resources  │
├─────────────────────────────────────────────────────┤
│  🛡️ PORT SECURITY                                   │
│  ├── Max 1 MAC address per access port              │
│  └── Violation: Shutdown                            │
├─────────────────────────────────────────────────────┤
│  🌐 NAT/PAT                                          │
│  ├── Overload on Serial0/1/0                        │
│  └── All internal networks translated to 11.11.11.1 │
└─────────────────────────────────────────────────────┘
```

---

## 📁 Repository Files

| File | Type | Description |
|------|------|-------------|
| `CNDC PROJECT FINAL CAMPUSES.pkt` | 🖧 Packet Tracer | Complete simulation file |
| `CNDC_Project_Report.pdf` | 📄 PDF | 40+ pages detailed documentation |
| `SZABIST_Network_Project.xlsx` | 📊 Excel | Complete IP & VLAN tables |

---

## ✅ Testing Validation Matrix

| Test Case | Source | Destination | Result |
|-----------|--------|-------------|:------:|
| Same VLAN Ping | C100 CS Lab PC | C100 FTP Server | ✅ PASS |
| Inter-VLAN Ping | C100 CS Lab | C100 AI Lab | ✅ PASS |
| Cross-Campus Ping | C100 PC | C154 Faculty | ✅ PASS |
| Cross-Campus Ping | C100 PC | Media Villa | ✅ PASS |
| Internet Connectivity | Any Campus PC | 8.8.8.8 | ✅ PASS |
| ACL Verification | Non-Faculty | Faculty Printer | ✅ BLOCK |
| DHCP Assignment | All VLANs | Dynamic PCs | ✅ PASS |

---

## 📈 Network Statistics

```
Total VLANs:        ████████████████████ 30+
Interfaces:         ████████████████████ 50+
Static Devices:     ████████████████░░░░ 25+
DHCP Pools:         ████████████████████ 30+
OSPF Routes:        ████████████████████ 25+
ACL Rules:          ████████████████░░░░ 23
```

---

## 📅 Project Timeline

| Phase | Completion |
|-------|:----------:|
| Network Design | ✅ |
| VLAN Configuration | ✅ |
| Inter-VLAN Routing | ✅ |
| DHCP Setup | ✅ |
| OSPF Implementation | ✅ |
| ACL & Security | ✅ |
| Testing & Validation | ✅ |
| Documentation | ✅ |

---

## 📚 References

- Cisco Systems — *Packet Tracer 8.x Documentation*
- Tanenbaum, A. S. & Wetherall, D. — *Computer Networks, 5th Edition*
- RFC 1918 — *Address Allocation for Private Internets*
- Cisco Press — *CCNA Routing and Switching 200-125 Official Cert Guide*

---

<div align="center">

**🚀 *A Fully Functional Multi-Campus Enterprise Network with 30+ VLANs, OSPF Routing, and Centralized Internet Access***

</div>
