# Changelog

All notable changes to the BSC-1000 BACnet Controller are documented in this file.

This format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and BSC-1000 follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.0.0] — 2026-06-XX (Unreleased)

**Major release** spanning ~3 months of development since v1.0.0 (March 2026). The scope and breadth of changes — including a vendor ID change visible to BACnet networks and several breaking-shape persistence updates — warrant a major version bump.

> **In progress.** Additional improvements to HHL remote support are landing before the v2.0.0 release. This CHANGELOG will be updated when those commit.

### Added

- **BACnet/SC** (Secure Connect) end-to-end support with persistent device identity across restarts and full hub-and-Direct-Connect operation. (Professional)
- **CAN bus protocol support** with a J1939 dashboard, protocol selector, and live tile results. (Engineering preview; hardware required.)
- **App Builder — EtherNet/IP (CIP) driver**: tag access for Logix-family PLCs, file-element access for legacy SLC/PLC controllers, and generic CIP explicit messaging for instruments and drives. Auto-reconnect with connection management.
- **App Builder — SNMP driver**: read SNMP data from UPSes, switches, and IT-room monitors. Supports SNMPv1, v2c, and v3 with authentication and privacy. Optional alarm-trap listener.
- **BSC-IO firmware OTA (over-the-air) updates**: Web UI workflow for updating BSC-IO board firmware. Boards cannot be downgraded (firmware version is checked before applying). Reconnect is coordinated around the board reboot window.
- **Graphics V2 — full canvas engine**: object-based canvas editor, animation primitives, push-based live updates, equipment widget palette, template gallery. Replaces the legacy graphics system.
- **Graphics — isometric 3D mode**: dual-mode editor (2D flat / isometric), 314-icon SCADA library, drag/connector tools, BACnet object picker with live values, undo, keyboard shortcuts.
- **Graphics — custom symbol library**: customer upload of SVG symbols, import/export, preload engine.
- **`/api/version` public identity endpoint**: returns version, model, vendor, vendor ID, BACnet protocol version + revision. No authentication required. Designed for asset inventory across a fleet of controllers.
- **Field Mode** + first-boot / OTA workflow refinements for service technicians working on un-networked controllers.
- **Persisted-state schema versioning** foundation: configuration and state files written by v2.0.0 are versioned so future releases can migrate older shapes forward without silently misreading on-disk state. Files from v1.0.0 installs load cleanly with no operator action required.
- **HHL Remote Support** (Professional): vendor-assisted troubleshooting is now available on request. Sessions require explicit customer approval each time; opt-in.
- **Image signature verification** on the appliance update path: a tamper-proof signature check runs before any new image is applied. Verification key is bundled on the appliance and can be independently confirmed by the customer.
- **Container hardening** updates applied to both appliance and customer Docker deployments.
- **Structured View** BACnet object type — hierarchical grouping of related objects for tools like YABE / Niagara.

### Changed

- **BACnet vendor identifier is now `1612`** (ASHRAE-registered to Humber Horizons / BACsync). Previously a placeholder. Operators with inventory systems that track vendor ID will see this change after upgrade.
- **HVAC library expanded to 19 classes**: PID + Deadband, ProofCheck, Timer, MinOnOff, RunHours, Interlock, HeatingCoolingLockout, FreezeProtect, StagingController, LeadLag, Economizer, LinearReset, RampLimiter, OptimalStart, LookupTable, MovingAverage, DutyCycle, AlarmWithSilence, Totalizer.
- **BACnet object types now 12** (added Structured View).
- **App Builder Modbus TCP** now supports function codes 01, 02, 03, 04, 05, 06, 16. (Documentation previously claimed FC0F; that function code is not implemented.)
- **Programs** UI: Stop/Start renamed to Disable/Enable; status badge updated correspondingly.
- **Web UI**: BSC-1000 model badge on login page; global alarm badge in sidebar nav (persists across pages); Release button added to write modal for priority relinquish.
- **Docker volume names aligned**: customer-facing `docker run` examples and `docker-compose.yml` now use the same volume names (`controller-data`, plus `./programs` bind mount), so switching from `docker run` to `docker compose up -d` no longer creates fresh empty volumes.
- **Hyper-V install instructions** now include the required `gunzip bacsync-controller.vhd.gz` step (the release artifact is `.vhd.gz`).
- **MCP server** now exposes 37 integration tools (up from 25 in v1.0.0).
- **License terms** now distributed as `LICENSE.md` (plain-English Community Edition terms). Replaces the absence of a license file in v1.0.0.

### Fixed

- **Comprehensive code review**: correctness and robustness improvements across the controller.
- **BSC-IO** stability: trend sync resumes correctly across board migration and removal; programs report status accurately; long-session stability improvements.
- **BSC-IO OTA**: chunked-transfer correctness at boundary sizes; reconnect-during-board-reboot timing handled cleanly.
- **Console log viewer**: live capture works reliably; cursor reset on view.
- **Graphics editor**: comprehensive stability pass across the new graphics subsystem. New Graphic / template picker, isometric save, viewer-token management, selector-write actions, imported graphics, and background image upload all hardened. Real-time updates are more efficient on graphics with many sparkline widgets, and the live-update channel survives idle disconnects cleanly.
- **Programs UI**: card-button interactions corrected.
- **App Builder reliability**: improved transient-failure recovery across drivers.

### Security

- **Image signature verification** end-to-end. Customers can independently confirm the signature on every downloaded image.
- **Container hardening** updates applied (see Changed).
- **BACnet/SC** connections enforce modern transport security and mutual authentication.
- **Comprehensive code review** addressing correctness and robustness across the controller.

### Documentation

- **USER-GUIDE.md** (in-controller, at `/ui/docs`): brought up to date with current object types, HVAC library, MCP tool count, `/api/version` endpoint, trademark line.
- **API-REFERENCE.md**: added full `GET /api/version` section.
- **DEPLOYMENT-GUIDE.md**: reconciled `:compiled` vs `:latest` tag scheme; cross-link to the public republish workflow.
- **LICENSE.md** added: plain-English Community Edition terms (free for personal + commercial use; safety exclusion; reverse-engineering prohibited; trademark + jurisdiction notes).

### Upgrade notes (v1.0.0 → v2.0.0)

- **Vendor ID change (999 → 1612)** is visible on the BACnet network. Inventory systems tracking vendor ID will see the new value after upgrade. No action required.
- **Persisted state files** written by v2.0.0 are versioned so future releases can migrate them forward. v1.0.0 file shapes load cleanly without operator action. If you need to roll back from v2.0.0 to v1.0.0, persistence files may need manual conversion — an in-place rollback path is not part of this release.
- **HHL Remote Support** (Professional) is opt-in. Deployments that prefer no vendor support channel can disable it via controller environment configuration; see `LICENSE.md` §7 for details.
- **Docker volume names** in customer install examples are aligned between `docker run` and `docker compose`. If you previously followed the v1.0.0 README's `docker run` example, your data is in a volume named `bacsync-data`. To preserve it when switching to the v2.0.0 compose pattern, either rename the volume to `controller-data` (re-create with a copy step) or keep pointing your run command at `bacsync-data` until you do a clean migration.
- **No license file required.** Community Edition remains free. Existing Professional `.lic` files continue to work without re-issuance.

---

## [1.0.0] — 2026-03-05

Initial public release of the BSC-1000 software BACnet controller.

Available as:
- Virtual appliance images: OVA (VMware / VirtualBox), VHD (Hyper-V), qcow2 (Proxmox / KVM)
- Container image: `ghcr.io/humber-horizons-limited/bsc-1000:latest`

Community Edition (free, no time limit) and Professional Edition (paid, license cryptographically bound to the controller).
