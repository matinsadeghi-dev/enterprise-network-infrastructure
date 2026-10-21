# Routing between LANs

The two router interfaces on the transit network are:

- Router 1 Fa0/0: `192.10.170.18/30`
- Router 2 Fa0/0: `192.10.170.17/30`

The transit network is `192.10.170.16/30` with mask `255.255.255.252`.

## Example interface commands

Only use these if they match the existing configuration. Check interface names and existing settings before pasting.

### Router 1

```text
enable
configure terminal
interface fastEthernet 0/1
 description LAN_1
 ip address 10.0.0.1 255.255.255.0
 no shutdown
 exit
interface fastEthernet 0/0
 description LINK_TO_ROUTER_2
 ip address 192.10.170.18 255.255.255.252
 no shutdown
 exit
end
show ip interface brief
```

`10.0.0.1` is an assumed LAN 1 gateway; verify it first.

### Router 2

```text
enable
configure terminal
interface fastEthernet 0/1
 description LAN_2
 ip address 192.10.170.1 255.255.255.240
 no shutdown
 exit
interface fastEthernet 0/0
 description LINK_TO_ROUTER_1
 ip address 192.10.170.17 255.255.255.252
 no shutdown
 exit
end
show ip interface brief
```

## Example static routes

If using static routing and no existing routing protocol provides the routes:

**Router 1 — route to LAN 2**

```text
ip route 192.10.170.0 255.255.255.240 192.10.170.17
```

**Router 2 — route to LAN 1**

```text
ip route 10.0.0.0 255.255.255.0 192.10.170.18
```

Verify with:

```text
show ip route
show running-config
```

Do not configure static routes if a routing protocol already provides equivalent routes. Both directions need valid reachability for return traffic. If the Web Server and DNS server are in LAN 1, clients in LAN 2 need routes to LAN 1 and a working DNS configuration.
