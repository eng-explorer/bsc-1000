# BSC-1000 Community Edition — Software License Terms

**Effective date:** 2026-06-03
**Licensor:** Humber Horizons Limited ("HHL"), Ontario, Canada

These terms govern your use of the BSC-1000 BACnet Controller software in its
**Community Edition** form, including any virtual appliance image, container
image, or supporting integration files distributed from this repository or
from `ghcr.io/humber-horizons-limited/`.

By installing, running, or distributing the Software you agree to these terms.
If you do not agree, do not install or run the Software.

---

## 1. Grant of use

HHL grants you a worldwide, royalty-free, non-exclusive, non-transferable
right to install and run an unlimited number of instances of the BSC-1000
Community Edition for any lawful purpose — personal, internal commercial,
or production. No fee is charged and no separate license file is required for
Community Edition use.

## 2. Community Edition limits

The Software enforces certain feature limits in code (number of control
programs, trend logs, schedules, applications, custom graphics, user
accounts, and the protocols / interfaces enabled by default). These limits
are part of the Community Edition. To remove them, see Section 9
(Professional Edition).

## 3. What you may do

- Install and run the Software on your own hardware or virtual infrastructure.
- Use it in commercial settings, including charging for services delivered
  with the Software.
- Distribute the unmodified container image, virtual appliance image, or this
  repository's integration files (compose, README, examples) to others,
  provided this LICENSE accompanies the distribution.
- Configure, integrate, develop on top of, and write control programs against
  the Software's public APIs (REST, MCP, BACnet, BACnet/SC, MS/TP, Modbus,
  MQTT, OPC UA, HTTP, EtherNet/IP, SNMP, OPC UA Server, web UI).

## 4. What you may not do

- Reverse-engineer, decompile, disassemble, or otherwise attempt to derive
  the source code of any compiled binary distributed by HHL.
- Modify the Software's compiled binaries or repackage them under a
  different name or branding.
- Remove, disable, or circumvent any feature-limit enforcement, license
  checks, telemetry, or attribution.
- Use the names "BACsync", "BSC-1000", "Humber Horizons", or related logos
  except to refer accurately to the Software (e.g., "this device runs
  BACsync BSC-1000").
- Sublicense, sell, or rent the Software itself as a stand-alone product.
  (Selling integration services or solutions built on top of it is fine.)

## 5. Safety disclaimer — read this

THE SOFTWARE IS NOT DESIGNED FOR USE IN LIFE-SAFETY-CRITICAL APPLICATIONS,
including nuclear, medical life-support, aviation control, mass transit
control, weapons systems, or any application where failure could result in
death, personal injury, or severe property damage. Use in such systems is
at your sole risk and outside the intended scope of the Software.

Building HVAC, lighting, energy management, irrigation, agriculture, light
industry, environmental monitoring, and similar non-life-safety applications
are within scope.

## 6. No warranty

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT. IN NO EVENT SHALL
HHL BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY, WHETHER IN AN
ACTION OF CONTRACT, TORT, OR OTHERWISE, ARISING FROM, OUT OF, OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## 7. Network communications and telemetry

By default the Software may attempt outbound network connections to
HHL-operated coordination services for: license validation (Professional
Edition only), software update notifications, anonymous telemetry of
controller version and feature usage, and — only when the operator
explicitly approves an active session — outbound reverse SSH tunnels for
support purposes.

You may disable these features from the controller's Settings page. The
Software remains fully functional with all outbound HHL connections
disabled.

## 8. Image signatures

Container and virtual appliance images distributed by HHL are signed with
[Sigstore cosign](https://www.sigstore.dev/). The verification key is
published in this repository at `cosign.pub`. You are encouraged to
verify signatures before deployment in production.

## 9. Professional Edition

The Professional Edition unlocks the full feature set (unlimited programs,
trends, schedules, App Builder apps, graphic pages, users; alarm email;
MQTT Bridge; Modbus TCP Server; read-write OPC UA Server; BACnet/SC;
MS/TP; full SSH console; network diagnostics; multi-user RBAC; priority
support). It requires a separate paid license, delivered as a machine-bound
`.lic` file. Contact `info@humberhorizons.ca` for terms and pricing.

The Professional Edition is governed by a separate written agreement
between you and HHL. These Community Edition terms do not grant any
Professional Edition rights.

## 10. Term and termination

Your rights under these terms continue for as long as you comply with them.
If you materially breach Sections 4 or 5, your rights terminate
automatically. On termination, you must stop using and distributing the
Software. Sections 5, 6, and 11 survive termination.

## 11. Governing law

These terms are governed by the laws of the Province of Ontario, Canada,
and the laws of Canada applicable therein, excluding any choice-of-law
rules that would direct the application of any other jurisdiction's laws.
Disputes are subject to the exclusive jurisdiction of the courts of
Ontario.

## 12. Trademarks

"BACsync", "BSC-1000", "BSP-1000", and the Humber Horizons logo are
trademarks of Humber Horizons Limited.

## 13. Contact

- Licensing and general inquiries: `info@humberhorizons.ca`
- Website: `https://humberhorizons.ca`

---

*These terms supersede any prior license or terms-of-use statements
distributed with this Software prior to the effective date above. HHL
may publish updated versions of these terms with future releases; the
version of the terms in effect for any particular release is the one
shipped with that release.*
