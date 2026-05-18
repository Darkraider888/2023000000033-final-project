# Active Reconnaissance Summary

## Tasks Completed
- Completed all 7 tasks in TryHackMe “Active Reconnaissance” room (score 100%).
- Used tools: `ping`, `traceroute`, `telnet`, `netcat`, and browser developer tools.

## Tools Used
| Tool         | Purpose                                      |
|--------------|----------------------------------------------|
| `ping`       | Check host reachability and measure RTT      |
| `traceroute` | Map network hops to target                   |
| `telnet`     | Manual banner grabbing and service interaction |
| `netcat`     | Port scanning, banner grabbing, simple shells |
| Web Browser  | View HTTP headers, inspect page source       |

## Key Findings
- **ICMP Echo requests** revealed live hosts but can be blocked by firewalls.
- **Traceroute** exposes internal router IPs and network topology.
- **Telnet** to open ports (e.g., 80, 25) can leak service banners and software versions.
- **Netcat** allows fast banner grabbing; e.g., `nc target 80` returned `HTTP/1.1 200 OK` with server header.

## Security Impact
- Attackers can map network infrastructure and identify outdated services.
- Banner information (Apache/2.4.18, OpenSSH 7.2p2) helps target known vulnerabilities.
- Unfiltered ICMP and open `telnet` ports increase reconnaissance surface.

## Remediation Recommendations
- Block inbound ICMP echo requests unless strictly needed.
- Disable unnecessary services (e.g., `telnet` – replace with SSH).
- Filter outbound traceroute probes at network perimeter.
- Remove or obfuscate service banners (e.g., `ServerTokens Prod` in Apache).
- Implement port knocking or a firewall to limit scan visibility.
