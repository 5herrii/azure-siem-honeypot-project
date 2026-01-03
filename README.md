# azure-siem-honeypot-lab
Cloud-based SOC lab using Azure, Windows VM (honeypot), Log Analytics, and Microsoft Sentinel to analyze real-world attack traffic on attack map.
# Azure Honeypot + Microsoft Sentinel (Mini SOC Lab)

## Overview
Built a cloud-based SOC lab using Azure and Microsoft Sentinel to collect, analyze,
and visualize real-world attack traffic against a Windows honeypot VM.

## What This Project Demonstrates
- Cloud security fundamentals (Azure VM, VNet, NSG)
- Centralized logging with Log Analytics Workspace
- SIEM analysis using Microsoft Sentinel
- KQL querying and log enrichment
- Attack visualization using Sentinel workbooks (Attack Map)

## Architecture
Internet → Windows VM (Honeypot) → Azure Monitor Agent → Log Analytics → Sentinel


## Key Skills Used
- Azure
- Microsoft Sentinel (SIEM)
- Log Analytics Workspace
- KQL
- Windows Security Logs (Event ID 4625)

## Highlights
- Collected thousands of real failed logon attempts within hours
- Identified attacker source countries using GeoIP enrichment
- Built an interactive attack map dashboard

## Screenshots
(Insert screenshots here)

## Future Improvements
- Create Sentinel analytic rules and incidents
- Add automated alerts for brute-force behavior
- Implement post-incident hardening
