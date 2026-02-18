

| # | Vulnerability | Location | Risk Level |
|---|---------------|----------|:----------:|
| 1 | **Hard-coded WiFi credentials** | Both files, lines 5-6 | 🔴 **Critical** |
| 2 | **Exposed ThingSpeak API key** | NodeMCU code, line 14 | 🔴 **Critical** |
| 3 | **No authentication on video server** | ESP32-CAM, entire server | 🔴 **Critical** |
| 4 | **HTTP (no TLS/SSL) on port 80** | ESP32-CAM, line 7 | 🟠 **High** |
| 5 | **No input validation** | Both files | 🟠 **High** |
| 6 | **Debug information exposed** | Serial outputs throughout | 🟡 **Medium** |
| 7 | **No rate limiting** | Server accepts unlimited requests → DoS vulnerability |
| 8 | **Missing boundary checks** | No validation on image size before transmission |
| 9 | **No session management** | Any client can access video feed indefinitely |
| 10 | **No firmware integrity checks** | No secure boot or signature verification |
| 11 | **Information disclosure** | Serial prints reveal IP addresses, connection status |
| 12 | **No access logs** | Cannot audit who accessed the system |
| 13 | **Default configurations** | No password rotation mechanism |
| 14 | **No HTTPS redirect** | Even if added, port 80 remains open |


## 2. Realistic Attack Scenarios

### Scenario 1: Rogue Access Point Attack
**How it works:**
1. Attacker sets up a rogue WiFi with same SSID ("CONFERENCE HALL")
2. Drone connects to attacker's network instead of legitimate one
3. Attacker gains full access to video feed and sensor data


### Scenario 2: API Key Extraction
**How it works:**
1. Attacker decompiles firmware or gains network access
2. Extracts ThingSpeak API key `6VP9XFXYB1F2N22I`
3. Sends fake data to cloud channel or intercepts real data


### Scenario 3: Unauthorized Video Surveillance
**How it works:**
1. Anyone on the same network discovers the drone's IP (via scanning)
2. Accesses `http://[drone-ip]/cam-hi.jpg`
3. Views live video with no authentication required


### Scenario 4: Denial of Service
**How it works:**
1. Attacker floods the ESP32-CAM with HTTP requests
2. Device resources exhausted
3. Video streaming stops; drone operations impacted

### Scenario 5: Man-in-the-Middle (MITM)
**How it works:**
1. Unencrypted HTTP traffic allows packet interception
2. Attacker views video streams and sensor data in transit
3. Can modify or inject data



## 3. Business Impact Analysis


| Impact Category | Consequence |
|-----------------|-------------|
| **Reputational Damage** | Client data exposure leads to loss of trust and future contracts |
| **Regulatory Fines** | GDPR/CCPA violations from unencrypted personal data (video footage) |
| **Competitive Disadvantage** | Proprietary surveillance patterns and operational data leaked |
| **Operational Disruption** | DoS attacks render drone useless during critical windows |
| **Legal Liability** | Unauthorized surveillance via compromised drones could lead to lawsuits |
| **Physical Security Breach** | Attackers could use compromised drones to map facilities and bypass physical security |


## 4. Mitigation Strategies (High-Level)

### Immediate Fixes 

| # | Issue | Mitigation |
|---|-------|------------|
| 1 | Hard-coded credentials | Move to secure storage, runtime input |
| 2 | Exposed API key | Environment variables, secure element |
| 3 | No authentication | Implement basic auth or token-based access |
| 4 | HTTP | Enable HTTPS with certificates |
| 5 | No input validation | Add validation for all inputs |

### Architectural Improvements 

| # | Improvement | Benefit |
|---|-------------|---------|
| 1 | Secure boot & firmware signing | Prevents unauthorized firmware modification |
| 2 | Rate limiting & request throttling | Prevents DoS attacks |
| 3 | Session management | Tracks and controls client access |
| 4 | Audit logging | Forensic capability after incidents |
| 5 | Network segmentation | Isolate drone traffic from corporate network |

### Strategic Recommendations 

| # | Recommendation | Rationale |
|---|----------------|-----------|
| 1 | Hardware Security Module (HSM) | Store keys in tamper-resistant hardware |
| 2 | Over-the-Air (OTA) secure updates | Patch vulnerabilities remotely |
| 3 | Third-party security audit | Independent validation |
| 4 | Bug bounty program | Crowdsourced security testing |
| 5 | ISO 27001 compliance | Demonstrates security maturity to clients |



