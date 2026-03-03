# BSC-1000 — Free BACnet Controller

A full-featured BACnet controller that runs as a virtual appliance on any hypervisor or as a native controller on any Linux single-board computer with auto-detected physical I/O. Multi-protocol support for BACnet/IP, Modbus TCP, Modbus RTU, MQTT, HTTP/REST, and OPC UA — plus a built-in OPC UA server for SCADA integration. Free forever, no license required.

![BACnet Conformance](https://img.shields.io/badge/BACnet_Conformance-228%2F228_Pass-55ba45)
![Protocol Revision](https://img.shields.io/badge/BACnet-Rev_22_(2020)-1d4ed8)
![License](https://img.shields.io/badge/Community-Free_Forever-55ba45)
![Platforms](https://img.shields.io/badge/Platforms-VMware_%7C_Hyper--V_%7C_Proxmox_%7C_Linux_SBC-3b82f6)

---

## What is this?

The BSC-1000 is a free BACnet controller built for building automation engineers who need a flexible, vendor-neutral controller without hardware lock-in or expensive licensing.

It runs as a pre-built virtual appliance — import it into your hypervisor, power on, and you have a working BACnet controller in under 5 minutes. Deploy the same image on a Linux single-board computer and it auto-detects physical I/O — GPIO, I2C ADC/DAC, and Modbus RTU serial — turning it into a full hardware controller.

## Features

**BACnet/IP Controller**
- 228/228 BACnet conformance tests passed (Protocol Revision 22)
- 11 object types: AI, AO, AV, BI, BO, BV, MSV, TrendLog, Schedule, Calendar, NotificationClass
- 27 BACnet services including ReadPropertyMultiple, SubscribeCOV, ReadRange
- Full 16-level priority arrays on commandable outputs
- Segmentation support (tested with 1,040+ objects in single response)
- BBMD with broadcast distribution and foreign device registration
- Tested with 20,000 objects on 1 GB RAM

**Python Control Programming**
- Write control logic in Python — not proprietary function blocks
- 18 built-in HVAC classes: PID, Deadband, LeadLag, Economizer, FreezeProtect, StagingController, OptimalStart, and more
- 23 program templates: AHU, VAV, Boiler Plant, Chiller Plant, Zone Control, Pump Lead-Lag, and more
- BAS program converter — import from PPCL, Plain English, GCL+, Control Basic, and XML exports
- Program linter with 11 rules for HVAC safety and best practices
- Code editor with syntax highlighting, hot-reload, sandboxed execution

**Trend Logging, Scheduling & Alarms**
- Configurable circular buffer trend logging with chart visualization
- Weekly schedules with exception dates and calendar references
- Alarm management with high/low limits, deadband, and notification classes
- Email notifications for alarms and login alerts via SMTP

**Multi-Protocol Integration**
- App Builder bridges 6 protocols to BACnet objects: BACnet/IP, Modbus TCP, Modbus RTU, MQTT, HTTP/REST, OPC UA
- Built-in OPC UA server — all BACnet objects browsable from any SCADA system (read-only in Community, read+write in Professional). Tested with Ignition, WinCC, FactoryTalk
- Modbus RTU serial master with RS-485 support, multi-slave addressing, float32 decoding, and per-point scaling
- OPC UA client driver with subscription-based reads, security policies (Basic256Sha256), and authentication
- Built-in Modbus TCP slave (FC 01/03/05/06/0F/10) with register mapping (Professional)
- Built-in MQTT bridge with bidirectional pub/sub, TLS, QoS 0/1/2 (Professional)
- Auto-discovery tools for all 6 protocols — scan networks, browse OPC UA servers, probe serial buses
- Community Edition includes 1 app with 10 proxy points

**Physical I/O** (Linux Single-Board Computers)
- Hardware abstraction layer auto-detects GPIO, I2C, and serial devices
- Runs on Raspberry Pi, BeagleBone, and other ARM/x86 Linux SBCs
- Same software image as the virtual appliance

**Security & Authentication**
- Multi-factor authentication: TOTP with QR provisioning + FIDO2/WebAuthn hardware keys
- Role-based access control: Admin, Operator, Viewer
- Login alerts via email, session tracking with audit trail
- Failed login rate limiting with automatic lockout
- TLS/HTTPS with auto-generated or custom CA certificates
- API key authentication for scripting and automation

**Graphics & Visualization**
- SVG equipment graphics with live BACnet point binding
- 8 pre-built HVAC templates: AHU, VAV, Boiler, Chiller, Unit Heater, Cooling Tower, Pump, Zone
- Viewer tokens for unauthenticated public displays (lobby screens, customer portals)

**Web UI, API & Management**
- Modern dark-theme dashboard with real-time status
- Object management, program editor, trend charts, alarm viewer
- 35+ REST API endpoints
- SSH management console (port 2222) with interactive CLI, tab completion, context help, and command history
  - Browse objects, write values, manage trends, schedules, programs, alarms, BBMD, users, and network
  - Built-in network diagnostics: ping, traceroute, port check
  - Color-coded output with hierarchical command structure
- MCP (Model Context Protocol) server with 37 integration tools
- Semantic tags for equipment classification and cross-controller discovery

## Download

| Format | Platform | Size | Link |
|--------|----------|------|------|
| **OVA** | VMware ESXi, vSphere, VirtualBox | ~900 MB | [Download OVA](https://github.com/eng-explorer/bsc-1000/releases/latest/download/bacsync-controller.ova) |
| **VHD** | Microsoft Hyper-V | ~870 MB | [Download VHD.gz](https://github.com/eng-explorer/bsc-1000/releases/latest/download/bacsync-controller.vhd.gz) |
| **qcow2** | Proxmox VE, KVM, libvirt | ~950 MB | [Download qcow2](https://github.com/eng-explorer/bsc-1000/releases/latest/download/bacsync-controller.qcow2) |
| **Docker** | Raspberry Pi, Linux SBC, any Linux | `docker pull` | See [Docker instructions](#docker) |

## Quick Start

### VMware / VirtualBox (OVA)

1. Download `bacsync-controller.ova`
2. **File → Import Appliance** (VirtualBox) or **Deploy OVF Template** (VMware)
3. Set network adapter to **Bridged** (required for BACnet/IP broadcast)
4. Power on the VM
5. Wait 30–60 seconds for the controller to start
6. Open `https://<vm-ip>` in your browser (accept self-signed certificate)
7. Create your admin account on the first-run setup page

### Microsoft Hyper-V (VHD)

1. Download `bacsync-controller.vhd`
2. **Hyper-V Manager → New → Virtual Machine**
3. Select Generation 1, allocate 2048 MB memory
4. Connect to an **External** virtual switch
5. Choose **Use an existing virtual hard disk** → browse to the VHD
6. Start the VM and browse to `https://<vm-ip>`

### Proxmox VE (qcow2)

1. Download `bacsync-controller.qcow2`
2. **Transfer the image to your Proxmox server** (the web UI cannot import disk images):
   ```bash
   scp bacsync-controller.qcow2 root@<proxmox-ip>:/tmp/
   ```
3. **Create a new VM** in the Proxmox web UI (**Create VM** button, top right):
   - **OS**: Select "Do not use any media"
   - **System**: Defaults are fine
   - **Disks**: Delete the default disk (select it → Remove)
   - **CPU**: 2 cores
   - **Memory**: 2048 MB
   - **Network**: Select your bridge (e.g. `vmbr0`) and **uncheck Firewall**
   - Note the **VM ID** assigned (e.g. 104)
4. **Import the disk** via SSH on your Proxmox server:
   ```bash
   qm importdisk <vmid> /tmp/bacsync-controller.qcow2 local
   ```
   > **Note:** Replace `local` with your storage name. Run `pvesm status` to list available storage if you get a "storage does not exist" error. Common names: `local`, `local-lvm`, `local-zfs`.
5. **Attach the imported disk**: In the VM → **Hardware** tab, double-click **Unused Disk 0** → set bus to **VirtIO Block** → click **Add**
6. **Set boot order**: VM → **Options** → **Boot Order** → enable the new disk and move it to first position
7. **Start the VM** and wait 30–60 seconds for the controller to start
8. **Find the IP**: Check your router/DHCP server for the new lease, or run `nmap -sn <your-subnet>` to scan for it
9. Open `https://<vm-ip>` in your browser (accept self-signed certificate)
10. Create your admin account on the first-run setup page

### Docker

```bash
docker run -d \
  --name bacsync-controller \
  --network host \
  -v bacsync-data:/app/data \
  -v bacsync-programs:/app/programs/user \
  ghcr.io/eng-explorer/bacsync-controller:latest
```

Access the Web UI at `https://<host-ip>`.

> **Note:** `--network host` is required for BACnet/IP UDP broadcast communication.

### Docker Compose

For production deployments, use the included `docker-compose.yml`:

```bash
cp .env.example .env        # Edit with your settings
docker compose up -d
```

The compose file includes commented-out sections for serial devices (Modbus RTU, MS/TP), GPIO, and SBC hardware — uncomment what you need.

### ARM / Linux SBC (Raspberry Pi, R1125, BeagleBone)

Use the ARM64 image:

```bash
docker run -d \
  --name bacsync-controller \
  --network host \
  --cap-add NET_ADMIN \
  --cap-add SYS_RAWIO \
  -v bacsync-data:/app/data \
  -v /sys:/sys \
  --device /dev/ttyACM0 \
  --device /dev/ttyACM1 \
  ghcr.io/eng-explorer/bacsync-controller:latest-arm64
```

GPIO, I2C, and serial devices are auto-detected. Map the serial ports your hardware uses (e.g. `/dev/ttyACM0` for Modbus RTU, `/dev/ttyACM1` for MS/TP).

### Updating

```bash
docker compose pull
docker compose up -d
```

Your configuration and data persist in the `controller-data` volume across updates.

## Network Configuration

The appliance obtains an IP address via **DHCP** automatically. If no DHCP server responds within 60 seconds, it falls back to **192.168.1.10/24**.

**Ports used:**
| Port | Protocol | Service |
|------|----------|---------|
| 443 | TCP | HTTPS Web UI + REST API |
| 47808 | UDP | BACnet/IP (0xBAC0) |
| 502 | TCP | Modbus TCP (when enabled) |
| 4840 | TCP | OPC UA server (when enabled) |

## Hardware Requirements

| Platform | CPU | RAM | Storage |
|----------|-----|-----|---------|
| Virtual Appliance | 2 vCPU | 2 GB | 20 GB |
| Linux SBC (RPi, BeagleBone, etc.) | 4-core ARM | 2 GB+ | 16 GB+ |
| Docker (any Linux) | 1+ core | 512 MB+ | 5 GB |

## Editions

| Feature | Community (Free) | Professional |
|---------|:---:|:---:|
| BACnet Objects | Unlimited | Unlimited |
| Control Programs | 3 | Unlimited |
| Trend Logs | 3 | Unlimited |
| Schedules | 5 | Unlimited |
| Alarms (on-screen) | &#10003; | &#10003; |
| Alarm Email Notifications | — | &#10003; |
| Login Alerts & Test Email | &#10003; | &#10003; |
| Web UI, REST API & MCP Tools | &#10003; | &#10003; |
| App Builder (6 protocols) | 1 app / 10 points | Unlimited |
| MQTT Bridge (Publish All to Broker) | — | &#10003; |
| Modbus TCP Server (Expose Registers) | — | &#10003; |
| Custom Graphics | 1 page | Unlimited |
| Viewer Tokens (Shareable Displays) | — | &#10003; |
| SSH Console & Network Diagnostics | Read-only | Full access |
| BACnet/IP + BBMD + HTTPS | &#10003; | &#10003; |
| OPC UA Server (SCADA Integration) | Read-only | Read + Write |
| BACnet/SC & MS/TP | — | &#10003; |
| Multi-User & RBAC | 1 admin | Unlimited |
| Priority Support | — | &#10003; |

The Community Edition is **free forever** — no trial period, no time limit, no license file required. Unlimited BACnet objects out of the box.

## BACnet Conformance

The BSC-1000 has been tested against a comprehensive conformance test suite covering all required BACnet services and object types:

- **228/228 tests passed** (0 failures, 0 skipped) across 4 test phases
- Protocol Revision 22 (ASHRAE 135-2020)
- 11 object types, 27 services
- Segmentation tested with 1,040+ objects in single response
- Who-Is flood test: 99&ndash;100% response rate under rapid-fire requests
- Protocol fuzz testing: 15 malformed packet scenarios handled gracefully

**Stress Testing:**
- 20,000 objects on 1 GB RAM (99.99% success rate)
- 100 concurrent control programs (mixed complexity)
- 50 concurrent MCP sessions, 100% success, &lt;35ms response
- Combined load: 1,500 objects + 30 programs + 6 users &mdash; 0 errors, P95 23ms

**Stability Testing:**
- 11-hour continuous test, 6 controllers, 0 crashes, 0 errors
- 465 objects and 36 programs per controller running continuously
- MCP response stable at 3–5ms throughout entire run
- Resource usage: ~1% CPU, ~49 MB RAM per controller
- 94% data persistence after unexpected power loss (SIGKILL)

**Security Audit (Penetration Test):**
- 4-round penetration test covering HTTPS, MCP, TLS, cookies, authentication, headers, and BACnet/IP
- 14 findings identified — all medium-severity findings fixed, 3 low-risk accepted with rationale
- Timing-safe authentication prevents username enumeration (bcrypt with constant-time comparison)
- Security headers on all responses: CSP, HSTS, X-Content-Type-Options, X-Frame-Options, Referrer-Policy
- Secret masking: settings API never returns passwords or tokens in plaintext
- TLS 1.2+ enforced (TLS 1.0/1.1 rejected at handshake)
- MCP sensitive tools require authentication tokens
- Path traversal, session fixation, content-type confusion, large payload — all blocked
- Overall risk rating: **LOW** after remediation

**Program Sandbox Security:**
- Two-layer defense: AST validation before save + restricted runtime globals
- All classic Python escape vectors blocked (import, exec, eval, subprocess, os, sys, builtins)
- Infinite loop protection with AST analysis + runtime timeout, auto-disables program
- Session flooding resistance: rapid login attacks blocked, 0 unauthorized sessions

**OPC UA Server Testing (60+ tests):**
- Full node browsing, SCADA read/write interoperability, subscription monitoring
- 500-node bulk sync with all values verified, subscribe in 0.38s
- Dynamic object tracking: BACnet create/delete reflected in OPC UA within 3s
- Edge case validation: NaN/Inf rejection, integer clamping, out-of-range protection
- 20 concurrent SCADA client connections with zero data loss

## Verifying Downloads

### Appliance Images

Each release includes a `SHA256SUMS.txt` file. After downloading, verify the integrity:

```bash
sha256sum -c SHA256SUMS.txt
```

### Docker Images

Docker images are signed with [cosign](https://github.com/sigstore/cosign). To verify:

```bash
cosign verify --key https://raw.githubusercontent.com/eng-explorer/bsc-1000/main/cosign.pub \
  ghcr.io/eng-explorer/bacsync-controller:latest
```

## Documentation

- [Deployment Guide](#) — Installation, configuration, networking
- [Operator Guide](#) — Web UI, SSH console, configuration reference
- [HVAC Programming Guide](#) — Control program API, 18 HVAC classes, examples
- [REST API Reference](#) — 35+ endpoints with request/response examples

## Support

- **Community:** Open an [issue](../../issues) on this repo
- **Professional:** [info@humberhorizons.ca](mailto:info@humberhorizons.ca)

## About

The BSC-1000 is built by [Humber Horizons Limited](https://humberhorizons.ca), a technology company specializing in automation, controls, networking, and cyber security.

BACsync&trade; is a trademark of Humber Horizons Limited. Patent pending.
