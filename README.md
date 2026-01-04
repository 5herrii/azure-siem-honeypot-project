# azure-siem-honeypot-lab
Cloud-based SOC lab using Azure, Windows VM (honeypot), Log Analytics, and Microsoft Sentinel to analyze real-world attack traffic on attack map.
# Azure Honeypot + Microsoft Sentinel (Mini SOC Lab)

## Overview
Built a cloud-based SOC lab using Azure and Microsoft Sentinel to collect, analyze,
and visualize real-world attack traffic against a Windows honeypot VM and then visualize the attackers location(s) on the Attack Map.

## What This Project Demonstrates
- Cloud security concepts (Azure VM, VNet, NSG)
- Centralized logging with Log Analytics Workspace
- SIEM analysis using Microsoft Sentinel
- KQL querying and log enrichment
- Attack visualization using Sentinel workbooks (Attack Map)

## Architecture
Public Internet → NSG → Windows VM (Honeypot) → Log Analytics Workspace → Sentinel → Attack Map


<img width="1024" height="768" alt="Project Flow Diagram" src="https://github.com/user-attachments/assets/9dc3bd58-4b1f-4c1e-9836-63420fcbb389" />

## Highlights
- Collected thousands of real failed logon attempts within hours
- Identified attacker source countries using GeoIP enrichment
- Built an interactive attack map dashboard

## Screenshots

<img width="1919" height="860" alt="Log Analytics 10" src="https://github.com/user-attachments/assets/8e008854-4d5a-47e1-802b-8165c8938cc1" />
<img width="1472" height="784" alt="Last" src="https://github.com/user-attachments/assets/a31dc6db-23b2-4f02-b132-398f958143f3" />


## Future Improvements
- Create Sentinel analytic rules and incidents
- Add automated alerts for brute-force behavior
