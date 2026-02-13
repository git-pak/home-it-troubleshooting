# Wi-Fi Disconnections on IoT and Smart TV Devices

## Problem Description
Multiple devices located in the living room (baby monitor and smart TV) experienced frequent Wi-Fi disconnections.  
Devices required manual reconnection and occasionally failed to reconnect entirely.

## Initial Observations
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
1. Tested affected devices on alternate network locations
2. Created a dedicated 2.4 GHz-only SSID
3. Manually assigned Wi-Fi channels (1, 6, 11)
4. Segmented devices across SSIDs (IoT vs primary devices)
5. Monitored reconnection behavior over time

## Resolution
Separating 2.4 GHz and 5 GHz SSIDs and assigning non-overlapping channels significantly reduced disconnections and improved reconnection reliability.

## Lessons Learned
- IoT devices often struggle with band steering
- Channel planning matters even in small environments
- Structured isolation prevents unnecessary hardware replacement
