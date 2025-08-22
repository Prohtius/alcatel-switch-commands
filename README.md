# Alcatel Switch Commands

<details>
    <summary>Clear Certified Mode</summary>

`copy certified working make-running-directory`
</details>

<details>
    <summary>Save Commands</summary>
    
### Pre ver. 8 (OS6450 models)
```
copy running-config working
copy working certified
write memory flash-synchro
```
### Ver 8+ (OS6900, OS6360, OS6560, OS6860 models)
```
copy running certified
copy certified working
write memory flash-synchro
```
</details>

<details>
    <summary>DHCP Relay Commands</summary>
    
## DHCP Relay (ver 8+)
```
ip dhcp relay interface <interface name> destination <dhcp server ip address>
```
</details>

<details>
    <summary>Port Troubleshooting Commands</summary>
    
## Show/Clear Port Security Violations
```show port-security violation``` or ```show port-security shutdown```

### To Clear Violations and make changes (ver 8+)
- [ ] disable port to prevent immediate violation status ```interfaces <slot/port> admin-state disable```
- [ ] clear violations ```interfaces <slot/port> clear-violation-all```
- [ ] make changes
- [ ] enable port ```interfaces <slot/port> admin-state enable```

### Spantree Blocking
`show spantree ports blocking`
</details>


<details>
    <summary>Enable/Disable Multicast</summary>

## Multicast Commands    
```
ip multicast status [enable | disable]
ip multicast querying [enable | disable]
!
ip multicast querier-forwarding [enable | disable]
ip multicast vlan 100 status [enable | disable]
ip multicast vlan 702 status [enable | disable]
ip multicast vlan 998 status [enable | disable]
ip multicast vlan 100 querier-forwarding [enable | disable]
ip multicast vlan 702 querier-forwarding [enable | disable]
ip multicast vlan 998 querier-forwarding [enable | disable]
```
</details>

<details>
    <summary>Link Aggregation Commands</summary>

### Create Link Agg
#### lacp (dynamic) [2 linkagg with 2 ports]
```
    lacp linkagg 1 size 2 name "<name>" admin state enable
    lacp linkagg 2 size 2 name "<name>" admin state enable

    lacp linkagg 1 actor admin key 1
    lacp linkagg 2 actor admin key 2

    lacp agg 1/4 actor admin key 1
    lacp agg 1/5 actor admin key 1
    lacp agg 1/19 actor admin key 2
    lacp agg 1/20 actor admin key 2    

    vlan <vlan> port default 1
    vlan <vlan> port default 2
```
#### static
```
static linkagg 1 size 2 name "<name>" admin state enable
```
</details>

<details>
    <summary>Set Port Security</summary>
    
## Port Security Settings
```
port-security port 1/1/11 maximum 3
port-security port 1/1/11 learn-trap-threshold 3
port-security port 1/1/11 admin-state enable
```
</details>

<details>
    <summary>Spanning Tree Commands</summary>
    
## Spantree
```
show spantree <vlan 10>

show spantree ports

show spantree ports active
```
</details>

