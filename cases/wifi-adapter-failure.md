# Intermittent Wireless Adapter Failure – Windows (Hardware Replacement)
## Summary
Resolved Windows 10 Wi-Fi failures using Device Manager, ipconfig, and WLAN AutoConfig to isolate OS, driver, and service layers, identify M.2 wireless adapter hardware failure, and restore connectivity through hardware replacement.

## Problem Description and Observations
- A Windows 10 laptop began experiencing intermittent Wi-Fi disconnections.  
- Wi-Fi icon disappeared during failure events
- Wireless adapter intermittently missing in Device Manager
- Other devices on the network remained stable
- Issue progressed from intermittent drops to complete failure
- Ethernet connection remained stable
### Environment
- Windows 10 (64-bit)
- Internal M.2 wireless network adapter
- DHCP-based home network
- Dual-band router (2.4 GHz / 5 GHz)


## Hypotheses
- Wireless adapter disabled or misconfigured
- Corrupted or unstable driver
- Windows service dependency failure (WLAN AutoConfig)
- Progressive hardware degradation of the wireless card

## Troubleshooting Steps

1. Identified that the issue was isolated to the affected device by confirming other network devices remained stable and Ethernet restored connectivity.
2. Established probable causes including driver instability, service failure, or hardware degradation.
3. Tested hypotheses through controlled isolation:
   - Checked OS-level adapter detection via Device Manager and `ipconfig /all`.
   - Verified adapter was not administratively disabled.
   - Reinstalled and updated wireless drivers from manufacturer.
   - Confirmed WLAN AutoConfig service was running and set to Automatic.
4. Implemented corrective actions at the software level and monitored behavior.
5. Verified continued failure patterns, including consistent disappearance of the Wi-Fi icon and adapter from OS detection.

## Resolution
After software-level remediation failed and the adapter repeatedly disappeared from Windows detection, the internal M.2 wireless network card was physically replaced.

New hardware was installed and drivers configured.  
Wi-Fi connectivity remained stable following replacement.

## Lessons Learned
- If the adapter does not appear in Device Manager or `ipconfig`, the issue is likely below the TCP/IP layer.
- Ethernet testing is critical for isolating endpoint vs infrastructure issues.
- Persistent OS-level detection failure often indicates hardware degradation.
- Structured escalation prevents unnecessary network-side troubleshooting.
