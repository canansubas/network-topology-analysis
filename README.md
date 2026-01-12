# Network Topology Analysis – Home Lab

## Description
This project documents the network topology of a home lab environment created for security testing and learning purposes.

## Environment
- Internet Connection: VDSL (dedicated lab line)
- Modem: [TP-LINK VC220-G3u]
- OS: Kali Linux
- Network Type: NAT / DHCP
- Virtualization: VirtualBox (NAT Network)

## Network Configuration
- Modem IP: 192.168.1.1
- Kali IP: 10.0.2.5 (VirtualBox NAT)
- Default Gateway: 10.0.2.1 (VirtualBox NAT Gateway)
- DNS Server: 192.168.1.1

## Topology Diagram
Internet (VDSL)
	|
[VDSL Modem]
 192.168.1.1
	|
[Host Machine]
192.168.1.x
	|
[VirtualBox NAT]
10.0.2.1
	|
[Kali Linux]
10.0.2.5

## Commands Used

### Network Configuration
```bash
ip a
ip route
cat /etc/resolv.conf
```
Used to identify IP addressing, default gateway, and DNS configuration.

### Traffic Capture
```bash
sudo tcpdump -i eth1
sudo tcpdump -i eth1 -n
```
Captured live network traffic and displayed IP addresses instead of resolving hostnames.

### Protocol-Specific Filtering
```bash
sudo tcpdump -i eth1 port 53
sudo tcpdump -i eth1 port 80
sudo tcpdump -i eth1 port 443
```
Filtered DNS, HTTP, and HTTPS traffic to analyze protocol behavior and connection patterns.

## Traffic Analysis Findings

### HTTPS over TCP
Observed standard HTTPS traffic using TCP with PSH and ACK flags, indicating encrypted application data transfer after successful session establishment.

### Multiple DNS Queries
Multiple DNS queries were observed before HTTPS connections, which is expected behavior in modern web applications due to external resources such as CDNs and third-party services.

### HTTPS over UDP (QUIC / HTTP/3)
Detected UDP traffic on port 443 to Google IP addresses (216.58.212.2), which indicates the use of QUIC (HTTP/3). This protocol improves performance by reducing latency and connection setup time.

## Security Perspective
Understanding live network traffic is critical for detecting anomalies, misconfigurations, and potential attacks. 
By analyzing DNS queries, HTTPS traffic, and modern protocols such as QUIC, security analysts can better understand normal behavior and identify suspicious patterns.

## Why This Matters
This lab demonstrates foundational skills required for roles in network security and penetration testing, including traffic inspection, protocol awareness, and secure lab documentation.
