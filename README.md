# 5-wireshark

## Goal
Create separate packet captures showing exactly 4 ICMP echo requests and 4 echo replies for each target.
  - `google.pcapng` – ICMP capture for **google.com**
  - `gateway.pcapng` – ICMP capture for the **default gateway**
  - `localhost.pcapng` – ICMP capture for **127.0.0.1 (localhost)**
    
## Gateway IP Address
**192.168.1.1**

## Performance Observations

| Target | Target Type | Round-Trip Time (RTT) / Status |
|--------|-------------|--------------------------------|
| **google.com** | External WAN |  Average ~20ms |
| **Gateway IP** | Local Router/Hop | Average ~3ms |
| **127.0.0.1** | Localhost (Loopback) | Average <0.05ms |


### Observations
* **Fastest Target:** `127.0.0.1` (Localhost). This had the fastest response time because the traffic never leaves the local network stack/CPU, eliminating physical or virtual network latency.
* **Slowest:** google.com. This is expected because the packets had to travel across the physical internet to a remote server and back.
* **In between:** Gateway IP. This target was significantly faster than `google.com` because it is the local network router. The ICMP packets only had to travel a single hop over the local network layer (LAN) rather than routing out across the public internet WAN, resulting in near-instantaneous echo replies.
