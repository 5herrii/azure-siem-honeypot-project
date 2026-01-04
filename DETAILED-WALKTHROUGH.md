## What I Did (Detailed Breakdown)

I built this project to simulate a real-world SOC workflow in the cloud enviornment. The goal was to deploy an intentionally exposed machine (a honeypot), then collect security and event logs from it, centralize the logs, analyze them like a SOC analyst, and then visualize where the attacks were coming from using a SIEM dashboard (basically an attack map). Instead of relying on sample or pre-generated data, I used **live attack traffic from the public internet** for a more realistic experience.

---

### 1) Azure Environment Setup (Resource Group + Network)

I first started by creating a **Resource Group** to keep all the lab resources organized in one place.  
After that, I created a **Virtual Network (VNet)** and **Subnet** to host the Windows virtual machine inside an Azure network.

---

### 2) Deploying the Honeypot VM (Windows)

Next, I deployed a **Windows virtual machine** inside the VNet and subnet.  
As part of the deployment, Azure automatically created the following supporting components:

- A **Public IP address** for internet exposure  
- A **Network Interface (NIC)**  
- A **Network Security Group (NSG)**  
- The VM’s **OS disk**

This virtual machine was intentionally used as a **honeypot**. Its purpose was not to be secure, so that it attract scans and brute-force login attempts from the public internet.

---

### 3) Intentionally Exposing the VM (Lab Purposes Only)

To make the VM easy to be discovered and attacked:
- I modified the **NSG inbound rules** to allow all inbound traffic.
- I connected to the VM using **RDP** to confirm access.
- I disabled the **Windows Defender Firewall** inside the VM, which increased visibility and allowed traffic such as ICMP.
- I verified exposure by successfully pinging the VM’s **public IP address** from my local machine.

This ensured the VM would begin receiving real attack traffic.

---

### 4) Verifying Local Security Logs (Windows Event Viewer)

Before forwarding logs into the SIEM, I verified that the VM itself was logging useful security events:
- Opened **Event Viewer → Windows Logs → Security**
- Focused on **Event ID 4625**, which shows the failed login attempts
- Generated a few failed logons using fake usernames to confirm logging behavior

This step confirmed that the endpoint was producing the exact telemetry, which was needed for detection and investigation.

---

### 5) Creating the Central Log Repository (Log Analytics Workspace)

Once local logging was confirmed, I then created an **Azure Log Analytics Workspace**.  
This workspace acts as the centralized location where all there security logs are stored and queried.
In a real SOC environment, this would be the primary source analysts rely on when investigating the security events.

---

### 6) Connecting the SIEM (Microsoft Sentinel)

After creating the workspace, I enabled **Microsoft Sentinel** on top of it.  
This transformed the Log Analytics Workspace into a full SIEM, allowing me to:
- Query logs  
- Build dashboards and visualizations  
- Prepare the environment for future detections, alerts, and incidents  

---

### 7) Forwarding Windows Logs to Azure

To send logs from the VM into Log Analytics:
- I used the **Azure Monitor Agent (AMA)** to recieve Virtual Machine's logs on Sentinel.
- I created a **Data Collection Rule (DCR)** to collect all event logs.
- I verified successful ingestion of the logs by querying the `SecurityEvent` table and observing live events appear.

At this point, the logging pipeline from the VM to the SIEM was fully functional.

---

### 8) Finding Real Attacks with KQL

With logs coming in, I began investigating attack activity using **KQL (Kusto Query Language)**:
- Queried the `SecurityEvent` table
- Filtered specifically for **Event ID 4625** to show failed logon attempts only
- Focused on fields such as:
  - `TimeGenerated`
  - `Account`
  - `Computer`
  - `IpAddress`

Within a short span of time, I observed a very high volume of failed login attempts, showing how quickly exposed systems are targeted once they are reachable from the public internet.

---

### 9) GeoIP Enrichment Using a Sentinel Watchlist

The raw security logs only showed attacker IP addresses, so I added geographic context:
- Uploaded a **GeoIP CSV file** into Sentinel as a **Watchlist**
- Used `_GetWatchlist('geoip')` in KQL to reference this data
- This joined attacker IP addresses with geographic fields such as country, city, latitude, and longitude

This enrichment made the attack data much easier to understand and visualize.

---

### 10) Building the Attack Map Dashboard (Sentinel Workbook)

To bring everything together, I created an **Attack Map dashboard** using a Sentinel Workbook:
- Aggregated failed login attempts by geographic location
- Plotted attacker locations using latitude and longitude
- Displayed the results on an world map (attack map)

The final result is a SOC-style dashboard that updates automatically as new attack data is ingested into it.

