# Lab Report: Wazuh Endpoint Agent Installation, Infiltration, and SIEM Enrollment

* **Date of Operation:** September 21, 2026
* **SIEM Management Interface IP:** `192.168.6.133`
* **Enrolled Target Endpoint IP:** `192.168.6.130`
* **Target Desktop Environment:** Linux Mint 22.3 (Wilma)
* **Core Toolsets Deployed:** `wget`, `dpkg`, `systemctl`, Wazuh Endpoint Wizard
* **Status:** Central Enrollment Matrix Confirmed 100% Operational

---

## 1. Executive Summary
This post-installation laboratory report records the configuration, network setup, and enrollment verification of a Wazuh endpoint logging agent onto a remote Linux target. Operating inside a Type-2 hypervisor domain, a Linux Mint desktop node was configured as a target workspace asset. Utilizing the cloud operations console, custom installation variables were generated to bind the device to the centralized SIEM manager IP location (`192.168.6.133`). Following command-line package execution and system utility activation strings, the client endpoint successfully initialized telemetry streams. Connection indicators were verified on both the host workstation terminal and the central SIEM server console dashboard, confirming active enrollment.

---

## 2. Dynamic Command Generation & Parameter Building
To ensure smooth agent onboarding, registration profiles were established inside the Wazuh Dashboard deployment engine interface:
* **Target OS Selection:** Linux (`x86_64` Debian-based package framework layout).
* **Manager Binding Coordinate:** Exposing the permanent IP address block: `192.168.6.133`.
* **Agent Identifier Designation:** Customized with the unique asset token tag: `Linux_Mint`.
* **Group Definition Hook:** Assigned to the default infrastructure processing node ring: `default`.

The enrollment interface compiled these structural configurations into a single installation command string:
```bash
wget https://wazuh.com && sudo WAZUH_MANAGER='192.168.6.133' WAZUH_AGENT_NAME='Linux_Mint' dpkg -i ./wazuh-agent_4.14.7-1_amd64.deb
```

[IMAGE PLACEHOLDER: image_wCZyBh.png - Wazuh Deploy New Agent Wizard configuration screen highlighting selection of Linux DEB package and assignment of manager address 192.168.6.133]

[IMAGE PLACEHOLDER: image_4zFhoh.png - Wazuh Optional Settings layout displaying the custom agent name specification input block designated as Linux_Mint]

[IMAGE PLACEHOLDER: image_VhQ9Nu.png - Generated command matrix inside Wazuh Dashboard showing the explicit wget string and systemctl service start procedures]

---

## 3. Client-Side Installation & Daemon Infiltration
The generated package script was executed inside a root terminal workspace on the Linux Mint virtual node (`mint@mint-virtual-machine`). The `dpkg` installer unpacked the binary hooks, established the system user files, and compiled the configuration parameters inside the persistent server path `/var/ossec/etc/ossec.conf`.

To link the connection, the following administration commands were executed:
```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

### Client Daemon Status Audit
To confirm the local collector engine was up and running, a status audit was performed: `sudo systemctl status wazuh-agent`. The terminal telemetry confirmed a pristine execution ring:
* **Active Status:** `active (running) since Mon 2026-09-21 17:42:18 GMT; 7s ago`
* **Process Lineage Control:** Main Process PID initialized under tracking descriptor `7799`.
* **Memory Utilization Baseline:** Running within a safe footprint of `81.3M`.
* **Active Working Workers:** Spun up four key processing engines: `wazuh-execd`, `wazuh-agentd`, `wazuh-syscheckd`, and `wazuh-logcollector`.

[IMAGE PLACEHOLDER: image_ZaURA4.png - Linux Mint bash terminal output panel confirming active running status of wazuh-agent service with PID 7799 and active thread components]

---

## 4. SIEM Server Console Enrollment Verification
Following client execution, web validation checks were conducted by loading the manager UI framework at `https://192.168.6.133`.

### A. Agents Dashboard Telemetry Summary
Prior to performing the remote endpoint script installation steps, the central monitoring portal registered an entirely unmanaged host state:

[IMAGE PLACEHOLDER: image_mqJfxB.png - Empty Wazuh Dashboard baseline interface stating that the instance has no agents registered and prompting deployment]

Following successful deployment of the client collectors, the total agent metrics immediately refreshed across the central dashboard layout:

[IMAGE PLACEHOLDER: image_KFyQtn.png - Updated Wazuh Main Dashboard console revealing one active connected agent and tracking 43 medium severity security events]

### B. Analytical Asset Grid Verification
Navigating straight to the system `/endpoints-summary/` dashboard table confirms the exact agent properties parsed by the manager engine:
* **Assigned Asset ID:** `001`
* **Registered Node Name:** `Linux_Mint`
* **Static Host Address Location:** `192.168.6.130`
* **Target Operating System:** `Linux Mint 22.3`
* **Core Agent Software Version:** `v4.14.7`
* **Real-Time Operational Standing:** **`● active`**

[IMAGE PLACEHOLDER: image_5faXbA.png - Wazuh Endpoints registry table detailing the row tracking record for Agent 001 with active status verification under Linux Mint 22.3]

---

## 5. Security Architecture Findings & Incident Metrics
Upon enrollment, the agent automatically executed a vulnerability sweep and baseline log sync. The server telemetry interface recorded:
* **Total Incident Traffic Alerting Count:** Over a brief initialization window, the SIEM engine processed **43 Medium-Severity Alerts** (Rule levels 7 to 11) and **20 Low-Severity Alerts** (Rule levels 0 to 6).
* **Defensive Baseline Conclusion:** The central SIEM server node has established stable control over the target. System health indicators are reporting green, confirming that system logging data points are traversing the network securely.
