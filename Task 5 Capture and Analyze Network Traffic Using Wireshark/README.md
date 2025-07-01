# Task 5: Capture and Analyze Network Traffic Using Wireshark

This report details the process and findings of capturing and analyzing network traffic as part of the Cyber Security Internship task.

**Objective:** To capture live network packets using Wireshark and identify basic protocols and traffic types.

**Tools Used:**
*   Wireshark

---

## Identified Hosts

| IP Address | MAC Address | Vendor / Name | Role in Capture |
| :--- | :--- | :--- | :--- |
| **`192.168.1.5`** | `08:00:27:d1:f8:5d` | PCSSystemtec | **Attacker / Scanner** |
| **`192.168.1.4`** | `08:00:27:c1:cf:f6` | PCSSystemtec / METASPLOITABLE | **Target** |
| `192.168.1.1` | `52:54:00:12:35:00` | (Unknown) | **Gateway / Router** |
| `8.8.8.8` | (N/A) | Google | **Public DNS Server** |
| `192.168.1.3` | `08:00:27:40:c2:1f` | PCSSystemtec | **DHCP Server** |

## Timeline and Narrative of Events

The capture file details a logical sequence of reconnaissance performed by the attacker (`192.168.1.5`).

1.  **Initial Discovery (Frame 1):** The capture begins with the target machine (`192.168.1.4`) broadcasting a "Host Announcement" via the BROWSER protocol. It explicitly names itself "METASPLOITABLE," advertising its services.

2.  **Address Resolution (Frames 2-3, repeated):** Before sending any targeted packets, the attacker at `192.168.1.5` frequently sends ARP "Who has 192.168.1.4?" requests to find the target's MAC address. The target consistently replies with "192.168.1.4 is at 08:00:27:c1:cf:f6." This ARP resolution is a prerequisite for direct communication on the local network.

3.  **Information Gathering (Frames 6-7, repeated):** The attacker attempts to perform a reverse DNS lookup for the target's IP address by sending a query for `4.1.168.192.in-addr.arpa` to Google's DNS server (`8.8.8.8`). This is an attempt to find a hostname associated with the IP. The DNS server replies with "No such name," indicating the lookup failed.

4.  **Systematic Port Scanning (Frames 10-145):** The core of the activity is a series of TCP scans directed at port 80 of the target machine. The attacker cycles through different scan types to probe the port's state.

---
### TCP Port Scan Analysis

The attacker uses multiple Nmap-style scan techniques to determine the state of port 80 on the target.

#### 1. NULL Scan
*   **Packet:** Frame 10 (`192.168.1.5 → 192.168.1.4 TCP 49401 → 80 [<None>]`)
*   **Technique:** A TCP packet is sent with *no flags* set. According to RFC 793, a host receiving such a packet on a closed port should respond with a `RST` packet. If the port is open, it should be ignored.
*   **Observation:** The log does not show an immediate `RST` response from the target, suggesting the port is likely `open|filtered`.

#### 2. XMAS Scan
*   **Packet:** Frame 17 (`192.168.1.5 → 192.168.1.4 TCP 54732 → 80 [FIN, PSH, URG]`)
*   **Technique:** A TCP packet is sent with the FIN, PSH, and URG flags set ("lit up like a Christmas tree"). The logic is identical to a NULL scan.
*   **Observation:** Similar to the NULL scan, the target does not respond with a `RST`, suggesting the port is `open|filtered`.

#### 3. ACK Scan
*   **Packet Exchange:**
    *   Frame 23: `192.168.1.5 → 192.168.1.4 TCP 58774 → 80 [ACK]`
    *   Frame 24: `192.168.1.4 → 192.168.1.5 TCP 80 → 58774 [RST]`
*   **Technique:** An ACK packet is sent to a port. If the packet reaches the host and the port is not blocked by a firewall, the host's kernel will respond with a `RST` because the ACK packet is not part of an established connection.
*   **Observation:** The target responds with a `RST`. This tells the attacker that the port is **`unfiltered`**, meaning it is reachable and not blocked by a stateful firewall. It does not, however, confirm if the port is open or closed.

#### 4. FIN Scan
*   **Packet:** Frame 42 (`192.168.1.5 → 192.168.1.4 TCP 62878 → 80 [FIN]`)
*   **Technique:** A TCP packet is sent with only the FIN flag set. The logic is identical to NULL and XMAS scans.
*   **Observation:** The target does not respond with a `RST`, again suggesting the port is `open|filtered`.

#### 5. TCP Connect Scan (SYN Scan)
*   **Packet Exchange (The 3-Way Handshake):**
    *   Frame 27: `192.168.1.5 → 192.168.1.4 TCP 35152 → 80 [SYN]`
    *   Frame 28: `192.168.1.4 → 192.168.1.5 TCP 80 → 35152 [SYN, ACK]`
    *   Frame 29: `192.168.1.5 → 192.168.1.4 TCP 35152 → 80 [ACK]`
*   **Technique:** This is a standard attempt to open a full TCP connection.
*   **Observation:** The attacker sends a `SYN` packet, and the target responds with a `SYN, ACK`, indicating it is willing to open a connection. The attacker completes the handshake with an `ACK`. **This is definitive proof that port 80 is `open` on the target machine.** The attacker immediately sends a `RST, ACK` (Frame 30) to tear down the connection.

###  Other Protocols

*   **ARP (Address Resolution Protocol):** Used heavily by the attacker to resolve the target's MAC address before each scan attempt. This is normal and necessary for local network communication.
*   **DNS (Domain Name System):** The attacker repeatedly attempts reverse DNS lookups. This shows a methodical approach to information gathering.
*   **DHCP (Dynamic Host Configuration Protocol):** Frames 111-112 and 148-149 show DHCP request/acknowledgment cycles between hosts `192.168.1.4` and `192.168.1.3`. This appears to be background network activity unrelated to the primary scan.
*   **ICMPv6 (Internet Control Message Protocol v6):** Frame 12 shows a "Router Solicitation," which is standard behavior for a host on an IPv6-enabled network trying to find local routers.
---
