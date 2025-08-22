# Access List Commands

## Show Commands
```
show policy
show policy network group
show policy condition
show policy rule
```

## Create Services
```
policy service srcTCPport_53 source tcp port 53
policy service srcTCPport_123 source tcp port 123
!
policy service srcUDPport_53 source udp port 53
policy service srcUDPport_67 source udp port 67
policy service srcUDPport_68 source udp port 68
policy service srcUDPport_123 source udp port 123
```

## Destination Ports
```
policy service destTCPport_53 destination tcp port 53
policy service destTCPport_123 destination tcp port 123
!
policy service destUDPport_53 destination udp port 53
policy service destUDPport_67 destination udp port 67
policy service destUDPport_68 destination udp port 68
policy service destUDPport_123 destination udp port 123
```

## Create Service Groups
> [!TIP]
> policy service group <group_name> <service_to_be_added_to_group> <service_to_be_added_to_group> <etc...>

```
policy service group srcTCPports srcTCPport_53 srcTCPport_123
policy service group srcUDPports srcUDPPport_53 srcUDPport_67 srcUDPport_68 srcUDPport_123
!
policy service group destTCPports destTCPport_53 destTCPport_123
policy service group destUDPports destUDPport_53 destUDPport_67 destUDPport_68 destUDPport_123
```

### Create Network Groups
#### Common Network Groups (Private IP Ranges)
```
policy network group AnyIPnetwork 0.0.0.0
policy network group PrivateIPnetworks 10.0.0.0 mask 255.0.0.0 172.16.0.0 mask 255.240.0.0 192.168.0.0 mask 255.255.0.0
```

#### Other Network Groups
> [!TIP]
> policy network group <group_name> [<ip_address> | <ip_network> mask <subnet_mask>]
```
policy network group guestNetworks 172.31.255.15 10.5.0.0 mask 255.255.0.0 172.19.200.0 mask 255.255.255.0
policy network group guestNetworks_src 172.31.255.15 10.5.0.0 mask 255.255.0.0 172.19.200.0 mask 255.255.255.0
policy network group guestNetworks_dest 172.31.255.15 10.5.0.0 mask 255.255.0.0 172.19.200.0 mask 255.255.255.0
!
policy network group vlan999 172.16.99.0 mask 255.255.255.0
polciy network group vlan999_src 172.16.99.0 mask 255.255.255.0
policy network group vlan999_dest 172.16.99.0 mask 255.255.255.0
```

### Create Conditions
> [!TIP]
> policy condition <condition_name> <source/destination> <network group/service group> <group_name> <source/destination> <network group/service group> <group_name>
```
policy condition allowAny_src source ip Any destination ip Any
!
policy condition allowTCP_dst destination network group guestNetworks service group srcTCPports
policy condition allowTCP_src source network group guestNetworks service group destTCPports
policy condition allowUDP_dst destination network group guestNetworks service group srcUDPports
policy condition allowUDP_src source network group guestNetworks service group destUDPports
!
policy condition allowVlan999_src source network group vlan999_src destination network group vlan999_dest
policy condition allowVlan999_dest source network group vlan999_dest destination network group vlan999_src
!
policy condition denyVlan999_dest source network group PrivateIPnetworks destination network group vlan999
policy condition denyVlan999_src source network group vlan999 destination network group PrivateIPnetworks
```

### Create Actions
```
policy action Allow
policy action Block disposition deny
```

### Create Rules
> [!TIP]
> policy rule <rule_name> precedence <precedence_value> condition <condition_name> action Allow/Block<br/>
> precedence ranked highest number to lowest (90 greater precedence than 80)

```
policy rule allowTCP_source precedence 90 condition allowTCP_src action Allow
policy rule allowTCP_destination precedence 90 condition allowTCP_dst action Allow
!
policy rule allowUDP_source precedence 90 condition allowUDP_src action Allow
policy rule allowUDP_destination precedence 90 condition allowUDP_dest action Allow
!
policy rule allowVLAN999_src precedence 80 condition allowVlan999_src action Allow
policy rule allowVLAN999_dest precedence 80 condition allowVlan999_dest action Allow
!
policy rule denyVLAN999_src precedence 60 condition denyVlan99_src action Block
policy rule denyVLAN999_dest precedence 60 condition denyVlan999_dest action Block
!
policy rule allowAny condition allowAny_src action Allow
```

### QOS Apply
> [!IMPORTANT]
> The `qos apply` command must be run to see any changes in the qos policy and run every time changes are made.
```
qos apply
```
