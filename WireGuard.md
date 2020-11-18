## WireGuard

### macOS

1. [Install from Apple Store](https://itunes.apple.com/us/app/wireguard/id1451685025?ls=1&mt=12)

2. Add empty tunnel

3. Configure tunnel:

__On-Demand__: Always on, when for example all traffic shall be routed via VPN or AllowedIPs are configured for specific networks/IPs. When off, you activate WireGuard tunnels each time you want to use them.

```ini
[Interface]
PrivateKey = private-key-this-machine
Address = 10.1.1.3/24   # VPN IP and subnet of your machine

[Peer]
PublicKey = public-key-remote-machine
AllowedIPs = 10.1.1.0/24  # VPN network/IP on server, expected traffic from these IPs
Endpoint = ip:port  # real WAN IP and VPN port of remote machine

```

Here, the [Peer] config describes the server. These values come from the WireGuard setup process on your Hetzner machine, probably done by your IT expert.

__AllowedIPs__:
- describes an IP or Network segment:

    - You connect to only one machine, enter the IP with a subnet mask of 32 (`10.1.1.6/32`)
    - You connect to a network segment, enter the network mask accordingly (`10.1.0.0/16`)
    - Everything goes through the VPN (`0.0.0.0/0, ::0/0`)

- has 2 meanings:
    - traffic to this IP/Network will be routed through this VPN connection
    - traffic from this IP/Network is expected
