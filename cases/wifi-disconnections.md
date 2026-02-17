# Wi-Fi Disconnections on IoT and Smart TV Devices

## Problem Description and Observations
- Multiple devices located in the living room (baby monitor and smart TV) experienced frequent Wi-Fi disconnections.  
- Devices required manual reconnection and occasionally failed to reconnect entirely.
- Router located in same room
- 2.4 GHz and 5 GHz bands enabled on a single SSID
- Other devices in different rooms remained stable
- Issue persisted across reboots

## Hypotheses
- RF interference on 2.4 GHz band
- Band steering issues between 2.4 GHz and 5 GHz
- Channel congestion from nearby networks
- Client device compatibility limitations

## Troubleshooting Steps

1. Identified that the issue was isolated to specific IoT-class devices while other endpoints remained stable.
2. Established probable causes including band steering instability and 2.4 GHz channel congestion.
3. Tested hypotheses through controlled isolation:
   - Tested affected devices in alternate physical locations.
   - Created a dedicated 2.4 GHz-only SSID to remove band steering variables.
   - Manually assigned non-overlapping Wi-Fi channels (1, 6, 11).
4. Implemented corrective configuration:
   - Permanently separated 2.4 GHz and 5 GHz into distinct SSIDs.
   - Segmented IoT devices onto a dedicated SSID.
5. Verified functionality by monitoring reconnection behavior over time and confirming reduced disconnections.

## Resolution
Separating 2.4 GHz and 5 GHz SSIDs and assigning non-overlapping channels significantly reduced disconnections and improved reconnection reliability.

## Lessons Learned
- IoT devices often struggle with band steering
- Channel planning matters even in small environments
- Structured isolation prevents unnecessary hardware replacement

