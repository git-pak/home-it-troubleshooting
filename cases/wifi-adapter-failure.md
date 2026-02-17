# Intermittent Wireless Adapter Failure – Windows (Hardware Replacement)

## Problem Description
A Windows 10 laptop initially experienced intermittent Wi-Fi connectivity issues.  
Connections would randomly drop and temporarily restore after reboot. Over time, the issue progressively worsened until the wireless adapter failed completely.

Each time connectivity was lost, the Wi-Fi icon in the Windows taskbar disappeared entirely, as if wireless capability did not exist on the system.

## Environment
- Windows 10 (64-bit)
- Internal M.2 wireless network adapter
- DHCP-based home network
- Dual-band router (2.4 GHz / 5 GHz)

## Initial Observations
- Other devices on the network remained stable
- Ethernet connection consistently restored full internet access
- Wi-Fi icon disappeared every time connectivity was lost
- Wireless adapter intermittently failed to appear in Device Manager
- Issue progressed from intermittent failure to complete loss of wireless functionality

## Symptoms
- Random Wi-Fi disconnections
- Wi-Fi option disappearing from taskbar
- Wireless adapter missing in Device Manager during failure events
- Event Viewer logging adapter initialization warnings/errors
- Eventually, no wireless connectivity available

## Hypotheses
- Corrupted or unstable wireless driver
- Power management disabling the adapter
- Windows network stack corruption
- Progressive hardware failure of the wireless card

## Troubleshooting Steps

1. Verified issue was isolated to the affected device by testing other endpoints.
2. Confirmed router and ISP stability by connecting via Ethernet (which restored consistent internet access).
3. Checked Device Manager during failure events and observed adapter disappearance.
4. Reinstalled and updated wireless adapter drivers.
5. Disabled power management settings allowing Windows to turn off the adapter.
6. Reset TCP/IP stack using `netsh int ip reset`.
7. Renewed DHCP lease using `ipconfig /release` and `ipconfig /renew`.
8. Reviewed Event Viewer logs for recurring adapter initialization errors.
9. Monitored symptom progression from intermittent instability to total failure.

## Resolution
Physically replaced the internal M.2 wireless network card with a compatible adapter.  
Installed updated drivers and verified stable Wi-Fi connectivity during extended monitoring.

## Root Cause
Progressive hardware failure of the internal wireless adapter caused repeated device initialization failures, resulting in loss of OS-level detection and eventual complete wireless failure.

## Lessons Learned
- If the Wi-Fi icon disappears, the issue likely involves hardware detection rather than simple connectivity.
- Symptom consistency across failures is a critical diagnostic clue.
- Ethernet testing effectively isolates infrastructure vs endpoint issues.
- Structured escalation prevents unnecessary troubleshooting repetition.
