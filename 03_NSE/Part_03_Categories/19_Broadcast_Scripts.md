# Chapter 19 — Broadcast Scripts

The **broadcast** category contains NSE scripts that discover network information by sending broadcast or multicast requests across the local network.

Unlike most NSE scripts, which communicate directly with a specific target host, broadcast scripts communicate with an entire network segment. They are designed to identify devices, services, protocols, and network infrastructure that respond to broadcast or multicast traffic.

Broadcast scripts are especially valuable during internal network assessments, asset discovery, and network administration. Since broadcast traffic is generally not routed across networks, these scripts are primarily useful within the same local area network (LAN).

---

## What Are Broadcast Scripts?

Broadcast scripts use network broadcast or multicast protocols to discover information from multiple hosts simultaneously.

Instead of scanning individual IP addresses, these scripts send a single request that may be answered by many devices.

Typical objectives include:

- Discovering active hosts
- Identifying network devices
- Enumerating printers
- Finding DHCP servers
- Detecting multicast services
- Discovering file shares
- Identifying media devices
- Locating industrial control devices

Broadcast scripts provide rapid visibility into a local network without scanning every address individually.

---

## Executing Broadcast Scripts

Execute all broadcast scripts:

```bash
nmap --script broadcast
```

Run together with service detection:

```bash
nmap -sV --script broadcast
```

Execute a specific broadcast script:

```bash
nmap --script broadcast-dhcp-discover
```

Another example:

```bash
nmap --script broadcast-ping
```

Because broadcast scripts target the local network rather than a specific host, some do not require a target IP address.

---

## How Broadcast Scripts Work

The workflow differs from traditional host-based scanning.

```text
Broadcast Script
        │
        ▼
Create Broadcast Packet
        │
        ▼
Send to Local Network
        │
        ▼
Multiple Devices Receive Packet
        │
        ▼
Devices Respond
        │
        ▼
Collect Responses
        │
        ▼
Generate Report
```

A single broadcast request may generate responses from dozens or even hundreds of devices.

---

## Broadcast vs Multicast

Although often grouped together, broadcast and multicast are different networking concepts.

| Broadcast | Multicast |
|------------|-----------|
| Sent to every device on the local network | Sent only to subscribed devices |
| Higher network traffic | More efficient communication |
| Uses broadcast address | Uses multicast address |
| Supported by most LAN protocols | Requires multicast-capable protocols |

Many NSE broadcast scripts support one or both communication methods depending on the protocol.

---

## Common Broadcast Scripts

Examples of official broadcast scripts include:

| Script | Purpose |
|---------|---------|
| broadcast-ping | Discovers active hosts |
| broadcast-dhcp-discover | Identifies DHCP servers |
| broadcast-dns-service-discovery | Discovers DNS-SD services |
| broadcast-netbios-master-browser | Finds Windows master browsers |
| broadcast-avahi-dos | Tests Avahi service behavior |
| broadcast-upnp-info | Discovers UPnP devices |
| broadcast-wpad-discover | Detects WPAD configuration servers |

Each script focuses on a different network discovery protocol.

---

## Example Scan

Discover DHCP servers on the local network.

```bash
nmap --script broadcast-dhcp-discover
```

Example output:

```text
Pre-scan script results:

| broadcast-dhcp-discover:
|   Response 1 of 1:
|     DHCP Server Identifier: 192.168.1.1
|     IP Address Lease Time: 86400
|     Router: 192.168.1.1
|     DNS Server: 192.168.1.1
|_    Domain Name: example.local
```

Unlike traditional scans, the information is collected before host scanning begins.

---

## Information Gathered

Broadcast scripts may discover:

- DHCP servers
- DNS services
- Routers
- Network printers
- NAS devices
- Smart TVs
- IP cameras
- Industrial controllers
- Windows systems
- Media servers
- IoT devices

This information helps build an accurate inventory of network assets.

---

## Advantages

Broadcast scripts provide several important benefits.

| Benefit | Description |
|---------|-------------|
| Fast Asset Discovery | Identifies many devices with minimal traffic |
| Local Network Awareness | Reveals infrastructure not easily detected otherwise |
| Automated Enumeration | Reduces manual discovery work |
| Infrastructure Visibility | Discovers network services automatically |
| Efficient Reconnaissance | Collects information quickly |

These advantages make broadcast scripts especially useful during internal assessments.

---

## Limitations

Broadcast scripts also have important limitations.

They generally:

- Work only on local networks
- Cannot cross routers
- Depend on broadcast-enabled protocols
- May be blocked by network policies
- Require compatible devices
- Produce different results on segmented networks

As a result, they are not suitable for scanning Internet hosts.

---

## Operational Considerations

Although broadcast scripts are generally considered low risk, they may:

- Generate noticeable network traffic
- Trigger monitoring systems
- Produce numerous responses
- Increase traffic on busy LANs
- Reveal the presence of the scanning system

Network administrators should understand these effects before large-scale execution.

---

## Best Practices

When using broadcast scripts:

- Execute them only on authorized networks.
- Understand local network topology.
- Record discovered infrastructure.
- Verify unexpected devices manually.
- Avoid unnecessary repeated execution.
- Combine results with traditional host scanning.

These practices improve both accuracy and efficiency.

---

## Real-World Use Cases

Broadcast scripts are commonly used for:

- Internal penetration testing
- Asset discovery
- Network inventory
- Infrastructure documentation
- Blue team operations
- Security audits
- Network troubleshooting
- Device discovery before vulnerability assessments

Because they rapidly identify network infrastructure, broadcast scripts are often executed during the earliest stages of an internal assessment.

---

## Broadcast Scripts vs Traditional Port Scanning

Although both techniques discover network information, they operate differently.

| Broadcast Scripts | Traditional Port Scanning |
|-------------------|---------------------------|
| Query the entire local network | Scan one host at a time |
| Discover infrastructure automatically | Identify open ports |
| Protocol-based discovery | Port-based discovery |
| LAN-focused | Works across routed networks |

Together, they provide a more complete understanding of the target environment.

---

## Chapter Summary

The **broadcast** category contains NSE scripts that use broadcast and multicast protocols to discover devices, infrastructure, and services on local networks.

Rather than scanning individual hosts sequentially, these scripts communicate with entire network segments, making them highly effective for asset discovery, infrastructure mapping, and internal reconnaissance.

Because broadcast traffic generally remains within the local network, these scripts are best suited for authorized internal security assessments and network administration tasks.

---

# Next Chapter

## Chapter 20 — Fuzzer Scripts