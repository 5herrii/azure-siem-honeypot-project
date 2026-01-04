# Azure Honeypot (SOC) Lab
Cloud-based SOC lab built using Azure, a Windows honeypot VM, Log Analytics Workspace, and Microsoft Sentinel to observe and analyze real-world attack activity and visualize attacker locations on an attack map.

## Overview
In this project, I built a cloud-based SOC lab using Microsoft Azure and Sentinel.
A Windows virtual machine was intentionally exposed to the public internet to act as a honeypot and attract real attackers. Security logs from the VM were collected, centralized using Log Analytics Workspace, analyzed, and then visualized on an Attack Map to show where attacks were originating from around the world.

The goal of this lab was to understand how endpoint logs flow into a SIEM, how the analysts investigate failed authentication attempts, and how raw security data can be turned into meaningful visual information.

## What This Project Demonstrates
- Core cloud security concepts using Azure (Virtual Machines, VNets, NSGs)
- Centralized log collection with Azure Log Analytics Workspace
- SIEM setup and analysis using Microsoft Sentinel
- Threat investigation using KQL (Kusto Query Language)
- Log enrichment using GeoIP data
- Visualizing attack activity through Sentinel workbooks (Attack Map)

## Architecture
Public Internet → NSG → Windows VM (Honeypot) → Log Analytics Workspace → Sentinel → Attack Map


<img width="1024" height="768" alt="Project Flow Diagram" src="https://github.com/user-attachments/assets/9dc3bd58-4b1f-4c1e-9836-63420fcbb389" />

## Highlights
- Collected thousands of real failed login attempts within a short time of exposing the VM
- Analyzed Windows Security Events, focusing on Event ID 4625 (failed logons)
- Enriched attacker IP addresses with geographic data 
- Built an attack map (interactive world map showing attacker locations)

## Screenshots

<img width="1919" height="860" alt="Log Analytics 10" src="https://github.com/user-attachments/assets/8e008854-4d5a-47e1-802b-8165c8938cc1" />
<img width="1472" height="784" alt="Last" src="https://github.com/user-attachments/assets/a31dc6db-23b2-4f02-b132-398f958143f3" />


## Future Improvements
- Create Microsoft Sentinel analytics rules to automatically detect brute-force behavior
- Generate incidents and alerts based on suspicious activity and known patterns
- Apply post-incident hardening (restrict NSG rules, enable firewall, limit RDP access)
