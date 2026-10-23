# ISA100Forge Pro (v1.0.0)

**ISA100.11a (IEC 62734 / IEEE 802.15.4) Wireless Mesh Studio, TDMA Superframe & 16-Channel Hopping Scheduler, RF Path Loss & Battery Sizer, & 10-Point Mesh Safety Auditor**

---

## ⚡ Overview

**ISA100Forge Pro** is an industrial wireless mesh protocol engineering suite specifically targeted at **ISA100.11a (IEC 62734 / IEEE 802.15.4)** wireless sensor networks (refineries, petrochemical complexes, offshore platforms, tank farms). It delivers zero-dependency, browser-based, and command-line automation for:

1. **IEEE 802.15.4 2.4 GHz DSSS Physical Layer & MAC Engine**: Models 250 kbps O-QPSK signaling, 4-byte preambles, `0xA7` Start Delimiter, Frame Control Fields (`0x8861`), and 16-bit CRC Frame Check Sequences (\$x^{16} \+ x^{12} \+ x^5 \+ 1\$).  
2. **Cryptographic Security Layer**: Implements AES-128 CCM\* authenticated encryption with 32-bit Message Integrity Codes (MIC-32) to enforce cyber protection across untrusted radio environments.  
3. **TDMA Superframe & 16-Channel Hopping Scheduler**: Sequences 10.0 ms timeslot templates (Radio lock, Clear Channel Assessment, 250 kbps transmission, turnaround, immediate ACK, and deep sleep) across 16 DSSS channels (2405 MHz to 2480 MHz).  
4. **RF Link Budget & Battery Life Sizer**: Models heavy industrial log-distance path loss (\$n \= 3.4\$), Fresnel zone clearances, and 19.0 Ah Lithium Thionyl Chloride (\$\\text{Li-SOCl}\_2\$) cell discharge profiles to verify NAMUR NE 124 \$\\ge 5\$-year battery maintenance targets.  
5. **10-Point Mesh Safety Auditor**: Enforces short address uniqueness (`0x0002..0xFFFD`), Subnet PAN ID alignment, RF fade margin thresholds (\$\\ge 15\\text{ dB}\$), mesh path diversity (\$\\ge 2\$ routing parents), and Redundant System Manager readiness.  
6. **Multi-Target Exporter**: Outputs Yokogawa YFGW410/YFGW510 Gateway provisioning XML, Honeywell OneWireless network CSVs, and Python IEEE 802.15.4 packet simulation scripts.

---

## 📁 Repository Structure

product\_200/

├── source-code/

│   ├── isa100-engine.js             \# IEEE 802.15.4 framing, MAC headers, AES-128 MIC-32

│   ├── isa100-scheduler.js          \# TDMA superframe & 16-channel hopping allocator

│   ├── isa100-rf-sizer.js           \# Industrial RF path loss & Li-SOCl2 battery sizer

│   ├── isa100-auditor.js            \# 10-Point ISA100.11a mesh safety auditor

│   ├── isa100-forge.css             \# Industrial wireless teal & cyan UI theme

│   ├── app.js                       \# Interactive web controller

│   └── index.html                   \# Responsive 5-tab web studio

├── build/

│   ├── isa100-cli.py                \# Standalone Python CLI executable (chmod \+x)

│   └── isa100forge-pro-v1.0.0.zip   \# Production release archive

├── documentation/

│   ├── ARCHITECTURE.md              \# Engineering specification & RF/battery mathematics

│   ├── USER\_GUIDE.md                \# Operator manual & CLI instructions

│   ├── MONETIZATION\_AND\_MARKETING\_PLAYBOOK.md \# Commercial strategy & pricing tiers

│   └── PROGRESS\_REPORT.md           \# Cycle \#200 milestone report

├── screenshots/

│   └── isa100-studio-preview.svg    \# High-resolution SVG preview diagram

└── README.md                        \# Master product documentation

---

## 🚀 Quick Start

### 1\. Launch Interactive Web Studio

Open `product_200/source-code/index.html` in any web browser. Zero server, node packages, or build steps required.

### 2\. Standalone Python CLI Usage

\# Make CLI executable

chmod \+x product\_200/build/isa100-cli.py

\# Build an ISA100.11a Data Packet for Node 0x0014 publishing PV \= 75.0

./product\_200/build/isa100-cli.py packet-build \--pan 0x100A \--src 0x0014 \--dest 0x0001 \--pv 75.0

\# Dissect an over-the-air packet hex stream

./product\_200/build/isa100-cli.py packet-dissect "00 00 00 00 A7 16 61 88 2A 0A 10 01 00 14 00 05 00 42 96 00 00 80 F7 A6 3C C2 CB 6C"

\# Calculate RF Link Budget & Battery Longevity

./product\_200/build/isa100-cli.py rf-size \--dist 50 \--env HEAVY\_INDUSTRIAL \--interval 10

\# Run 10-Point Mesh Safety Auditor

./product\_200/build/isa100-cli.py audit \--devices '\[{"addr":1,"name":"Gateway","router":true,"sm":true},{"addr":20,"name":"PT-1","router":false,"parents":2}\]' \--dist 40

---

## 🧪 Verification & Automated Testing

The engine has been tested against 10 comprehensive unit tests:

python3 test\_isa100forge.py

\# Output: Ran 10 tests in 0.657s \- OK

---

## 💼 Commercial & Pricing Model

- **Community Edition**: Free / Open Source (Packet Builder, Dissector, Basic RF Sizer, Web UI).  
- **Professional License**: \$299 one-time per engineer seat (Full TDMA Superframe Allocator, 10-Point Safety Auditor, Python CLI, Yokogawa & Honeywell Exporters).  
- **Plant Site License**: \$2,490 / facility / year (Site-wide multi-seat license, automated CI/CD mesh validation hooks, priority support).