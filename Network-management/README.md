# 🌐 Linux Network Management

## What is Network Management?

Network management is the process of monitoring, configuring, maintaining, and securing computer networks to ensure reliable communication between devices. It helps administrators keep networks stable, efficient, and available while quickly identifying and resolving issues.

Network management helps administrators:

- Configure network devices
- Monitor network performance
- Troubleshoot connectivity issues
- Secure network communication
- Optimize bandwidth usage
- Maintain high network availability

💡 Why it matters: Every modern system relies on networking. Whether you're accessing a website, connecting to a remote server, or transferring files, network management ensures data reaches its destination securely and efficiently.

## 🧩 Basic Network Components

Every network consists of essential components that work together.

1.Host – Any device connected to the network (computer, server, phone).
2.IP Address – Unique numerical address assigned to a device.
3.MAC Address – Physical hardware address of a network interface.
4.Router – Connects different networks and forwards traffic.
5.Switch – Connects devices within the same local network.
6.Gateway – Entry and exit point between networks.
7.DNS Server – Converts domain names into IP addresses.
8.DHCP Server – Automatically assigns IP addresses to devices.
9.Firewall – Filters incoming and outgoing network traffic.

## understanding IP Address

An IP Address (Internet Protocol Address) is a unique logical address assigned to every device connected to a network.

It helps devices locate and communicate with each other.

#### There are two versions:

1.IPv4
- Example:192.168.1.10
- 32-bit address
- Most commonly used

2.IPv6
- Example:2001:db8::10
- 128-bit address
- Supports a much larger address space
- IPv6 was introduced because IPv4 addresses are limited.

### 🏠 Private vs Public IP

1.Private IP-Used inside local networks.

Ranges:

10.0.0.0/8

172.16.0.0 – 172.31.255.255

192.168.0.0/16

2.Public IP-Accessible over the Internet.

Example:

8.8.8.8

### 🔁 Special IP Addresses

| IP Address | Purpose | Example Usage |
|------------|---------|---------------|
| **127.0.0.1** | Loopback (localhost) | Testing a local web server using `http://localhost` or `127.0.0.1`. |
| **0.0.0.0** | Unspecified / All Interfaces | A web server listening on `0.0.0.0:8080` accepts connections from all network interfaces. |
| **255.255.255.255** | Limited Broadcast Address | A DHCP client broadcasts a request to discover a DHCP server on the local network. |
| **169.254.x.x** | APIPA (Automatic Private IP Addressing) | A Windows or Linux system automatically assigns an address like `169.254.10.20` when it cannot obtain an IP address from a DHCP server. |

> 💡 **Note:** These IP addresses are reserved for special networking functions and are **not typically assigned as regular host IP addresses** on a network.

### 🏷️ MAC Address

A MAC (Media Access Control) Address is the physical hardware address of a Network Interface Card (NIC).

Example:

00:1A:2B:3C:4D:5E

Characteristics:

- Physical address
- Assigned by manufacturer
- Unique for every NIC
- Works at Data Link Layer

## 📦 Subnet

A subnet divides a large network into smaller networks.

Benefits:

- Better performance
- Reduced broadcast traffic
- Improved security
- Easier management

Example:

192.168.1.0/24

### 📦 Common CIDR Values

| CIDR | Subnet Mask |
|------|-------------|
| **/8** | 255.0.0.0 |
| **/16** | 255.255.0.0 |
| **/24** | 255.255.255.0 |
| **/32** | 255.255.255.255 |
> 💡**Note:**  CIDR (Classless Inter-Domain Routing) notation defines the network prefix length and determines how many hosts can exist within a subnet.

## 🚪 Default Gateway

A Default Gateway is the router that forwards traffic outside the local network.

Example:

PC
 │
 ▼
Router (Gateway)
 │
 ▼
Internet

Without a gateway, devices can communicate only within the local network.

## 🌐 DNS (Domain Name System)

DNS converts domain names into IP addresses.

### How DNS Works (Step by Step):

1. You type: google.com in browser
                ↓
2. Computer checks: /etc/hosts (local file)
                ↓
3. If not found, asks: DNS server (configured in /etc/resolv.conf)
                ↓
4. DNS server responds: 142.250.185.46
                ↓
5. Browser connects to: 142.250.185.46 on port 443

### 🌐 Public DNS Servers

| Provider | Primary DNS | Secondary DNS | Features |
|----------|-------------|---------------|----------|
| **Google** | 8.8.8.8 | 8.8.4.4 | Fast, reliable, and widely used. |
| **Cloudflare** | 1.1.1.1 | 1.0.0.1 | Privacy-focused with excellent performance. |
| **Quad9** | 9.9.9.9 | 149.112.112.112 | Security-focused; blocks malicious domains. |
| **OpenDNS** | 208.67.222.222 | 208.67.220.220 | Provides content filtering and parental controls. |

> 💡 **Note:**  Public DNS servers can be configured manually when your ISP's DNS is slow, unavailable, or for better performance, privacy, or security.

## 🔌 Ports

A Port is a logical communication endpoint used by applications.

One IP address can have multiple ports.

Example:

192.168.1.10:22

### 🔌 Common Network Ports

| Port | Service | Purpose |
|------|---------|---------|
| **20/21** | FTP | Transfers files between computers. |
| **22** | SSH | Provides secure remote login and administration. |
| **23** | Telnet | Allows remote login (not secure). |
| **25** | SMTP | Sends email between mail servers. |
| **53** | DNS | Resolves domain names to IP addresses. |
| **67/68** | DHCP | Automatically assigns IP addresses to devices. |
| **80** | HTTP | Delivers web pages over the Internet. |
| **110** | POP3 | Retrieves emails from a mail server. |
| **143** | IMAP | Accesses and synchronizes emails on a mail server. |
| **443** | HTTPS | Provides secure and encrypted web communication. |
| **3306** | MySQL | Default port for MySQL database services. |
| **5432** | PostgreSQL | Default port for PostgreSQL database services. |

>💡 **Note:** A port is a logical communication endpoint that allows multiple network services to run simultaneously on the same device.

## 📨Network Protocols

A network protocol is a set of rules that defines how devices communicate and exchange data over a network.

Just as people follow a common language to understand each other, computers use network protocols to send, receive, and process information correctly.

###  Common Network Protocols

| Protocol | Purpose |
|----------|---------|
| **TCP** | Provides reliable and connection-oriented communication. |
| **UDP** | Provides fast, connectionless communication. |
| **HTTP** | Transfers web pages between web servers and browsers. |
| **HTTPS** | Transfers encrypted and secure web traffic. |
| **FTP** | Transfers files between computers over a network. |
| **SSH** | Enables secure remote login and command execution. |
| **DNS** | Translates domain names into IP addresses. |
| **DHCP** | Automatically assigns IP addresses and network settings. |
| **ICMP** | Performs network diagnostics and error reporting (used by `ping`). |
| **ARP** | Maps IP addresses to MAC addresses within a local network. |

> **💡 Note:** Multiple protocols work together during communication. For example, when opening a website, DNS resolves the domain name, TCP establishes the connection, and HTTP/HTTPS transfers the web page to your browser.

## ⚡ TCP vs UDP

TCP and UDP are the two primary transport layer protocols used for data communication. While **TCP** focuses on reliable and accurate data delivery, **UDP** prioritizes speed with minimal overhead.

| Feature | TCP | UDP |
|---------|-----|-----|
| **Connection** | Connection-oriented | Connectionless |
| **Reliability** | Guarantees data delivery | Best-effort delivery |
| **Packet Order** | Delivers packets in sequence | Packets may arrive out of order |
| **Speed** | Slower due to additional checks | Faster with minimal overhead |
| **Error Checking** | Detects and retransmits lost packets | Performs basic error checking only |
| **Header Size** | 20 Bytes | 8 Bytes |
| **Common Uses** | Web browsing, Email, File Transfer | Streaming, Gaming, VoIP, DNS |
| **Examples** | HTTP, HTTPS, SSH, FTP | DNS, DHCP, VoIP, Live Streaming |

### 📌 When to Use TCP

Use **TCP** when data accuracy and reliability are more important than speed.

Suitable for:

- Complete and reliable data delivery
- Ordered packet transmission
- File downloads and uploads
- Web browsing
- Database communication
- Remote server access (SSH)

### 📌 When to Use UDP

Use **UDP** when speed and low latency are more important than guaranteed delivery.

Suitable for:

- Live video and audio streaming
- Online gaming
- Video conferencing
- DNS queries
- Voice over IP (VoIP)
- Real-time applications

> 💡 **Note:** TCP is preferred when **every packet must arrive correctly**, whereas UDP is ideal for **real-time communication**, where occasional packet loss is acceptable in exchange for faster performance.

## 🌐 Network Models

Network communication follows layered models that divide data transmission into separate functions. Each layer has a specific responsibility, making networks easier to design, maintain, and troubleshoot.

The two most common networking models are:

- **OSI Model** – A 7-layer conceptual model used to understand and troubleshoot network communication.
- **TCP/IP Model** – A practical 4-layer model used by modern operating systems, including Linux and the Internet.

> 💡 **Why it matters:** Network models help identify where communication problems occur and explain how data moves between devices.


### 🌐 OSI Model (Open Systems Interconnection)

The **OSI Model** divides network communication into **seven layers**, where each layer performs a specific task and works together to deliver data from one device to another.

#### 📚 OSI Layers

| Layer | Name | Primary Function | Examples |
|------|------|------------------|----------|
| **7** | Application | Provides network services to user applications. | HTTP, HTTPS, FTP, DNS |
| **6** | Presentation | Formats, encrypts, and compresses data. | SSL/TLS, JPEG |
| **5** | Session | Establishes and manages communication sessions. | RPC, NetBIOS |
| **4** | Transport | Ensures reliable data delivery. | TCP, UDP |
| **3** | Network | Handles logical addressing and routing. | IP, ICMP |
| **2** | Data Link | Transfers frames using MAC addresses. | Ethernet, Switches |
| **1** | Physical | Transmits data through physical media. | Cables, Fiber, Wi-Fi |

#### 🔄 OSI Data Flow

```text 
Application
"User requests https://google.com"
      │
      ▼
Presentation
"Data is encrypted using TLS/SSL"
      │
      ▼
Session
"Connection between browser and server is managed"
      │
      ▼
Transport
"TCP breaks data into segments and guarantees delivery"
      │
      ▼
Network
"IP routes packets across networks to Google's server"
      │
      ▼
Data Link
"Ethernet/Wi-Fi uses MAC addresses to reach the next hop"
      │
      ▼
Physical
"Packets travel through cables, fiber optics, or Wi-Fi signals"
```
Data moves **from Layer 7 to Layer 1** when it is sent and **from Layer 1 to Layer 7** when it is received.

### 🌐 TCP/IP Model

The **TCP/IP Model** is the networking model used by Linux and the Internet. It simplifies communication into **four layers**, combining several OSI layers.

#### 📚 TCP/IP Layers

| Layer | Primary Function | Common Protocols |
|------|------------------|------------------|
| **Application** | Provides network services for applications. | HTTP, HTTPS, FTP, SSH, DNS |
| **Transport** | Delivers data between applications. | TCP, UDP |
| **Internet** | Provides IP addressing and packet routing. | IP, ICMP, ARP |
| **Network Access** | Sends data across the physical network. | Ethernet, Wi-Fi |

#### 🔄 TCP/IP Data Flow

```text
Application
"Browser sends an HTTPS request"
      │
      ▼
Transport
"TCP guarantees reliable delivery"
      │
      ▼
Internet
"IP routes packets to the server"
      │
      ▼
Network Access
"Ethernet or Wi-Fi transmits the frames"
```
Linux networking is built on the **TCP/IP Model**, making it the standard model used in modern computer networks.

## 🔄 Basic Network Communication Workflow

```text
User Types: google.com
        │
        ▼
Browser Asks DNS for the IP Address
        │
        ▼
DNS Returns the Server's IP Address
        │
        ▼
Browser Establishes a TCP Connection
        │
        ▼
Connection Uses Port 443 (HTTPS)
        │
        ▼
Encrypted Communication Begins
        │
        ▼
Web Server Sends HTML, CSS, and JavaScript
        │
        ▼
Browser Renders the Website
```
💡 This workflow illustrates how a Linux system communicates with remote servers over a network.

## 🖥️ Essential Network Configuration Commands

``` bash
ip addr                 # Displays all network interfaces and assigned IP addresses.
ip -br addr             # Shows IP addresses in a concise, easy-to-read format.
ip link                 # Lists all network interfaces and their status.
ip route                # Displays the system's routing table.
hostname                # Prints the system hostname.
hostname -I             # Displays all assigned IP addresses.
nmcli device status     # Shows the status of network devices managed by NetworkManager.
cat /etc/hosts          # Displays local hostname-to-IP mappings.
cat /etc/resolv.conf    # Shows the configured DNS servers.
``` 
### 🔍 Connectivity Testing

```bash 
ping google.com             # Tests network connectivity to the remote host.
ping -c 4 google.com        # Sends only four ICMP packets.
ping 8.8.8.8                # Tests Internet connectivity without DNS.
traceroute google.com       # Displays the path packets take to the destination.
tracepath google.com        # Traces the route without requiring root privileges.
mtr google.com              # Continuously monitors latency and packet loss
```
## 🚪 Port & Socket Utilities

### 🔹 `netstat`

**Purpose:** Displays network connections, routing tables, interface statistics, and listening ports. *(Legacy command)*

#### Common Flags

| Flag | Description |
|------|-------------|
| `-t` | Show TCP connections. |
| `-u` | Show UDP connections. |
| `-l` | Display listening ports only. |
| `-n` | Show numeric IP addresses and port numbers. |
| `-p` | Display the process using each socket. |
| `-a` | Show all active and listening connections. |
| `-r` | Display the routing table. |

#### Examples

```bash
netstat -tuln              # Lists all listening TCP and UDP ports.
netstat -tulnp             # Shows listening ports with associated processes.
netstat -an                # Displays all active network connections.
netstat -rn                # Shows the system routing table.
```
### 🔹 `ss`

**Purpose:** Displays network sockets and connections. It is the modern replacement for `netstat`.

#### Common Flags

| Flag | Description |
|------|-------------|
| `-t` | Show TCP connections. |
| `-u` | Show UDP connections. |
| `-l` | Display listening sockets only. |
| `-n` | Show numeric IP addresses and port numbers. |
| `-p` | Display the process using each socket. |
| `-a` | Show all sockets. |
| `-s` | Display a summary of socket statistics. |

#### Examples

```bash
ss -tuln                  # Lists all listening TCP and UDP ports.
ss -tulnp                 # Shows listening ports with associated processes.
ss -p                     # Displays processes using network sockets.
ss -s                     # Displays socket usage statistics.
```
### 🔹 `lsof -i`

**Purpose:** Lists processes that are using network ports or active network connections.

#### Common Flags

| Flag | Description |
|------|-------------|
| `:PORT` | Show the process using a specific port. |
| `TCP` | Display TCP connections only. |
| `UDP` | Display UDP connections only. |
| `-n` | Show numeric IP addresses. |
| `-P` | Show numeric port numbers. |

#### Examples

```bash
lsof -i                   # Lists all network-related open files.
lsof -i :22               # Shows the process using port 22.
lsof -i TCP               # Displays all TCP connections.
lsof -i UDP               # Displays all UDP connections.
lsof -i -nP               # Shows numeric IP addresses and port numbers.
```
### 🔹 `telnet`

**Purpose:** Tests connectivity to a remote TCP port.

#### Syntax

```bash
telnet <hostname> <port>
```
#### Examples

```bash
telnet google.com 80      # Tests connectivity to port 80.
telnet 192.168.1.10 22    # Tests connectivity to the SSH port.
```
> 💡 **Result:** If the connection succeeds, the port is open and reachable. If it fails, the service may not be running, the port may be blocked by a firewall, or the host may be unreachable.

## 📊 Network Monitoring

```bash
ip -s link                  # Displays network interface statistics, including transmitted and received packets.
ip monitor                  # Monitors real-time network configuration changes.
iftop                       # Displays real-time bandwidth usage by network connection.
nload                       # Monitors incoming and outgoing network traffic.
vnstat                      # Displays historical network traffic statistics.
sar -n DEV                  # Shows network interface utilization statistics.
sar -n TCP                  # Displays TCP connection statistics.
sar -n UDP                  # Displays UDP traffic statistics.
tcpdump -i eth0             # Captures and analyzes packets on the specified network interface.
tcpdump -i any              # Captures packets on all available network interfaces.
ethtool eth0                # Displays Ethernet interface information and link status.
watch -n 2 ip -s link       # Refreshes interface statistics every two seconds.
```
## 🌍 DNS Troubleshooting

```bash
dig google.com              # Performs a detailed DNS lookup.
dig +short google.com       # Displays only the resolved IP address.
nslookup google.com         # Queries DNS records.
host google.com             # Performs a simple DNS lookup.
cat /etc/resolv.conf        # Displays configured DNS servers.
cat /etc/hosts              # Shows local hostname mappings.
resolvectl status           # Displays DNS resolver configuration.
```
## 🌐 Web & HTTP Testing

```bash
curl http://example.com              # Retrieves the content of a web page.
curl -I http://example.com           # Displays only the HTTP response headers.
curl -X POST -d "name=John" http://example.com/api   # Sends an HTTP POST request with data.
curl -L http://example.com           # Follows HTTP redirects automatically.
curl -o file.html http://example.com # Saves the response to a local file.

wget http://example.com/file.zip     # Downloads a file from a remote server.
wget --spider http://example.com     # Checks whether a URL is reachable without downloading it.
wget -O index.html http://example.com # Downloads and saves the file with a custom name.
wget -r http://example.com           # Recursively downloads a website.
```