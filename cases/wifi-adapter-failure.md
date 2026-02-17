# Intermittent Wireless Adapter Failure – Windows (Hardware Replacement)

## Problem Description
A Windows 10 laptop began experiencing intermittent Wi-Fi disconnections.  
Over time, the issue worsened until the wireless adapter failed completely.

Each time connectivity was lost, the Wi-Fi icon in the Windows taskbar disappeared entirely, as if wireless capability did not exist on the system.

Ethernet connectivity consistently restored internet access, indicating the issue was isolated to the wireless subsystem.

## Environment
- Windows 10 (64-bit)
- Internal M.2 wireless network adapter
- DHCP-based home network
- Dual-band router (2.4 GHz / 5 GHz)

## Observed Behavior
- Wi-Fi icon disappeared during failure events
- Wireless adapter intermittently missing in Device Manager
- Other devices on the network remained stable
- Issue progressed from intermittent drops to complete failure

---

## Troubleshooting Process

### Step 1 — Confirm OS-Level Adapter Detection

Checked whether Windows recognized the wireless adapter:

- **Device Manager → Network adapters**
- `ipconfig /all`

During failure events, no wireless adapter appeared.

Conclusion:  
If the adapter is not detected at OS level, the issue is not DHCP or TCP/IP related.

---

### Step 2 — Verify Adapter Not Disabled

Checked for administrative disablement:

- Settings → Network & Internet → Advanced network settings
- Device Manager → Ensure adapter is enabled

No manual disablement detected.

---

### Step 3 — Validate Driver Integrity

Inspected Device Manager for:

- Warning icons (⚠️)
- “Unknown device” entries
- Driver errors

Actions taken:
- Reinstalled wireless driver
- Updated to latest manufacturer driver

Issue persisted.

---

### Step 4 — Verify Required Service

Checked Windows service dependency:

- `services.msc`
- WLAN AutoConfig → Confirmed Running and Startup Type = Automatic

Service was functioning properly.

---

### Isolation Testing

- Connected via Ethernet → Internet restored immediately.
- Confirmed router and ISP stability using other devices.
- Observed consistent disappearance of adapter during Wi-Fi failure events.

---

## Resolution

After software-level troubleshooting failed and the adapter repeatedly disappeared from OS detection, the internal M.2 wireless network card was physically replaced.

New adapter installed and drivers configured.

Wi-Fi connectivity remained stable following replacement.

---

## Root Cause

Progressive hardware failure of the internal wireless adapter caused repeated OS-level detection loss, ultimately resulting in complete wireless failure.

---

## Lessons Learned

- If the adapter is not visible in Device Manager or `ipconfig`, the issue is below the TCP/IP layer.
- OS-level detection failure narrows troubleshooting away from DHCP/network configuration.
- Structured escalation prevents unnecessary network-side troubleshooting.
- Consistent symptom patterns over time often indicate hardware degradation.
