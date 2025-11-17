# Wireless Troubleshooting

## Quick Reference Guide

### Critical Thresholds

- **Minimum Usable RSSI**: -70 dBm (typical roaming trigger)
- **Minimum Usable SNR**: 15 dB
- **Excellent RSSI**: -50 dBm or higher
- **Excellent SNR**: 40+ dB

### Common Issues Quick Lookup

| Symptom | Likely Cause | First Check |
| ------- | ------------ | ----------- |
| Can't connect | Authentication failure | Check credentials, certificate, RADIUS logs |
| Slow speeds | Poor signal or interference | Check RSSI, SNR, channel utilization |
| Frequent disconnects | Roaming issues | Check roaming settings, AP coverage |
| Intermittent connectivity | Interference or coverage gaps | Check channel overlap, RF environment |

### Key dB Values to Remember

- **+3 dB** = double the power
- **-3 dB** = half the power
- **+10 dB** = 10x the power
- **-10 dB** = 1/10th the power

## Understanding Wireless RF

RF or Radio Frequency is what enables wireless communication.

### Decibels

A decibel is a logarithmic unit of measurement that expresses the amount relative to a reference.

- 10 dB: when the power is 10 dB, the compared value is 10 times more powerful.
- 3 dB: when the power is 3 dB, the compared value is 2 times more powerful.
- 0 dB: equal power
- -3 dB: the compared value is half as powerful
- -10 dB: the compared value is one-tenth as powerful

### Attenuation

Wireless signals degrade over distance because the electromagnetic waves lose energy as they travel, making it harder to transfer data. Additionally, obstacles like walls and furniture can further weaken the signal, leading to slower communication speeds.

If the signal has to go through solid objects, this will weaken the signal further.

  | Object in Signal Path       | Signal Attenuation |
  | --------------------------- | ------------------ |
  | Plasterboard wall           | 3 dB               |
  | Glass wall with metal frame | 6 dB               |
  | Cinderblock wall            | 4 dB               |
  | Office window               | 1-3 dB             |
  | Metal door                  | 6 dB               |
  | Brick wall                  | 8 dB               |
  | Concrete wall               | 12 dB              |
  | Phone and body position     | 3-6 dB             |
  | Phone near field absorption | Up to 15 dB        |
  | Elevator shaft              | 30 dB              |

### Signal to Noise Ratio

Signal-to-noise ratio (SNR) evaluates a signal based on the noise present. SNR is the difference between the signal level and the noise floor. The higher the SNR, the better the signal quality.

  | SNR (dB) | Signal Quality |
  | -------- | -------------- |
  | 40+ dB   | Excellent      |
  | 25-40 dB | Good           |
  | 15-25 dB | Fair           |
  | 10-15 dB | Poor           |
  | <10 dB   | Unusable       |

### RSSI

RSSI stands for Received Signal Strength Indicator, which measures how well a device can receive a signal from a Wi-Fi router or access point. RSSI is measured in dBm (decibels relative to one milliwatt) and is typically a negative value. A higher (less negative) RSSI value indicates a stronger signal.

  | RSSI (dBm) | Signal Strength | Expected Performance               |
  | ---------- | --------------- | ---------------------------------- |
  | -30 dBm    | Excellent       | Maximum performance                |
  | -50 dBm    | Very Good       | Excellent for all applications     |
  | -60 dBm    | Good            | Reliable for most applications     |
  | -67 dBm    | Fair            | Minimum for reliable packet delivery |
  | -70 dBm    | Weak            | Typical roaming threshold          |
  | -80 dBm    | Poor            | Basic connectivity, frequent drops |
  | -90 dBm    | Unusable        | Approaching noise floor            |

## Wireless Protocols

Wireless protocols begin with 802.11. Below are the standards you're most likely to encounter in enterprise environments:

### 802.11n (WiFi 4)

**Released**: 2009
**Frequency Bands**: 2.4 GHz and 5 GHz
**Maximum Speed**: 600 Mbps (theoretical)
**Channel Width**: 20 MHz or 40 MHz
**Modulation**: 16-QAM and 64-QAM
**Spatial Streams**: Up to 4

**Key Features:**

- First dual-band standard
- Introduced MIMO (Multiple Input Multiple Output)
- Backward compatible with 802.11a/b/g

**Deployment Notes:**

- Still common in legacy devices
- 40 MHz channels on 2.4 GHz not recommended due to limited spectrum
- Being phased out but still supported for compatibility

### 802.11ac (WiFi 5)

**Released**: 2013
**Frequency Bands**: 5 GHz only
**Maximum Speed**: 6.9 Gbps (theoretical)
**Channel Width**: 20, 40, 80, or 160 MHz
**Modulation**: Up to 256-QAM
**Spatial Streams**: Up to 8

**Key Features:**

- **MU-MIMO** (Multi-User MIMO): Simultaneous transmission to multiple clients
- **Beamforming**: Directional signal transmission for better range
- **Channel bonding**: 4x 20 MHz → 80 MHz or 8x 20 MHz → 160 MHz
- 5 GHz only, reducing 2.4 GHz congestion

**Deployment Notes:**

- Current mainstream standard in most enterprises
- Excellent balance of speed, compatibility, and cost
- 80 MHz channels common, 160 MHz requires careful planning

### 802.11ax (WiFi 6 and WiFi 6E)

**Released**: 2019 (WiFi 6), 2020 (WiFi 6E)
**Frequency Bands**: 2.4 GHz, 5 GHz, and 6 GHz (6E only)
**Maximum Speed**: 9.6 Gbps (theoretical)
**Channel Width**: 20, 40, 80, or 160 MHz
**Modulation**: Up to 1024-QAM
**Spatial Streams**: Up to 8

**Key Features:**

- **OFDMA** (Orthogonal Frequency Division Multiple Access): More efficient spectrum use, similar to cellular technology
- **Target Wake Time (TWT)**: Improves battery life on mobile devices
- **BSS Coloring**: Reduces interference from neighboring networks
- **Uplink MU-MIMO**: Multi-user transmissions in both directions
- **WPA3**: Enhanced security protocol
- **WiFi 6E**: Adds 6 GHz band (1200 MHz additional spectrum)

**6 GHz Band Details (WiFi 6E):**

- 14 x 80 MHz channels (no overlap)
- 7 x 160 MHz channels (no overlap)
- Clean spectrum with no legacy devices
- Lower transmit power limits in some regions

**Deployment Notes:**

- Current recommended standard for new deployments
- Better performance in high-density environments
- 6E requires compatible clients and appropriate licensing/regulation
- Significant improvement for crowded networks (offices, stadiums, etc.)

### 802.11be (WiFi 7)

**Released**: 2024
**Frequency Bands**: 2.4 GHz, 5 GHz, and 6 GHz
**Maximum Speed**: 46 Gbps (theoretical)
**Channel Width**: 20, 40, 80, 160, or 320 MHz
**Modulation**: Up to 4096-QAM
**Spatial Streams**: Up to 16

**Key Features:**

- **Multi-Link Operation (MLO)**: Simultaneous transmission across multiple bands
- **320 MHz channels**: Available on 6 GHz band only
- **4K-QAM**: Higher modulation for increased throughput
- **Multi-Resource Units (MRU)**: More flexible spectrum allocation
- Extremely low latency for real-time applications

**Deployment Notes:**

- Emerging standard, limited enterprise deployment as of 2025
- Requires WiFi 7 capable clients (still uncommon)
- Best suited for ultra-high-density or latency-sensitive applications
- Consider cost vs. benefit - WiFi 6E sufficient for most current needs

## Wireless Security

Enterprise environments usually use WPA3 Enterprise.

Guest clients get redirected to a portal to go through an authentication process and agree to Terms of Use.

Enterprise clients usually authenticate with a certificate using an EAP protocol.  Their authentication are cached and shared with other APs so that they can roam from AP to AP without re-authenticating.  For this reason, client devices should be set to a more aggressive roaming level.

### Cisco ISE (Identity Services Engine)

Cisco ISE serves as our centralized RADIUS server for wireless authentication, providing policy-based network access control.

#### EAP-TLS Authentication

We use EAP-TLS (Extensible Authentication Protocol - Transport Layer Security) for enterprise wireless clients. This is the most secure EAP method as it uses certificate-based mutual authentication.

**EAP-TLS Requirements:**

- **Client certificate**: Each device must have a valid client certificate installed
- **CA certificate**: Client must trust the Certificate Authority that signed the RADIUS server certificate
- **ISE certificate**: ISE presents its server certificate to the client during authentication
- **No password required**: Authentication is entirely certificate-based

**Authentication Flow:**

1. Client associates with wireless network (WPA3-Enterprise)
2. RADIUS authentication request sent from wireless controller to ISE
3. ISE and client exchange certificates and establish TLS tunnel
4. ISE validates client certificate against configured policies
5. ISE returns authorization policies (VLAN, ACL, etc.) to wireless controller
6. Client receives network access with appropriate permissions

**Common EAP-TLS Issues:**

- Expired client or server certificates
- Missing or untrusted CA certificate on client device
- Certificate revocation list (CRL) checking failures
- Client certificate not matching ISE authorization policy
- Time synchronization issues between client and ISE

#### Checking Authentication in Cisco ISE

**Operations > RADIUS > Live Logs**

This is the primary location for troubleshooting wireless authentication:

- **Real-time view** of all RADIUS authentication attempts
- **Search filters**: Filter by username, MAC address, NAS IP (wireless controller), status
- **Authentication details**: Click on any entry to see full authentication flow
- **Failure reasons**: Clear explanation of why authentication failed
- **Authorization policies**: Shows which policies were matched and applied

**Key Information in Live Logs:**

- **Identity**: Username or MAC address of authenticating device
- **Endpoint ID**: Device MAC address
- **Authentication Method**: Should show EAP-TLS
- **Authentication Status**: Pass/Fail with detailed reason
- **Authorization Profile**: Which profile was applied (determines VLAN, ACL, etc.)
- **NAS IP Address**: Which wireless controller processed the request
- **Network Device**: AP or controller name
- **Timestamp**: When authentication occurred

**Other Useful ISE Locations:**

- **Context Visibility > Endpoints**: View all known endpoints and their status
- **Operations > Authentications**: Historical authentication records (not real-time)
- **Operations > Reports > Endpoints and Users**: Detailed authentication reports
- **Administration > System > Certificates**: Manage ISE certificates and trust stores
- **Policy > Policy Sets**: View authentication and authorization policies

#### ISE Troubleshooting Tips

1. **Certificate expiration**: Check certificate validity dates in ISE and on client devices
2. **Time synchronization**: Ensure client, ISE, and wireless controller clocks are synchronized (NTP)
3. **Certificate chain**: Verify complete certificate chain is present on both ISE and client
4. **Policy matching**: Check ISE Live Logs to see which policies are being matched
5. **Endpoint identity groups**: Verify device is in correct endpoint identity group
6. **Profiling**: ISE may profile devices incorrectly, affecting authorization
7. **RADIUS shared secret**: Ensure wireless controller and ISE have matching shared secret

#### Fast Roaming with ISE

ISE supports **PMK caching** and **802.11r** to enable fast roaming:

- **PMK caching**: Authentication session cached for configured timeout (default 24 hours)
- **Client roams** to new AP without full EAP-TLS re-authentication
- **Session continues** seamlessly for voice/video applications
- **Check in ISE Live Logs**: Look for "Session Resume" events during roaming

## Wireless Controllers

The wireless access points we will deal with in Enterprise environments are *lightweight* access points.  They depend on wireless controllers for most of their functionality.

The lightweight access points connect to the wireless controller through a CAPWAP (Control And Provisioning of Wireless Access Points) tunnel.  Wireless Controllers use this CAPWAP connection to control wireless access points.  Client Wireless Data traffic also goes through this tunnel to the Wireless Controller and then get sent on through to the destination.

### Anchor Controllers

Wireless Controllers can be configured pass Client Traffic to a different Wireless Controller over a CAPWAP tunnel.  This is often seen with Guest users.  If a client connects to a Guest Wifi, we probably want to send that client to a Wireless controller that terminates to a DMZ so that Guest clients can access the Internet but not Confidential internal network resources.

### Fortigate Wireless Controllers

Fortinet FortiGate firewalls can function as wireless controllers for FortiAP access points. This unified approach integrates wireless management with firewall and security functions.

**Key Features:**

- **Integrated security**: Apply firewall policies directly to wireless traffic
- **FortiAP management**: Configure and monitor FortiAPs from FortiGate GUI
- **Tunnel vs Local modes**:
  - Tunnel mode: All traffic flows through FortiGate (similar to CAPWAP)
  - Local mode: Traffic bridges locally, management through FortiGate
- **Guest portal**: Built-in captive portal for guest authentication
- **FortiClient integration**: Seamless VPN and security client integration

**Troubleshooting Notes:**

- Check FortiAP connection status in FortiGate: `WiFi & Switch Controller > Managed FortiAPs`
- Review wireless client list for connection details
- Monitor FortiAP tunnel status (similar to CAPWAP)
- Check FortiGate logs for wireless authentication and traffic events
- Verify FortiAP firmware compatibility with FortiGate version

### Cisco Wireless Controllers

Cisco wireless controllers manage Cisco lightweight APs through CAPWAP tunnels.

**Key Platforms:**

- **Catalyst 9800 Series**: Current generation, IOS-XE based
- **Legacy WLC (5520, 8540)**: AireOS-based, being phased out
- **Embedded controllers**: Integrated in switches or routers

**Troubleshooting Notes:**

- Access via web GUI or SSH
- Check AP join status: `show ap summary`
- View client details: `show client detail <MAC>`
- Check CAPWAP status: `show capwap client`
- Review logs in real-time or historical
- Use Prime Infrastructure for multi-controller management

## Wireless Roaming

### layer 2 roaming

This is the simplest kind of roaming.  Client stays on the same vlan with the same IP.  The only change is the client changes from being associated from one AP to another.  This is usually Intracontroller roaming where the client remains on the same wireless controller.

### layer 3 roaming

This is more complex.  The client can be moving far enough that the closest AP is connected to a different wireless controller with different vlans.  In this case, the client can be tunneled back to the original wireless controller.  If that's not possible, then the client will receive new IP addressing and all existing connections will be reset.  This type of roaming can cause the most interruptions to the client's experience.  Voip calls and video conferencing will disconnect for example.

### Client device roaming settings

#### 802.11r

802.11r is a standard that enhances Wi-Fi roaming by allowing devices to transition quickly and securely between different access points, improving connectivity for mobile devices. It is particularly useful for applications like voice over IP (VoIP), where maintaining a stable connection is crucial.

#### 802.11k

assisted roaming.  AP monitors RSSI of a client.  AP sends a message to Roam and provide neighbor APs and channel... up to 6 of these in a priority order.

#### 802.11v

can push clients to roam, but it doesn't provide more info.  The AP can deny association to client, shrinking cell size.  If RSSI is too bad, then AP can deny connectivity.

#### Windows 10/11

There are 3 roaming settings in Windows 11

- Low: Device sticks to one AP, reducing interruptions but may lead to poor connectivity in weak areas.
- Medium (Default): Balanced between maintaining a connection and switching to a better AP when needed
- High: Device frequently switches APs, which can cause connection drops during authentication.

These settings are in network adapter properties, advanced tab under Roaming Aggressiveness.

#### Mac OS and iPhone

Mac OS supports 802.11k, 802.11r and 802.11v protocols for roaming.  Devices detect when to roam by checking current RSSI in comparison of the RSSI of another access point.  If current signal goes below -70 dBm, then the device seeks to roam to the AP with better RSSI.

#### Android

To improve WiFi roaming aggressiveness on an Android device, you can adjust settings such as enabling roaming, setting a roaming trigger to -70 dBm, and configuring the background scan interval to every 20 seconds. These changes can help your device switch more effectively between access points as you move around.

## Channel Planning and Optimization

### 2.4 GHz Band

- Only 3 non-overlapping channels available: 1, 6, 11
- 20 MHz channel width recommended
- Longer range but more congested and interference-prone
- Better penetration through walls and obstacles

### 5 GHz Band

- 24+ non-overlapping channels available (depending on region)
- Can use 20, 40, or 80 MHz channel widths
- Less congested, higher throughput potential
- Shorter range, less wall penetration
- **DFS channels** (52-144): Require radar detection, may cause brief disconnects if radar detected

### 6 GHz Band (WiFi 6E/7)

- 14 x 80 MHz channels or 7 x 160 MHz channels
- No legacy devices, cleaner spectrum
- Very short range, requires dense AP deployment
- Best for high-density, high-performance environments

### Channel Width Considerations

- **20 MHz**: Maximum compatibility, better for high-density
- **40 MHz**: 2x throughput, moderate compatibility
- **80 MHz**: 4x throughput, requires clean spectrum
- **160 MHz**: 8x throughput, very spectrum-intensive

## Common Interference Sources

### RF Interference

- **Microwave ovens**: Operate at 2.4 GHz, can cause significant interference
- **Bluetooth devices**: Share 2.4 GHz spectrum
- **Cordless phones**: Older models use 2.4 GHz or 5 GHz
- **Baby monitors**: Often use 2.4 GHz
- **Neighboring APs**: Overlapping channels or high transmit power
- **Radar systems**: Can force DFS channel changes on 5 GHz
- **Wireless video cameras**: Continuous transmissions cause constant interference

### Physical Interference

- **Metal objects**: Reflect RF signals, create dead zones
- **Water**: Fish tanks, water heaters absorb RF signals
- **Mirrors**: Metal backing reflects signals
- **Dense construction materials**: See attenuation table above

### Detecting Interference

- Check channel utilization on wireless controller
- Use spectrum analyzer to identify non-WiFi interference
- Monitor packet retransmission rates
- Look for sudden drops in SNR without RSSI changes

## Common Issues and Solutions

### Authentication Failures

**Symptoms:**

- Client cannot connect despite correct password
- "Unable to join network" errors
- Repeated authentication attempts

**Common Causes:**

1. **Certificate issues** (Enterprise)
   - Expired certificates
   - Certificate trust chain problems
   - Wrong CA certificate installed
2. **RADIUS server issues**
   - RADIUS server unreachable
   - Incorrect shared secret
   - User not in correct group
3. **PSK mismatch** (Personal networks)
   - Wrong password entered
   - Special characters causing issues

**Resolution Steps:**

- Check RADIUS logs for authentication failures (Cisco ISE)
- Verify certificate validity and trust chain
- Test with known-good credentials
- Check wireless controller authentication logs
- Verify VLAN assignments for user role

### Poor Performance

**Symptoms:**

- Slow download/upload speeds
- High latency
- Buffering during streaming

**Common Causes:**

1. **Weak signal**: RSSI below -70 dBm
2. **Low SNR**: Below 15 dB
3. **Channel congestion**: High utilization on current channel
4. **Interference**: Non-WiFi devices causing noise
5. **Client capabilities**: Old devices limited to 802.11n or 2.4 GHz only

**Resolution Steps:**

- Check RSSI and SNR values
- Review channel utilization on controller
- Verify client is connecting to nearest AP
- Check client device capabilities (WiFi standard, band support)
- Consider AP placement adjustments
- Review transmit power settings

### Frequent Disconnections

**Symptoms:**

- Client drops connection repeatedly
- VoIP calls disconnecting
- Video conferences failing

**Common Causes:**

1. **Poor roaming configuration**: Client staying on weak AP too long
2. **Coverage gaps**: Areas with no strong AP signal
3. **Interference**: Intermittent RF interference
4. **AP overload**: Too many clients on one AP
5. **Controller issues**: CAPWAP tunnel instability

**Resolution Steps:**

- Check roaming aggressiveness settings on client
- Review AP coverage maps
- Monitor client association history across APs
- Check AP client count and utilization
- Verify CAPWAP tunnel stability
- Review controller and AP logs during disconnect events

### Intermittent Connectivity

**Symptoms:**

- Connection works but periodically stops responding
- Some applications work, others don't
- Random timeouts

**Common Causes:**

1. **Multicast/broadcast issues**: IGMP snooping misconfiguration
2. **DHCP problems**: Lease expiration, DHCP server unreachable
3. **DNS issues**: DNS server resolution failures
4. **Firewall blocking**: Traffic being blocked intermittently
5. **QoS settings**: Traffic being deprioritized

**Resolution Steps:**

- Verify IP address lease time and DHCP server reachability
- Test DNS resolution from client
- Check firewall logs for blocks
- Review QoS policies on controller
- Packet capture during issue occurrence

## Troubleshooting Tools and Commands

### Wireless Controller Tools

#### Client Lookup

- Search for client by MAC address, username, or IP
- View current association status
- Check RSSI, SNR, data rates
- Review authentication method and VLAN assignment

#### RF Metrics

- Channel utilization graphs
- Interference detection
- Neighboring AP discovery
- Client distribution across APs

#### Logs and Events

- Client authentication logs
- Roaming event logs
- AP connection logs (CAPWAP status)
- RADIUS authentication logs

### Client-Side Tools

#### Windows

- `netsh wlan show interfaces` - Current connection details
- `netsh wlan show networks mode=bssid` - Available networks with signal strength
- `netsh wlan show profiles` - Saved network profiles
- Network adapter properties - Check roaming aggressiveness

#### macOS

- Hold Option key + click WiFi icon - Detailed connection info (RSSI, channel, PHY mode)
- `airport -s` - Scan for networks (requires full path: `/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport`)
- `airport -I` - Current connection information
- Wireless Diagnostics app - Comprehensive analysis tool

#### Linux

- `iwconfig` - Wireless interface configuration
- `iw dev wlan0 scan` - Scan for networks
- `iw dev wlan0 link` - Current connection details
- `wavemon` - Real-time signal monitoring (if installed)

#### Mobile Devices

- **iOS**: Settings > WiFi > Information icon - Shows RSSI and connection details
- **Android**: WiFi Analyzer apps from Play Store
- Many vendors provide diagnostic apps

### Packet Capture

Use Wireshark or tcpdump to capture wireless frames for deep analysis:

- Authentication handshakes
- Roaming events (802.11r fast transition frames)
- Deauthentication causes
- Data transmission analysis

## Troubleshooting Steps

### Initial Information Gathering

**Collect the following information from the user:**

1. **User details**: Name, username, device MAC address (if available)
2. **Location**: Building, floor, room number
3. **Device type**: Laptop (OS version), phone (make/model), tablet, etc.
4. **Symptom details**:
   - When did the issue start?
   - Is it constant or intermittent?
   - Does it affect specific applications or all connectivity?
   - Can other nearby users connect successfully?
5. **SSID**: Which wireless network are they trying to connect to?
6. **Recent changes**: New device, OS update, password change, physical location move?

### Step-by-Step Troubleshooting Process

#### Step 1: Locate Client on Wireless Controller

1. **Search for the client** using MAC address, username, or IP address in the wireless controller
2. **Check if client appears**:
   - **Not found**: Client never successfully associated - likely authentication issue
   - **Found**: Proceed to gather connection details

#### Step 2: Review Current Connection Status

**If client is currently connected, check:**

- **RSSI**: Should be -70 dBm or better
  - **-70 dBm or worse**: Signal strength issue (see Step 3)
  - **-70 dBm or better**: Signal adequate (see Step 4)
- **SNR**: Should be 15 dB or higher
  - **Below 15 dB**: Interference likely (see Step 5)
- **Data rates**: Check current TX/RX rates
  - Very low rates may indicate poor RF conditions or client limitations
- **Associated AP**: Which AP is the client connected to?
  - Verify it's the nearest/strongest AP available
- **VLAN/IP assignment**: Verify correct network segment
- **Authentication method**: Check if using expected method (PSK, 802.1X, etc.)

#### Step 3: Poor Signal Strength (RSSI < -70 dBm)

**Possible causes:**

1. **Coverage gap**: Client is in an area with no nearby AP
2. **Sticky client**: Client associated to distant AP instead of nearer one
3. **Physical obstructions**: Dense walls, metal, or other barriers
4. **AP failure**: Nearby AP is down or malfunctioning

**Resolution steps:**

1. **Check AP status**: Verify nearby APs are online and functioning
   - Look for APs in the same area on controller
   - Check CAPWAP tunnel status
   - Review AP uptime and recent reboots
2. **Check coverage map**: Determine if location has adequate coverage
   - If no coverage: Recommend user move closer to AP or request AP installation
   - If coverage should exist: Investigate AP issues
3. **Review client association history**: Check if client is "stuck" on wrong AP
   - If yes: Increase roaming aggressiveness on client device
   - May need to disconnect/reconnect client
   - Consider adjusting AP power levels
4. **Physical survey**: If possible, verify physical obstructions
   - Recent construction, furniture moves, metal equipment installation

#### Step 4: Good Signal but Poor Performance

**Possible causes:**

1. **Channel congestion**: Too many clients or neighboring networks
2. **Interference**: Non-WiFi devices causing noise
3. **Client capabilities**: Old device with limited WiFi standards
4. **Bandwidth constraints**: Network/internet congestion
5. **Application-specific issues**: QoS, firewall, routing problems

**Resolution steps:**

1. **Check channel utilization** on controller
   - High utilization (>50%): Consider channel changes or additional APs
2. **Review client capabilities**:
   - Check WiFi standard (n/ac/ax)
   - Check supported bands (2.4 GHz only vs dual-band)
   - Check negotiated data rates
3. **Test with different application**:
   - Web browsing slow but streaming works: Possible DNS or routing issue
   - Everything slow: Likely RF or bandwidth issue
4. **Check AP client count**: Is AP overloaded?
   - Typical threshold: 25-50 clients per AP depending on usage
5. **Review QoS policies**: Ensure traffic isn't being deprioritized

#### Step 5: Low SNR (Below 15 dB)

**Indicates interference - not just weak signal:**

**Resolution steps:**

1. **Check channel utilization and interference metrics** on controller
2. **Identify interference sources**:
   - Check for neighboring APs on same/overlapping channels
   - Ask user about nearby devices (microwave, Bluetooth speakers, wireless cameras)
   - Check for DFS radar events if using 5 GHz DFS channels
3. **Consider channel change**:
   - Move to less congested channel
   - Use auto-channel selection feature if available
   - For 2.4 GHz: Use only channels 1, 6, or 11
4. **Adjust AP transmit power** if needed:
   - Too high power can cause co-channel interference
   - Auto power adjustment usually optimal

#### Step 6: Authentication Failures

**Client cannot connect at all:**

**Resolution steps:**

1. **Check authentication logs**:
   - Controller authentication logs
   - RADIUS server logs (for Enterprise networks)
2. **For Enterprise (802.1X) networks**:
   - Verify user account is active
   - Check user group memberships
   - Verify RADIUS server reachability
   - Check certificate validity (both user and CA certificates)
   - Test with known-good credentials
3. **For PSK (Personal) networks**:
   - Verify correct password
   - Check for special characters that might be misinterpreted
   - Try removing and re-adding network profile on client
4. **Check VLAN assignment**:
   - Verify user role maps to correct VLAN
   - Ensure VLAN exists and is properly configured

#### Step 7: Intermittent Disconnections

**Client connects but drops frequently:**

**Resolution steps:**

1. **Review client roaming behavior**:
   - Check association history - is client roaming excessively?
   - Review roaming aggressiveness setting on client
   - Check for 802.11k/r/v support and configuration
2. **Check for controller/AP issues**:
   - Review CAPWAP tunnel stability
   - Check for AP reboots or controller failovers
   - Monitor AP CPU and memory utilization
3. **Review RF environment changes**:
   - Recent interference sources introduced?
   - Neighboring network changes?
   - Physical environment changes?
4. **Analyze deauth reasons**:
   - Check controller logs for deauthentication reason codes
   - Common codes:
     - Code 1: Unspecified (client initiated)
     - Code 2: Previous authentication no longer valid
     - Code 3: Client leaving/roaming
     - Code 4: Inactivity timeout

#### Step 8: Layer 3 Connectivity Issues

**Client connected to WiFi but no network access:**

**Resolution steps:**

1. **Check DHCP**:
   - Verify client received IP address
   - Check IP address is in correct subnet
   - Verify default gateway and DNS servers assigned
   - Test DHCP server reachability from VLAN
2. **Test connectivity**:
   - Can client ping default gateway?
   - Can client ping external IP (e.g., 8.8.8.8)?
   - Can client resolve DNS names?
3. **Check firewall rules**:
   - Review firewall logs for blocked traffic
   - Verify correct security policies applied to VLAN
4. **Check client firewall/security software**:
   - Corporate security software blocking traffic?
   - Personal firewall too restrictive?

### Advanced Troubleshooting

**If basic steps don't resolve the issue:**

1. **Packet capture**: Capture wireless frames to analyze:
   - Authentication sequences
   - Deauthentication causes
   - Roaming behavior
   - Data transmission patterns
2. **Client-side diagnostics**:
   - Use OS-specific WiFi diagnostic tools
   - Check client WiFi driver version and update if needed
   - Review client system logs during connection attempts
3. **RF spectrum analysis**:
   - Use spectrum analyzer to identify non-WiFi interference
   - Identify rogue APs or unauthorized devices
4. **Controller debug logs**:
   - Enable debug logging for specific client MAC
   - Review detailed connection/disconnection events
5. **Compare with working client**:
   - Test with known-good device in same location
   - If known-good device works, issue likely client-specific

### Escalation Criteria

**Engage vendor support when:**

1. Controller or AP hardware appears faulty
2. CAPWAP tunnel issues persist despite basic troubleshooting
3. Suspected firmware bugs or need for software upgrades
4. Advanced RF analysis required beyond basic tools
5. Configuration changes requiring vendor approval or best practices guidance
6. Multiple clients affected suggesting infrastructure-wide issue

### Documentation

**Always document:**

- Symptoms reported and when they started
- Troubleshooting steps performed and results
- Current client metrics (RSSI, SNR, AP, VLAN, etc.)
- Any changes made (configuration, reboots, etc.)
- Resolution or current status
- Ticket numbers for related issues or vendor cases
